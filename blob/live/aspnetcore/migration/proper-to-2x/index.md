---
title: "Migration d’ASP.NET vers ASP.NET Core 2.0"
author: isaac2004
description: "Ce document de référence fournit de l’aide sur la migration d’applications ASP.NET MVC ou API web ASP.NET existantes vers ASP.NET Core 2.0."
ms.author: scaddie
manager: wpickett
ms.date: 08/27/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: migration/proper-to-2x/index
ms.openlocfilehash: 96e645129fa53b10d352dcfda8f1ebb152c4dbac
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="migrating-from-aspnet-to-aspnet-core-20"></a><span data-ttu-id="3e3c2-103">Migration d’ASP.NET vers ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="3e3c2-103">Migrating from ASP.NET to ASP.NET Core 2.0</span></span>

<span data-ttu-id="3e3c2-104">De [Isaac Levin](https://isaaclevin.com)</span><span class="sxs-lookup"><span data-stu-id="3e3c2-104">By [Isaac Levin](https://isaaclevin.com)</span></span>

<span data-ttu-id="3e3c2-105">Cet article sert de guide de référence pour la migration d’applications ASP.NET vers ASP.NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-105">This article serves as a reference guide for migrating ASP.NET applications to ASP.NET Core 2.0.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e3c2-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="3e3c2-106">Prerequisites</span></span>

* <span data-ttu-id="3e3c2-107">[SDK .NET Core 2.0.0](https://dot.net/core) ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="3e3c2-107">[.NET Core 2.0.0 SDK](https://dot.net/core) or later.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="3e3c2-108">Versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3e3c2-108">Target Frameworks</span></span>
<span data-ttu-id="3e3c2-109">Les projets ASP.NET Core 2.0 permettent aux développeurs de cibler le .NET Core, le .NET Framework ou les deux.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-109">ASP.NET Core 2.0 projects offer developers the flexibility of targeting .NET Core, .NET Framework, or both.</span></span> <span data-ttu-id="3e3c2-110">Consultez [Choix entre le .NET Core et le .NET Framework pour les applications serveur](https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server) afin de déterminer quel est le framework cible le plus approprié.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-110">See [Choosing between .NET Core and .NET Framework for server apps](https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server) to determine which target framework is most appropriate.</span></span>

<span data-ttu-id="3e3c2-111">Quand vous ciblez le .NET Framework, les projets doivent référencer des packages NuGet individuels.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-111">When targeting .NET Framework, projects need to reference individual NuGet packages.</span></span>

<span data-ttu-id="3e3c2-112">Le ciblage du .NET Core vous permet d’éliminer de nombreuses références de packages explicites, grâce au [métapackage](xref:fundamentals/metapackage) ASP.NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-112">Targeting .NET Core allows you to eliminate numerous explicit package references, thanks to the ASP.NET Core 2.0 [metapackage](xref:fundamentals/metapackage).</span></span> <span data-ttu-id="3e3c2-113">Installez le métapackage `Microsoft.AspNetCore.All` dans votre projet :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-113">Install the `Microsoft.AspNetCore.All` metapackage in your project:</span></span>

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.0" />
</ItemGroup>
```

<span data-ttu-id="3e3c2-114">Quand le métapackage est utilisé, aucun package référencé dans le métapackage n’est déployé avec l’application.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-114">When the metapackage is used, no packages referenced in the metapackage are deployed with the app.</span></span> <span data-ttu-id="3e3c2-115">Le magasin de runtimes du .NET Core inclut ces composants. Ceux-ci sont précompilés pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-115">The .NET Core Runtime Store includes these assets, and they are precompiled to improve performance.</span></span> <span data-ttu-id="3e3c2-116">Pour plus d’informations, consultez [Métapackage Microsoft.AspNetCore.All pour ASP.NET Core 2.x](xref:fundamentals/metapackage).</span><span class="sxs-lookup"><span data-stu-id="3e3c2-116">See [Microsoft.AspNetCore.All metapackage for ASP.NET Core 2.x](xref:fundamentals/metapackage) for more detail.</span></span>

## <a name="project-structure-differences"></a><span data-ttu-id="3e3c2-117">Différences de structure de projet</span><span class="sxs-lookup"><span data-stu-id="3e3c2-117">Project structure differences</span></span>
<span data-ttu-id="3e3c2-118">Le format de fichier *.csproj* a été simplifié dans ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-118">The *.csproj* file format has been simplified in ASP.NET Core.</span></span> <span data-ttu-id="3e3c2-119">Voici certains changements notables :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-119">Some notable changes include:</span></span>
- <span data-ttu-id="3e3c2-120">Il n’est pas nécessaire d’inclure explicitement les fichiers pour qu’ils soient considérés comme faisant partie du projet.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-120">Explicit inclusion of files is not necessary for them to be considered part of the project.</span></span> <span data-ttu-id="3e3c2-121">Cela réduit le risque de conflits de fusion XML quand vous travaillez avec des équipes de grande taille.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-121">This reduces the risk of XML merge conflicts when working on large teams.</span></span>
- <span data-ttu-id="3e3c2-122">Il n’existe aucune référence basée sur un GUID à d’autres projets, ce qui améliore la lisibilité du fichier.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-122">There are no GUID-based references to other projects, which improves file readability.</span></span>
- <span data-ttu-id="3e3c2-123">Vous pouvez modifier le fichier sans devoir le décharger dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-123">The file can be edited without unloading it in Visual Studio:</span></span>

    ![Option de menu contextuel de modification du CSPROJ dans Visual Studio 2017](_static/EditProjectVs2017.png)

## <a name="globalasax-file-replacement"></a><span data-ttu-id="3e3c2-125">Remplacement du fichier Global.asax</span><span class="sxs-lookup"><span data-stu-id="3e3c2-125">Global.asax file replacement</span></span>
<span data-ttu-id="3e3c2-126">ASP.NET Core a introduit un nouveau mécanisme pour le démarrage d’une application.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-126">ASP.NET Core introduced a new mechanism for bootstrapping an app.</span></span> <span data-ttu-id="3e3c2-127">Le point d’entrée des applications ASP.NET est le fichier *Global.asax*.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-127">The entry point for ASP.NET applications is the *Global.asax* file.</span></span> <span data-ttu-id="3e3c2-128">Les tâches telles que la configuration de l’itinéraire ou l’inscription des filtres et des zones sont traitées dans le fichier *Global.asax*.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-128">Tasks such as route configuration and filter and area registrations are handled in the *Global.asax* file.</span></span>

[!code-csharp[Main](samples/globalasax-sample.cs)]

<span data-ttu-id="3e3c2-129">Cette approche couple l’application au serveur sur lequel elle est déployée d’une manière qui interfère avec l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-129">This approach couples the application and the server to which it's deployed in a way that interferes with the implementation.</span></span> <span data-ttu-id="3e3c2-130">Pour y remédier, [OWIN](http://owin.org/) a donc été introduit afin d’optimiser l’utilisation de plusieurs frameworks à la fois.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-130">In an effort to decouple, [OWIN](http://owin.org/) was introduced to provide a cleaner way to use multiple frameworks together.</span></span> <span data-ttu-id="3e3c2-131">OWIN fournit un pipeline qui permet d’ajouter uniquement les modules nécessaires.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-131">OWIN provides a pipeline to add only the modules needed.</span></span> <span data-ttu-id="3e3c2-132">L’environnement d’hébergement utilise une fonction [Startup](xref:fundamentals/startup) pour configurer les services et le pipeline de requêtes de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-132">The hosting environment takes a [Startup](xref:fundamentals/startup) function to configure services and the app's request pipeline.</span></span> <span data-ttu-id="3e3c2-133">`Startup` inscrit un ensemble d’intergiciels (middleware) auprès de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-133">`Startup` registers a set of middleware with the application.</span></span> <span data-ttu-id="3e3c2-134">Pour chaque requête, l’application appelle chacun des composants intergiciels (middleware) à l’aide du pointeur d’en-tête d’une liste liée à un ensemble existant de gestionnaires.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-134">For each request, the application calls each of the the middleware components with the head pointer of a linked list to an existing set of handlers.</span></span> <span data-ttu-id="3e3c2-135">Chaque composant intergiciel (middleware) peut ajouter un ou plusieurs gestionnaires au pipeline de traitement des requêtes.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-135">Each middleware component can add one or more handlers to the request handling pipeline.</span></span> <span data-ttu-id="3e3c2-136">Pour ce faire, une référence doit être retournée au gestionnaire qui représente le nouvel en-tête de la liste.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-136">This is accomplished by returning a reference to the handler that is the new head of the list.</span></span> <span data-ttu-id="3e3c2-137">Chaque gestionnaire doit mémoriser et appeler le prochain gestionnaire de la liste.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-137">Each handler is responsible for remembering and invoking the next handler in the list.</span></span> <span data-ttu-id="3e3c2-138">Avec ASP.NET Core, comme le point d’entrée d’une application est `Startup`, vous n’avez plus de dépendance relative à *Global.asax*.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-138">With ASP.NET Core, the entry point to an application is `Startup`, and you no longer have a dependency on *Global.asax*.</span></span> <span data-ttu-id="3e3c2-139">Quand vous employez OWIN avec le .NET Framework, utilisez l’exemple de code suivant en tant que pipeline :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-139">When using OWIN with .NET Framework, use something like the following as a pipeline:</span></span>

[!code-csharp[Main](samples/webapi-owin.cs)]

<span data-ttu-id="3e3c2-140">Cela permet de configurer vos itinéraires par défaut, et de privilégier XmlSerialization à JSON.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-140">This configures your default routes, and defaults to XmlSerialization over Json.</span></span> <span data-ttu-id="3e3c2-141">Ajoutez d’autres intergiciels (middleware) à ce pipeline selon les besoins (services de chargement, paramètres de configuration, fichiers statiques, etc.).</span><span class="sxs-lookup"><span data-stu-id="3e3c2-141">Add other Middleware to this pipeline as needed (loading services, configuration settings, static files, etc.).</span></span>

<span data-ttu-id="3e3c2-142">ASP.NET Core utilise une approche similaire mais n’a pas besoin d’OWIN pour prendre en charge l’entrée.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-142">ASP.NET Core uses a similar approach, but doesn't rely on OWIN to handle the entry.</span></span> <span data-ttu-id="3e3c2-143">À la place, l’opération est effectuée via la méthode `Main` de *Program.cs* (un peu comme pour les applications console) et `Startup` est chargé à partir de là.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-143">Instead, that is done through the *Program.cs* `Main` method (similar to console applications) and `Startup` is loaded through there.</span></span>

[!code-csharp[Main](samples/program.cs)]

<span data-ttu-id="3e3c2-144">`Startup` doit inclure une méthode `Configure`.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-144">`Startup` must include a `Configure` method.</span></span> <span data-ttu-id="3e3c2-145">Dans `Configure`, ajoutez l’intergiciel (middleware) nécessaire au pipeline.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-145">In `Configure`, add the necessary middleware to the pipeline.</span></span> <span data-ttu-id="3e3c2-146">Dans l’exemple suivant (provenant du modèle de site web par défaut), plusieurs méthodes d’extension permettent de configurer le pipeline pour une prise en charge des éléments ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-146">In the following example (from the default web site template), several extension methods are used to configure the pipeline with support for:</span></span>

* [<span data-ttu-id="3e3c2-147">BrowserLink</span><span class="sxs-lookup"><span data-stu-id="3e3c2-147">BrowserLink</span></span>](http://vswebessentials.com/features/browserlink)
* <span data-ttu-id="3e3c2-148">Pages d’erreur</span><span class="sxs-lookup"><span data-stu-id="3e3c2-148">Error pages</span></span>
* <span data-ttu-id="3e3c2-149">Fichiers statiques</span><span class="sxs-lookup"><span data-stu-id="3e3c2-149">Static files</span></span>
* <span data-ttu-id="3e3c2-150">ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="3e3c2-150">ASP.NET Core MVC</span></span>
* <span data-ttu-id="3e3c2-151">identité</span><span class="sxs-lookup"><span data-stu-id="3e3c2-151">Identity</span></span>

[!code-csharp[Main](../../common/samples/WebApplication1/Startup.cs?highlight=8,9,10,14,17,19,21&start=58&end=84)]

<span data-ttu-id="3e3c2-152">L’hôte et l’application ont été découplés, ce qui permet de passer facilement plus tard à une autre plateforme.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-152">The host and application have been decoupled, which provides the flexibility of moving to a different platform in the future.</span></span>

<span data-ttu-id="3e3c2-153">**Remarque :** Pour obtenir des informations de référence plus approfondies sur le démarrage des applications dans ASP.NET Core et sur les intergiciels (middleware), consultez [Démarrage dans ASP.NET Core](xref:fundamentals/startup)</span><span class="sxs-lookup"><span data-stu-id="3e3c2-153">**Note:** For a more in-depth reference to ASP.NET Core Startup and Middleware, see [Startup in ASP.NET Core](xref:fundamentals/startup)</span></span>

## <a name="storing-configurations"></a><span data-ttu-id="3e3c2-154">Stockage des configurations</span><span class="sxs-lookup"><span data-stu-id="3e3c2-154">Storing Configurations</span></span>
<span data-ttu-id="3e3c2-155">ASP.NET prend en charge le stockage des paramètres.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-155">ASP.NET supports storing settings.</span></span> <span data-ttu-id="3e3c2-156">Ces paramètres sont utilisés, par exemple, pour prendre en charge l’environnement sur lequel les applications ont été déployées.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-156">These setting are used, for example, to support the environment to which the applications were deployed.</span></span> <span data-ttu-id="3e3c2-157">Habituellement, toutes les paires clé-valeur personnalisées sont stockées dans la section `<appSettings>` du fichier *Web.config* :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-157">A common practice was to store all custom key-value pairs in the `<appSettings>` section of the *Web.config* file:</span></span>

[!code-xml[Main](samples/webconfig-sample.xml)]

<span data-ttu-id="3e3c2-158">Les applications lisent ces paramètres à l’aide de la collection `ConfigurationManager.AppSettings` dans l’espace de noms `System.Configuration` :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-158">Applications read these settings using the `ConfigurationManager.AppSettings` collection in the `System.Configuration` namespace:</span></span>

[!code-csharp[Main](samples/read-webconfig.cs)]

<span data-ttu-id="3e3c2-159">ASP.NET Core peut stocker les données de configuration de l’application dans un fichier et les charger dans le cadre du démarrage d’un intergiciel (middleware).</span><span class="sxs-lookup"><span data-stu-id="3e3c2-159">ASP.NET Core can store configuration data for the application in any file and load them as part of middleware bootstrapping.</span></span> <span data-ttu-id="3e3c2-160">Le fichier par défaut utilisé dans les modèles de projet est *appsettings.json* :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-160">The default file used in the project templates is *appsettings.json*:</span></span>

[!code-json[Main](samples/appsettings-sample.json)]

<span data-ttu-id="3e3c2-161">Le chargement de ce fichier dans une instance de `IConfiguration` au sein de votre application s’effectue dans *Startup.cs* :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-161">Loading this file into an instance of `IConfiguration` inside your application is done in *Startup.cs*:</span></span>

[!code-csharp[Main](samples/startup-builder.cs)]

<span data-ttu-id="3e3c2-162">L’application lit `Configuration` pour obtenir les paramètres :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-162">The app reads from `Configuration` to get the settings:</span></span>

[!code-csharp[Main](samples/read-appsettings.cs)]

<span data-ttu-id="3e3c2-163">Il existe des extensions à cette approche pour rendre le processus plus robuste, par exemple en utilisant l’[injection de dépendances](xref:fundamentals/dependency-injection) pour charger un service avec ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-163">There are extensions to this approach to make the process more robust, such as using [Dependency Injection](xref:fundamentals/dependency-injection) (DI) to load a service with these values.</span></span> <span data-ttu-id="3e3c2-164">L’approche par injection de dépendances fournit un ensemble d’objets de configuration fortement typés.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-164">The DI approach provides a strongly-typed set of configuration objects.</span></span>

````csharp
// Assume AppConfiguration is a class representing a strongly-typed version of AppConfiguration section
services.Configure<AppConfiguration>(Configuration.GetSection("AppConfiguration"));
````

<span data-ttu-id="3e3c2-165">**Remarque :** Pour obtenir des informations de référence plus approfondies sur la configuration d’ASP.NET Core, consultez [Configuration dans ASP.NET Core](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="3e3c2-165">**Note:** For a more in-depth reference to ASP.NET Core configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

## <a name="native-dependency-injection"></a><span data-ttu-id="3e3c2-166">Injection de dépendances native</span><span class="sxs-lookup"><span data-stu-id="3e3c2-166">Native Dependency Injection</span></span>
<span data-ttu-id="3e3c2-167">Quand vous générez des applications majeures et scalables, il est important d’avoir un couplage faible entre les composants et les services.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-167">An important goal when building large, scalable applications is the loose coupling of components and services.</span></span> <span data-ttu-id="3e3c2-168">L’[injection de dépendances](xref:fundamentals/dependency-injection) est une technique répandue qui permet d’y parvenir. Elle représente un composant natif d’ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-168">[Dependency Injection](xref:fundamentals/dependency-injection) is a popular technique for achieving this, and it is a native component of ASP.NET Core.</span></span>

<span data-ttu-id="3e3c2-169">Dans les applications ASP.NET, les développeurs s’appuient sur une bibliothèque tierce pour implémenter l’injection de dépendances.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-169">In ASP.NET applications, developers rely on a third-party library to implement Dependency Injection.</span></span> <span data-ttu-id="3e3c2-170">L’une de ces bibliothèques, [Unity](https://github.com/unitycontainer/unity), est fournie par Microsoft Patterns & Practices.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-170">One such library is [Unity](https://github.com/unitycontainer/unity), provided by Microsoft Patterns & Practices.</span></span> 

<span data-ttu-id="3e3c2-171">L’implémentation de `IDependencyResolver` qui inclut `UnityContainer` dans un wrapper est un exemple de configuration d’une injection de dépendances avec Unity :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-171">An example of setting up Dependency Injection with Unity is implementing `IDependencyResolver` that wraps a `UnityContainer`:</span></span>

[!code-csharp[Main](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample8.cs)]

<span data-ttu-id="3e3c2-172">Créez une instance de `UnityContainer`, inscrivez votre service, puis définissez le programme de résolution de dépendances de `HttpConfiguration` en fonction de la nouvelle instance de `UnityResolver` pour votre conteneur :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-172">Create an instance of your `UnityContainer`, register your service, and set the dependency resolver of `HttpConfiguration` to the new instance of `UnityResolver` for your container:</span></span>

[!code-csharp[Main](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample9.cs)]

<span data-ttu-id="3e3c2-173">Injectez `IProductRepository` aux emplacements nécessaires :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-173">Inject `IProductRepository` where needed:</span></span>

[!code-csharp[Main](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample5.cs)]

<span data-ttu-id="3e3c2-174">Dans la mesure où l’injection de dépendances fait partie d’ASP.NET Core, vous pouvez ajouter votre service à la méthode `ConfigureServices` de *Startup.cs* :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-174">Because Dependency Injection is part of ASP.NET Core, you can add your service in the `ConfigureServices` method of *Startup.cs*:</span></span>

[!code-csharp[Main](samples/configure-services.cs)]

<span data-ttu-id="3e3c2-175">Vous pouvez injecter le dépôt à l’emplacement de votre choix, comme c’était le cas avec Unity.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-175">The repository can be injected anywhere, as was true with Unity.</span></span>

<span data-ttu-id="3e3c2-176">**Remarque :** Pour obtenir des informations de référence sur l’injection de dépendances dans ASP.NET Core, consultez [Injection de dépendances dans ASP.NET Core](xref:fundamentals/dependency-injection#replacing-the-default-services-container)</span><span class="sxs-lookup"><span data-stu-id="3e3c2-176">**Note:** For an in-depth reference to dependency injection in ASP.NET Core, see [Dependency Injection in ASP.NET Core](xref:fundamentals/dependency-injection#replacing-the-default-services-container)</span></span>

## <a name="serving-static-files"></a><span data-ttu-id="3e3c2-177">Traitement des fichiers statiques</span><span class="sxs-lookup"><span data-stu-id="3e3c2-177">Serving Static Files</span></span>
<span data-ttu-id="3e3c2-178">Une partie importante du développement web réside dans la capacité de traitement des composants statiques, côté client.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-178">An important part of web development is the ability to serve static, client-side assets.</span></span> <span data-ttu-id="3e3c2-179">Les fichiers HTML, CSS, JavaScript et image sont les exemples les plus courants de fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-179">The most common examples of static files are HTML, CSS, Javascript, and images.</span></span> <span data-ttu-id="3e3c2-180">Ces fichiers doivent être enregistrés à l’emplacement publié de l’application (ou CDN) et référencés pour pouvoir être chargés par une requête.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-180">These files need to be saved in the published location of the app (or CDN) and referenced so they can be loaded by a request.</span></span> <span data-ttu-id="3e3c2-181">Ce processus a changé avec ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-181">This process has changed in ASP.NET Core.</span></span>

<span data-ttu-id="3e3c2-182">Avec ASP.NET, les fichiers statiques sont stockés dans différents répertoires et référencés dans des vues.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-182">In ASP.NET, static files are stored in various directories and referenced in the views.</span></span>

<span data-ttu-id="3e3c2-183">Avec ASP.NET Core, les fichiers statiques sont stockés à la « racine web » (*&lt;racine du contenu&gt;/wwwroot*), sauf si la configuration est différente.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-183">In ASP.NET Core, static files are stored in the "web root" (*&lt;content root&gt;/wwwroot*), unless configured otherwise.</span></span> <span data-ttu-id="3e3c2-184">Les fichiers sont chargés dans le pipeline de requêtes via l’appel de la méthode d’extension `UseStaticFiles` à partir de `Startup.Configure` :</span><span class="sxs-lookup"><span data-stu-id="3e3c2-184">The files are loaded into the request pipeline by invoking the `UseStaticFiles` extension method from `Startup.Configure`:</span></span>

[!code-csharp[Main](../../fundamentals/static-files/samples/1x/StartupStaticFiles.cs?highlight=3&name=snippet_ConfigureMethod)]

<span data-ttu-id="3e3c2-185">**Remarque :** Si vous ciblez le .NET Framework, installez le package NuGet `Microsoft.AspNetCore.StaticFiles`.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-185">**Note:** If targeting .NET Framework, install the NuGet package `Microsoft.AspNetCore.StaticFiles`.</span></span>

<span data-ttu-id="3e3c2-186">Par exemple, un composant image dans le dossier *wwwroot/images* est accessible au navigateur à un emplacement tel que `http://<app>/images/<imageFileName>`.</span><span class="sxs-lookup"><span data-stu-id="3e3c2-186">For example, an image asset in the *wwwroot/images* folder is accessible to the browser at a location such as `http://<app>/images/<imageFileName>`.</span></span>

<span data-ttu-id="3e3c2-187">**Remarque :** Pour obtenir des informations de référence plus approfondies sur le traitement des fichiers statiques dans ASP.NET Core, consultez [Présentation de l’utilisation des fichiers statiques dans ASP.NET Core](xref:fundamentals/static-files).</span><span class="sxs-lookup"><span data-stu-id="3e3c2-187">**Note:** For a more in-depth reference to serving static files in ASP.NET Core, see [Introduction to working with static files in ASP.NET Core](xref:fundamentals/static-files).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e3c2-188">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3e3c2-188">Additional Resources</span></span>
* [<span data-ttu-id="3e3c2-189">Portage des bibliothèques vers le .NET Core</span><span class="sxs-lookup"><span data-stu-id="3e3c2-189">Porting Libraries to .NET Core</span></span>](https://docs.microsoft.com/dotnet/core/porting/libraries)