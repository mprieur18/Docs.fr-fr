---
title: "Implémentation du serveur web HTTP.sys dans ASP.NET Core"
author: tdykstra
description: "Découvrez HTTP.sys, un serveur web pour ASP.NET Core sous Windows. Basé sur le pilote en mode noyau HTTP.sys, HTTP.sys est une solution qui permet d’établir une connexion directe à Internet sans IIS ni Kestrel."
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/httpsys
ms.openlocfilehash: d7ae6c070c7eecfd714086e15f32eff96c0943d9
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a>Implémentation du serveur web HTTP.sys dans ASP.NET Core

[Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher) et [Luke Latham](https://github.com/guardrex)

> [!NOTE]
> Cette rubrique s’applique à ASP.NET Core 2.0 et aux versions ultérieures. Dans les versions antérieures d’ASP.NET Core, HTTP.sys est appelé [WebListener](xref:fundamentals/servers/weblistener).

[HTTP.sys](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture#hypertext-transfer-protocol-stack-httpsys) est un [serveur web pour ASP.NET Core](xref:fundamentals/servers/index) qui s’exécute uniquement sous Windows. Il offre des fonctionnalités supplémentaires par rapport à [Kestrel](xref:fundamentals/servers/kestrel).

> [!IMPORTANT]
> HTTP.sys est incompatible avec le [Module ASP.NET Core](xref:fundamentals/servers/aspnet-core-module) et n’est pas utilisable avec IIS ni IIS Express.

HTTP.sys prend en charge les fonctionnalités suivantes :

* [Authentification Windows](xref:security/authentication/windowsauth)
* Partage de port
* HTTPS avec SNI
* HTTP/2 sur TLS (Windows 10 et versions ultérieures)
* Transmission de fichier directe
* Mise en cache des réponses
* WebSockets (Windows 8 et versions ultérieures)

Versions Windows prises en charge :

* Windows 7 ou version ultérieure
* Windows Server 2008 R2 ou une version ultérieure

[Affichez ou téléchargez l’exemple de code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample) ([procédure de téléchargement](xref:tutorials/index#how-to-download-a-sample))

## <a name="when-to-use-httpsys"></a>Quand utiliser HTTP.sys

HTTP.sys est utile pour les déploiements lorsque :

* Il est nécessaire d’exposer directement le serveur à Internet sans passer par IIS.

  ![HTTP.sys communique directement avec Internet](httpsys/_static/httpsys-to-internet.png)

* Un déploiement interne implique une fonctionnalité qui n’est pas disponible dans Kestrel, par exemple, [l’authentification Windows](xref:security/authentication/windowsauth).

  ![HTTP.sys communique directement avec le réseau interne](httpsys/_static/httpsys-to-internal.png)

HTTP.sys est une technologie aboutie qui assure une protection contre de nombreux types d’attaques et offre la robustesse, la sécurité et l’extensibilité d’un serveur web haut de gamme. Pour sa part, IIS s’exécute en tant qu’écouteur HTTP sur HTTP.sys. 

## <a name="how-to-use-httpsys"></a>Comment utiliser HTTP.sys

### <a name="configure-the-aspnet-core-app-to-use-httpsys"></a>Configurer l’application ASP.NET Core afin d’utiliser HTTP.sys

1. Il n’est pas nécessaire d’ajouter une référence de package dans le fichier projet dès lors que le [métapaquet Microsoft.AspNetCore.All](xref:fundamentals/metapackage) ([nuget.org](https://www.nuget.org/packages/Microsoft.AspNetCore.All/)) est utilisé (ASP.NET Core 2.0 et versions ultérieures). Si vous n'utilisez pas le métapaquet `Microsoft.AspNetCore.All`, ajoutez une référence de package à [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/).

1. Appelez la méthode d’extension [UseHttpSys](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderhttpsysextensions.usehttpsys) au moment de générer l’hôte web, en spécifiant les [options HTTP.sys](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions) requises :

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=4-12)]

   Le reste de la configuration de HTTP.sys est géré par le biais des [paramètres du Registre](https://support.microsoft.com/kb/820129).

   **Options HTTP.sys**

   | Propriété | Description | Par défaut |
   | -------- | ----------- | :-----: |
   | [AllowSynchronousIO](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.allowsynchronousio) | Contrôle si l’entrée/sortie synchrone est autorisée pour le `HttpContext.Request.Body` et le `HttpContext.Response.Body`. | `true` |
   | [Authentication.AllowAnonymous](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationmanager.allowanonymous) | Autorise les requêtes anonymes. | `true` |
   | [Authentication.Schemes](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationmanager.schemes) | Spécifie les schémas d’authentification autorisés. Peut être modifié à tout moment avant la suppression de l’écouteur. Les valeurs sont fournies par [l’enum AuthenticationSchemes](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationschemes) : `Basic`, `Kerberos`, `Negotiate`, `None` et `NTLM`. | `None` |
   | [EnableResponseCaching](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.enableresponsecaching) | Tente la mise en cache [en mode noyau](/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) pour les réponses comportant un en-tête compatible. La réponse peut ne pas inclure d’en-tête `Set-Cookie`, `Vary` ou `Pragma`. Elle doit comporter un en-tête `Cache-Control` `public` et soit une valeur `shared-max-age` ou `max-age`, soit un en-tête `Expires`. | `true` |
   | [MaxAccepts](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxaccepts) | Nombre maximal d'acceptations simultanées. | 5 &times; [Environment.<br>ProcessorCount](/dotnet/api/system.environment.processorcount) |
   | [MaxConnections](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxconnections) | Nombre maximum de connexions simultanées à accepter. Utilisez `-1` pour signifier l’infini, et `null` pour utiliser le paramètre du Registre qui s’applique à l’ordinateur dans son ensemble. | `null`<br>(illimité) |
   | [MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize) | Consultez la section <a href="#maxrequestbodysize">MaxRequestBodySize</a>. | 30 000 000 octets<br>(env. 28,6 Mo) |
   | [RequestQueueLimit](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.requestqueuelimit) | Nombre maximal de demandes pouvant être placées en file d'attente. | 1000 |
   | [ThrowWriteExceptions](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.throwwriteexceptions) | Indique si les écritures dans le corps de la réponse qui échouent en raison d’une déconnexion du client doivent lever des exceptions ou se terminer normalement. | `false`<br>(se terminer normalement) |
   | [Timeouts](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts) | Expose la configuration [TimeoutManager](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager) de HTTP.sys, également paramétrable dans le Registre. Suivez les liens de l’API pour en savoir plus sur chaque paramètre, y compris les valeurs par défaut :<ul><li>[Timeouts.DrainEntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.drainentitybody) &ndash; Temps alloué à l’API de serveur HTTP pour décharger le corps de l’entité sur une connexion persistante.</li><li>[Timeouts.EntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.entitybody) &ndash; Temps alloué pour que le corps de l'entité de la demande arrive.</li><li>[Timeouts.HeaderWait](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.headerwait) &ndash; Temps alloué à l’API de serveur HTTP pour analyser l’en-tête de la demande.</li><li>[Timeouts.IdleConnection](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.idleconnection) &ndash; Temps alloué pour une connexion inactive.</li><li>[Timeouts.MinSendBytesPerSecond](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.minsendbytespersecond) &ndash; Taux d’envoi minimal de la réponse.</li><li>[Timeouts.RequestQueue](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.requestqueue) &ndash; Temps alloué à la demande pour rester dans la file d’attente des demandes avant que l’application ne la récupère.</li></ul> |  |
   | [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes) | Spécifiez la [UrlPrefixCollection](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection) à inscrire auprès de HTTP.sys. La plus utile est [UrlPrefixCollection.Add](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection.add), qui permet d’ajouter un préfixe à la collection. Ces choix peuvent être modifiés à tout moment avant la suppression de l’écouteur. |  |

   <a name="maxrequestbodysize"></a>
   **MaxRequestBodySize**

   Taille maximale autorisée pour le corps d’une demande, en octets. Lorsque la valeur est `null`, elle est illimitée. Cette limite est sans effet sur les connexions mises à niveau, qui sont illimitées.

   Pour remplacer la limite d’un seul `IActionResult` dans une application MVC ASP.NET Core, nous vous recommandons d’utiliser l’attribut [RequestSizeLimitAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) sur une méthode d’action :
   
   ```csharp
   [RequestSizeLimit(100000000)]
   public IActionResult MyActionMethod()
   ```

   Une exception est levée si l’application tente de configurer la limite sur une demande dont l’application a commencé la lecture. La propriété `IsReadOnly` indique si la propriété `MaxRequestBodySize` est en lecture seule, et donc s’il est trop tard pour configurer la limite.

   Si l’application doit remplacer [MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize) demande par demande, utilisez [IHttpMaxRequestBodySizeFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpmaxrequestbodysizefeature) :

   [!code-csharp[](httpsys/sample/Startup.cs?name=snippet1&highlight=6-7)]

1. Si vous utilisez Visual Studio, vérifiez que l’application n’est pas configurée pour exécuter IIS ou IIS Express.

   Dans Visual Studio, le profil de démarrage par défaut est destiné à IIS Express. Pour exécuter le projet en tant qu’application console, changez manuellement le profil sélectionné, comme dans la capture d’écran suivante :

   ![Sélectionner le profil d’application console](httpsys/_static/vs-choose-profile.png)

### <a name="configure-windows-server"></a>Configurer Windows Server

1. Si l’application est un [déploiement dépendant de .NET Framework](/dotnet/core/deploying/#framework-dependent-deployments-fdd), installez .NET Core, .NET Framework ou les deux (si l’application est une application .NET Core ciblant .NET Framework).

   * **.NET Core** &ndash; Si l’application requiert .NET Core, allez chercher et exécutez le programme d’installation de .NET Core sur [Téléchargements .NET](https://www.microsoft.com/net/download/windows).
   * **.NET Framework** &ndash; Si l’application requiert .NET Framework, consultez la page [.NET Framework : guide d’installation](/dotnet/framework/install/) pour connaître les instructions d’installation. Installez la version requise de .NET Framework. Le programme d’installation de la dernière version de .NET Framework se trouve sur la page [Téléchargements .NET](https://www.microsoft.com/net/download/windows).

1. Configurez les ports et les URL de l’application.

   Par défaut, ASP.NET Core est lié à `http://localhost:5000`. Pour configurer les ports et les préfixes d’URL, il existe plusieurs possibilités :

   * [UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls)
   * Arguments de ligne de commande `urls`
   * Variable d’environnement `ASPNETCORE_URLS`
   * [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes)

   L’exemple de code suivant montre comment utiliser [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes) :

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=11)]

   `UrlPrefixes` présente l’avantage de générer immédiatement un message d’erreur en cas de préfixe mal formé.

   Les paramètres de `UrlPrefixes` remplacent les paramètres `UseUrls`/`urls`/`ASPNETCORE_URLS`. Par conséquent, avec `UseUrls`, `urls` et la variable d’environnement `ASPNETCORE_URLS`, il est plus facile de basculer entre Kestrel et HTTP.sys. Pour plus d’informations sur `UseUrls`, `urls` et `ASPNETCORE_URLS`, consultez la section [Hébergement](xref:fundamentals/hosting).

   HTTP.sys utilise les [formats de chaîne UrlPrefix de l’API de serveur HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).

   > [!WARNING]
   > Les liaisons génériques de niveau supérieur (`http://*:80/` et `http://+:80`) ne doivent **pas** être utilisées. Les liaisons génériques de niveau supérieur peuvent exposer votre application à des failles de sécurité. Cela s’applique aux caractères génériques forts et faibles. Utilisez des noms d’hôte explicites plutôt que des caractères génériques. Une liaison générique de sous-domaine (par exemple, `*.mysub.com`) ne présente pas ce risque de sécurité si vous contrôlez le domaine parent en entier (par opposition à `*.com`, qui est vulnérable). Consultez la [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) pour plus d’informations.

1. Préinscrivez les préfixes d’URL à lier à HTTP.sys et configurez les certificats x.509.

   Si les préfixes d’URL ne sont pas préinscrits sous Windows, exécutez l’application avec des privilèges Administrateur. Il existe une seule exception : si vous effectuez une liaison à localhost avec HTTP (et non HTTPS) et un numéro de port supérieur à 1024, les privilèges Administrateur ne sont pas nécessaires.

   1. L’outil intégré pour configurer HTTP.sys est *netsh.exe*. *netsh.exe* permet de réserver des préfixes d’URL et d’assigner des certificats X.509. L’outil requiert des privilèges Administrateur.

      L’exemple suivant montre les commandes à effectuer pour réserver des préfixes d’URL aux ports 80 et 443 :

      ```console
      netsh http add urlacl url=http://+:80/ user=Users
      netsh http add urlacl url=https://+:443/ user=Users
      ```

      L’exemple suivant montre comment assigner un certificat X.509 :

      ```console
      netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}"
      ```

      Documentation de référence de *netsh.exe* :

      * [Commandes netsh pour HTTP (Hypertext Transfer Protocol)](https://technet.microsoft.com/library/cc725882.aspx)
      * [Chaînes UrlPrefix](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

   1. Créez des certificats X.509 auto-signés, si nécessaire.

     [!INCLUDE[How to make an X.509 cert](../../includes/make-x509-cert.md)]

1. Ouvrez des ports du pare-feu pour autoriser le trafic à atteindre HTTP.sys. Utilisez *netsh.exe* ou les [cmdlets PowerShell](https://technet.microsoft.com/library/jj554906).

## <a name="additional-resources"></a>Ressources supplémentaires

* [API de serveur HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)
* [Référentiel GitHub aspnet/HttpSysServer (code source)](https://github.com/aspnet/HttpSysServer/)
* [Hébergement d’applications WPF](xref:fundamentals/hosting)
