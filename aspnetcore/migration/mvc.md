---
title: Migrer à partir de ASP.NET MVC à cœur d’ASP.NET MVC
author: ardalis
description: Découvrez comment commencer la migration vers ASP.NET MVC de base d’un projet ASP.NET MVC.
manager: wpickett
ms.author: riande
ms.date: 03/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/mvc
ms.openlocfilehash: e249be06726b307a1c41a525a132f7e0ab8b50ee
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
---
# <a name="migrate-from-aspnet-mvc-to-aspnet-core-mvc"></a>Migrer à partir de ASP.NET MVC à cœur d’ASP.NET MVC

Par [Rick Anderson](https://twitter.com/RickAndMSFT), [Michel Roth](https://github.com/danroth27), [Steve Smith](https://ardalis.com/), et [Scott Addie](https://scottaddie.com)

Cet article explique comment commencer la migration d’un projet ASP.NET MVC à [ASP.NET Core MVC](../mvc/overview.md). Dans le processus, il présente la plupart des éléments qui ont été modifiés dans ASP.NET MVC. Migration à partir d’ASP.NET MVC est un processus en plusieurs étapes, et cet article couvre la configuration initiale, contrôleurs de base et les vues, contenu statique et dépendances du côté client. Autres articles couvrent la migration de la configuration et le code d’identité trouvée dans de nombreux projets ASP.NET MVC.

> [!NOTE]
> Les numéros de version dans les exemples ne sont peut-être pas ceux en cours. Vous devrez peut-être mettre à jour vos projets en conséquence.

## <a name="create-the-starter-aspnet-mvc-project"></a>Créer le projet ASP.NET MVC starter

Pour illustrer la mise à niveau, nous allons commencer par la création d’une application ASP.NET MVC. Créez-la avec le nom *WebApp1* pour que l’espace de noms corresponde au projet ASP.NET Core que nous créons à l’étape suivante.

![Boîte de dialogue Visual Studio nouveau projet](mvc/_static/new-project.png)

![Boîte de dialogue nouvelle Application Web : modèle de projet MVC sélectionné dans le panneau de configuration de modèles ASP.NET](mvc/_static/new-project-select-mvc-template.png)

 *Facultatif :* Changez le nom de la solution de *WebApp1* en *Mvc5*. Visual Studio affichera le nouveau nom de la solution (*Mvc5*), ce qui permettra de distinguer plus facilement ce projet du projet suivant.

## <a name="create-the-aspnet-core-project"></a>Créer le projet ASP.NET Core

Créez une nouvelle application web ASP.NET Core *vide* avec le même nom que le projet précédent (*WebApp1*) afin de faire correspondre les espaces de noms dans les deux projets. Avoir le même espace de noms rend plus facile la copie de code entre les deux projets. Vous devez créer ce projet dans un autre répertoire que le projet précédent pour utiliser le même nom.

![Boîte de dialogue Nouveau projet](mvc/_static/new_core.png)

![Boîte de dialogue nouvelle Application Web ASP.NET : modèle de projet vide sélectionnée dans le panneau de configuration de modèles de base ASP.NET](mvc/_static/new-project-select-empty-aspnet5-template.png)

* *Facultatif :* créer une nouvelle application ASP.NET Core à l’aide du *Application Web* modèle de projet. Nommez le projet *WebApp1*, puis sélectionnez une option d’authentification de **comptes d’utilisateur individuels**. Renommer cette application *FullAspNetCore*. Création de ce projet seront gagner du temps lors de la conversion. Vous pouvez examiner le code généré de modèle pour afficher le résultat final ou copiez le code dans le projet de conversion. Il est également utile lorsque vous êtes bloqué sur une étape de conversion à comparer avec le projet de modèle généré.

## <a name="configure-the-site-to-use-mvc"></a>Configurer le site pour utiliser MVC

* Installez les packages NuGet `Microsoft.AspNetCore.Mvc` et `Microsoft.AspNetCore.StaticFiles`.

  `Microsoft.AspNetCore.Mvc` est le framework ASP.NET Core MVC. `Microsoft.AspNetCore.StaticFiles` est le Gestionnaire de fichiers statiques. Le runtime ASP.NET est modulaire, et vous devez explicitement s’abonner à des fichiers statiques (consultez [travailler avec des fichiers statiques](../fundamentals/static-files.md)).

* Ouvrez le *.csproj* fichier (avec le bouton droit dans le projet de **l’Explorateur de solutions** et sélectionnez **WebApp1.csproj de modifier**) et ajoutez une cible `PrepareForPublish` :

  [!code-xml[](mvc/sample/WebApp1.csproj?range=21-23)]

  La cible `PrepareForPublish` est nécessaire pour l’acquisition des bibliothèques côté client via Bower. Nous en parlerons plus tard.

* Ouvrez le fichier *Startup.cs* et modifiez le code comme suit :

  [!code-csharp[](mvc/sample/Startup.cs?highlight=14,27-34)]

  La méthode d’extension `UseStaticFiles` ajoute le Gestionnaire de fichiers statiques. Comme mentionné précédemment, le runtime ASP.NET est modulaire, et vous devez explicitement autoriser les fichiers statiques. La méthode d’extension `UseMvc` ajoute le routage. Pour plus d’informations, consultez [démarrage de l’Application](../fundamentals/startup.md) et [routage](../fundamentals/routing.md).

## <a name="add-a-controller-and-view"></a>Ajouter un contrôleur et une vue

Dans cette section, vous allez ajouter un contrôleur minimal et la vue comme des espaces réservés pour le contrôleur ASP.NET MVC et les vues que vous allez migrer dans la section suivante.

* Ajoutez un dossier *contrôleurs*.

* Ajoutez une **classe de contrôleur MVC** portant le nom *HomeController.cs* au dossier *contrôleurs*.

![Boîte de dialogue Ajouter un nouvel élément](mvc/_static/add_mvc_ctl.png)

* Ajoutez un dossier *Views*.

* Ajoutez un dossier *Views/Home*.

* Ajoutez une page de vue MVC *Index.cshtml* au dossier *Views/Home*.

![Boîte de dialogue Ajouter un nouvel élément](mvc/_static/view.png)

La structure de projet est indiquée ci-dessous :

![Explorateur de solutions affichant les fichiers et dossiers de WebApp1](mvc/_static/project-structure-controller-view.png)

Remplacez le contenu du fichier *Views/Home/Index.cshtml* avec les éléments suivants :

```html
<h1>Hello world!</h1>
```

Exécuter l’application.

![Application Web ouverte dans Microsoft Edge](mvc/_static/hello-world.png)

Consultez [contrôleurs](xref:mvc/controllers/actions) et [vues](xref:mvc/views/overview) pour plus d’informations.

Maintenant que nous avons un projet ASP.NET Core minimal, nous pouvons commencer la migration des fonctionnalités à partir du projet ASP.NET MVC. Vous devrez déplacer les éléments suivants :

* Contenu côté client (CSS, polices et scripts)

* Contrôleurs

* Vues

* Modèles

* Regroupement

* Filtres

* Connexion/déconnexion, identité (ceci sera effectué dans le prochain didacticiel.)

## <a name="controllers-and-views"></a>Contrôleurs et vues

* Chacune des méthodes copier à partir de l’ASP.NET MVC `HomeController` au nouveau `HomeController`. Notez que dans ASP.NET MVC, type de retour de méthode de modèle prédéfini contrôleur action est [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult(v=vs.118).aspx); dans ASP.NET MVC de base, les méthodes d’action retournés `IActionResult` à la place. `ActionResult` implémente `IActionResult`, il est donc inutile de modifier le type de retour de vos méthodes d’action.

* Copiez les fichiers de vues Razor *About.cshtml*, *Contact.cshtml* et *Index.cshtml* du projet ASP.NET MVC dans le projet ASP.NET Core.

* Exécutez l’application ASP.NET Core et chaque méthode de test. Nous n’avons pas encore effectué la migration du fichier de mise en page ou des styles, donc les vues de rendu ne contiennent que le contenu des fichiers de vue. Comme vous ne disposez pas des liens générés du fichier de mise en page pour les vues `About` et `Contact`, vous devez les appeler à partir du navigateur (remplacez **4492** par le numéro de port utilisé dans votre projet).

  * `http://localhost:4492/home/about`

  * `http://localhost:4492/home/contact`

![Page de contact](mvc/_static/contact-page.png)

Notez l’absence de styles et d’éléments de menu. Nous le corrigerons dans la section suivante.

## <a name="static-content"></a>Contenu statique

Dans les versions précédentes d’ASP.NET MVC, le contenu statique était hébergé à partir de la racine du projet web et mélangé avec les fichiers côté serveur. Dans ASP.NET Core, le contenu statique est hébergé dans le dossier *wwwroot*. Vous devez copier le contenu statique de votre ancienne application ASP.NET MVC dans le dossier *wwwroot* de votre projet ASP.NET Core. Dans cette exemple de conversion :

* Copie le *favicon.ico* fichier à partir de l’ancien projet MVC dans le *wwwroot* dossier dans le projet ASP.NET Core.

L’ancien ASP.NET MVC project utilise [Bootstrap](http://getbootstrap.com/) pour que son style et le programme d’amorçage des fichiers dans le *contenu* et *Scripts* dossiers. Le modèle, ce qui a généré l’ancien projet ASP.NET MVC, fait référence à l’amorçage dans le fichier de disposition (*Views/Shared/_Layout.cshtml*). Vous pouvez copier le *bootstrap.js* et *bootstrap.css* à partir de l’ASP.NET MVC, les fichiers de projet pour le *wwwroot* n’utilise pas de dossier dans le nouveau projet, mais cette approche le mécanisme améliorée pour la gestion des dépendances de côté client dans ASP.NET Core.

Dans le nouveau projet, nous allons ajouter la prise en charge de Bootstrap (et d’autres bibliothèques côté client) à l’aide de [Bower](https://bower.io/):

* Ajoutez un fichier de configuration [Bower](https://bower.io/) nommé *bower.json* à la racine du projet (cliquez avec le bouton droit sur le projet, puis sur **AAjouter > Nouvel élément > Fichier de Configuration Bower**). Ajoutez [Bootstrap](http://getbootstrap.com/) et [jQuery](https://jquery.com/) au fichier (voir les lignes en surbrillance ci-dessous).

  [!code-json[](mvc/sample/bower.json?highlight=5-6)]

Lors de l’enregistrement du fichier, Bower télécharge automatiquement les dépendances dans le dossier *wwwroot/lib*. Vous pouvez utiliser la **zone de recherche dans l’Explorateur de solutions** pour rechercher le chemin des ressources :

![ressources de jQuery apparaissent dans les résultats de recherche de l’Explorateur de solutions](mvc/_static/search.png)

Consultez [Pour plus d’informations, consultez Gérer les packages côté client avec Bower](../client-side/bower.md) pour plus d’informations.

<a name="migrate-layout-file"></a>

## <a name="migrate-the-layout-file"></a>Migrer le fichier de disposition

* Copiez le fichier*_ViewStart.cshtml* à partir du dossier *Views* de l’ancien projet ASP.NET MVC dans le dossier *Views* du projet de ASP.NET Core. Le fichier *_ViewStart.cshtml* n’a pas changé dans ASP.NET Core MVC.

* Créez un dossier *Views/Shared*.

* *Facultatif :* copie *_ViewImports.cshtml* à partir de la *FullAspNetCore* du projet MVC *vues* dossier dans le projet de ASP.NET Core  *Vues* dossier. Supprimez toute déclaration d’espace de noms dans le *_ViewImports.cshtml* fichier. Le *_ViewImports.cshtml* fournit des espaces de noms pour tous les fichiers de l’affichage de fichiers et permet de bénéficier de [programmes d’assistance de balise](xref:mvc/views/tag-helpers/intro). Programmes d’assistance de balise sont utilisés dans le nouveau fichier de disposition. Le *_ViewImports.cshtml* fichier est une nouveauté pour ASP.NET Core.

* Copiez le fichier *_Layout.cshtml* à partir du dossier *Views/Shared* de l’ancien projet ASP.NET MVC dans le dossier *Views/Shared* du projet ASP.NET Core.

Ouvrez *_Layout.cshtml* et apportez les modifications suivantes (le code complet est indiqué ci-dessous) :

   * Remplacez `@Styles.Render("~/Content/css")` par un élément `<link>` pour charger *bootstrap.css* (voir ci-dessous).

   * Supprimez `@Scripts.Render("~/bundles/modernizr")`.

   * Commentez la ligne `@Html.Partial("_LoginPartial")` (en la plaçant entre `@*...*@`). Nous y reviendrons dans un prochain didacticiel.

   * Remplacez `@Scripts.Render("~/bundles/jquery")` par un élément `<script>` (voir ci-dessous).

   * Remplacez `@Scripts.Render("~/bundles/bootstrap")` par un élément `<script>` (voir ci-dessous).

Le lien CSS de remplacement :

```html
<link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.css" />
```

Les balises de script de remplacement :

```html
<script src="~/lib/jquery/dist/jquery.js"></script>
<script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
```

La mise à jour *_Layout.cshtml* fichier est présenté ci-dessous :

[!code-html[](mvc/sample/Views/Shared/_Layout.cshtml?highlight=7,27,39-40)]

Afficher le site dans le navigateur. Il doit maintenant charger correctement, avec les styles attendus en place.

* *Facultatif :* Vous pouvez essayer d’utiliser le nouveau fichier de mise en page. Pour ce projet, copiez le fichier de mise en page à partir du projet *FullAspNetCore*. Le nouveau fichier de mise en page utilise les [Tags Helpers](xref:mvc/views/tag-helpers/intro) et comprend d’autres améliorations.

## <a name="configure-bundling-and-minification"></a>Configurer le regroupement et minimisation

Pour plus d’informations sur la configuration du regroupement et de la minimisation, consultez [Regroupement et Minimisation](../client-side/bundling-and-minification.md).

## <a name="solving-http-500-errors"></a>Résolution des erreurs HTTP 500

De nombreux problèmes peuvent provoquer un message d’erreur HTTP 500 qui ne donne aucune information sur la source du problème. Par exemple, si le fichier *Views/_ViewImports.cshtml* contient un espace de noms qui n’existe pas dans votre projet, vous obtenez une erreur HTTP 500. Pour obtenir un message d’erreur détaillé, ajoutez le code suivant :

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    if (env.IsDevelopment())
    {
         app.UseDeveloperExceptionPage();
    }

    app.UseStaticFiles();

    app.UseMvc(routes =>
    {
        routes.MapRoute(
            name: "default",
            template: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

Consultez **à l’aide de la Page d’Exception Developer** dans [gérer les erreurs](../fundamentals/error-handling.md) pour plus d’informations.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Développement côté client](xref:client-side/index)
* [Les Tag Helpers](xref:mvc/views/tag-helpers/intro)
