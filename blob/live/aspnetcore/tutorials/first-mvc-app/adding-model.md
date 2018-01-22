---
title: "Ajout d’un modèle à une application ASP.NET Core MVC"
author: rick-anderson
description: "Ajoutez un modèle à une application ASP.NET Core simple."
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 12/8/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/adding-model
ms.openlocfilehash: 03c16e523fe2f91cae5c71357835684d813e3a1f
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model1.md)]

<span data-ttu-id="3163a-104">Remarque : Les modèles ASP.NET Core 2.0 contiennent le dossier *Models*.</span><span class="sxs-lookup"><span data-stu-id="3163a-104">Note: The ASP.NET Core 2.0 templates contain the *Models* folder.</span></span>

<span data-ttu-id="3163a-105">Cliquez avec le bouton droit sur le dossier *Models* > **Ajouter** > **Classe**.</span><span class="sxs-lookup"><span data-stu-id="3163a-105">Right-click the *Models* folder > **Add** > **Class**.</span></span> <span data-ttu-id="3163a-106">Nommez la classe **Movie**, puis ajoutez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3163a-106">Name the class **Movie** and add the following properties:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]

<span data-ttu-id="3163a-107">Le champ `ID` est nécessaire à la base de données pour la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="3163a-107">The `ID` field is required by the database for the primary key.</span></span> 

<span data-ttu-id="3163a-108">Générez le projet pour vérifier qu’il ne comporte aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="3163a-108">Build the project to verify you don't have any errors.</span></span> <span data-ttu-id="3163a-109">Vous avez désormais un **M**odèle dans votre application **M**VC.</span><span class="sxs-lookup"><span data-stu-id="3163a-109">You now have a **M**odel in your **M**VC app.</span></span>

## <a name="scaffolding-a-controller"></a><span data-ttu-id="3163a-110">Génération de modèles automatique pour un contrôleur</span><span class="sxs-lookup"><span data-stu-id="3163a-110">Scaffolding a controller</span></span>

<span data-ttu-id="3163a-111">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le dossier *Contrôleurs* **> Ajouter > Contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="3163a-111">In **Solution Explorer**, right-click the *Controllers* folder **> Add > Controller**.</span></span>

![affichage de l’étape ci-dessus](adding-model/_static/add_controller.png)

<span data-ttu-id="3163a-113">Si la boîte de dialogue **Ajouter des dépendances MVC** apparaît :</span><span class="sxs-lookup"><span data-stu-id="3163a-113">If the **Add MVC Dependencies** dialog appears:</span></span>

* <span data-ttu-id="3163a-114">[Effectuez la mise à jour de Visual Studio vers la dernière version](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3163a-114">[Update Visual Studio to the latest version](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="3163a-115">Les versions de Visual Studio antérieures à 15.5 affichent cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3163a-115">Visual Studio versions prior to 15.5 show this dialog.</span></span>
* <span data-ttu-id="3163a-116">Si vous ne pouvez pas effectuer la mise à jour, sélectionnez **ADD**, puis suivez à nouveau les étapes pour ajouter un contrôleur.</span><span class="sxs-lookup"><span data-stu-id="3163a-116">If you can't update, select **ADD**, and then follow the add controller steps again.</span></span>

<span data-ttu-id="3163a-117">Dans la boîte de dialogue **Ajouter un modèle automatique**, appuyez sur **Contrôleur MVC avec vues, utilisant Entity Framework > Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3163a-117">In the **Add Scaffold** dialog, tap **MVC Controller with views, using Entity Framework > Add**.</span></span>

![Boîte de dialogue Ajouter un modèle automatique](adding-model/_static/add_scaffold2.png)

<span data-ttu-id="3163a-119">Renseignez la boîte de dialogue **Ajouter un contrôleur** :</span><span class="sxs-lookup"><span data-stu-id="3163a-119">Complete the **Add Controller** dialog:</span></span>

* <span data-ttu-id="3163a-120">**Classe de modèle :** *Movie (MvcMovie.Models)*</span><span class="sxs-lookup"><span data-stu-id="3163a-120">**Model class:** *Movie (MvcMovie.Models)*</span></span>
* <span data-ttu-id="3163a-121">**Classe de contexte de données :** sélectionnez l’icône **+** et ajoutez le **MvcMovie.Models.MvcMovieContext** par défaut.</span><span class="sxs-lookup"><span data-stu-id="3163a-121">**Data context class:** Select the **+** icon and add the default **MvcMovie.Models.MvcMovieContext**</span></span>

![Ajouter un contexte de données](adding-model/_static/dc.png)

* <span data-ttu-id="3163a-123">**Affichages :** conservez la valeur par défaut de chaque option activée.</span><span class="sxs-lookup"><span data-stu-id="3163a-123">**Views:** Keep the default of each option checked</span></span>
* <span data-ttu-id="3163a-124">**Nom du contrôleur :** conservez la valeur par défaut *MoviesController*.</span><span class="sxs-lookup"><span data-stu-id="3163a-124">**Controller name:** Keep the default *MoviesController*</span></span>
* <span data-ttu-id="3163a-125">Appuyez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3163a-125">Tap **Add**</span></span>

![Boîte de dialogue Ajouter un contrôleur](adding-model/_static/add_controller2.png)

<span data-ttu-id="3163a-127">Visual Studio crée :</span><span class="sxs-lookup"><span data-stu-id="3163a-127">Visual Studio creates:</span></span>

* <span data-ttu-id="3163a-128">Une [classe de contexte de base de données](xref:data/ef-mvc/intro#create-the-database-context) Entity Framework Core (*Data/MvcMovieContext.cs*)</span><span class="sxs-lookup"><span data-stu-id="3163a-128">An Entity Framework Core [database context class](xref:data/ef-mvc/intro#create-the-database-context) (*Data/MvcMovieContext.cs*)</span></span>
* <span data-ttu-id="3163a-129">Un contrôleur de films (*Controllers/MoviesController.cs*)</span><span class="sxs-lookup"><span data-stu-id="3163a-129">A movies controller (*Controllers/MoviesController.cs*)</span></span>
* <span data-ttu-id="3163a-130">Des fichiers de vues Razor pour les pages Create, Delete, Details, Edit et Index (*Views/Movies/&ast;.cshtml*)</span><span class="sxs-lookup"><span data-stu-id="3163a-130">Razor view files for Create, Delete, Details, Edit, and Index pages (*Views/Movies/&ast;.cshtml*)</span></span>

<span data-ttu-id="3163a-131">La création automatique du contexte de base de données et de méthodes d’action et de vues [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (créer, lire, mettre à jour et supprimer) porte le nom de *génération de modèles automatique*.</span><span class="sxs-lookup"><span data-stu-id="3163a-131">The automatic creation of the database context and [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views is known as *scaffolding*.</span></span> <span data-ttu-id="3163a-132">Vous aurez bientôt une application web entièrement opérationnelle qui vous permettra de gérer une base de données de films.</span><span class="sxs-lookup"><span data-stu-id="3163a-132">You'll soon have a fully functional web application that lets you manage a movie database.</span></span>

<span data-ttu-id="3163a-133">Si vous exécutez l’application et que vous cliquez sur le lien **Mvc Movie**, vous recevez une erreur semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="3163a-133">If you run the app and click on the **Mvc Movie** link, you get an error similar to the following:</span></span>

```
An unhandled exception occurred while processing the request.

SqlException: Cannot open database "MvcMovieContext-<GUID removed>" requested by the login. The login failed.
Login failed for user 'Rick'.

System.Data.SqlClient.SqlInternalConnectionTds..ctor(DbConnectionPoolIdentity identity, SqlConnectionString 
```

<span data-ttu-id="3163a-134">Vous devez créer la base de données, et vous utiliserez pour cela la fonctionnalité [Migrations](xref:data/ef-mvc/migrations) d’EF Core.</span><span class="sxs-lookup"><span data-stu-id="3163a-134">You need to create the database, and you'll use the EF Core [Migrations](xref:data/ef-mvc/migrations) feature to do that.</span></span> <span data-ttu-id="3163a-135">Les migrations permettent de créer une base de données qui correspond à votre modèle de données, et de mettre à jour le schéma de base de données quand votre modèle de données change.</span><span class="sxs-lookup"><span data-stu-id="3163a-135">Migrations lets you create a database that matches your data model and update the database schema when your data model changes.</span></span>

## <a name="add-ef-tooling-and-perform-initial-migration"></a><span data-ttu-id="3163a-136">Ajouter les outils EF et effectuer la migration initiale</span><span class="sxs-lookup"><span data-stu-id="3163a-136">Add EF tooling and perform initial migration</span></span>

<span data-ttu-id="3163a-137">Dans cette section, vous allez utiliser la console du Gestionnaire de package pour :</span><span class="sxs-lookup"><span data-stu-id="3163a-137">In this section you'll use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="3163a-138">Ajouter le package d’outils Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="3163a-138">Add the Entity Framework Core Tools package.</span></span> <span data-ttu-id="3163a-139">Ce package est nécessaire pour ajouter des migrations et mettre à jour la base de données</span><span class="sxs-lookup"><span data-stu-id="3163a-139">This package is required to add migrations and update the database.</span></span>
* <span data-ttu-id="3163a-140">Ajouter une migration initiale</span><span class="sxs-lookup"><span data-stu-id="3163a-140">Add an initial migration.</span></span>
* <span data-ttu-id="3163a-141">Mettez à jour la base de données avec la migration initiale.</span><span class="sxs-lookup"><span data-stu-id="3163a-141">Update the database with the initial migration.</span></span>

<span data-ttu-id="3163a-142">Dans le menu **Outils**, sélectionnez **Gestionnaire de package NuGet > Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="3163a-142">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>

<!-- following image shared with uid: tutorials/razor-pages/model -->
  ![Menu Console du Gestionnaire de package](adding-model/_static/pmc.png)

<span data-ttu-id="3163a-144">Dans la console du Gestionnaire de package, entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3163a-144">In the PMC, enter the following commands:</span></span>

``` PMC
Install-Package Microsoft.EntityFrameworkCore.Tools
Add-Migration Initial
Update-Database
```

<span data-ttu-id="3163a-145">**Remarque :** Si vous recevez une erreur avec la commande `Install-Package`, ouvrez le Gestionnaire de Package NuGet et recherchez le package `Microsoft.EntityFrameworkCore.Tools`.</span><span class="sxs-lookup"><span data-stu-id="3163a-145">**Note:** If you receive an error with the `Install-Package` command, open NuGet Package Manager and search for the `Microsoft.EntityFrameworkCore.Tools` package.</span></span> <span data-ttu-id="3163a-146">Ceci vous permet d’installer le package ou de vérifier s’il est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="3163a-146">This allows you to install the package or check if it is already installed.</span></span> <span data-ttu-id="3163a-147">Vous pouvez aussi appliquer [l’approche CLI](#cli) si vous rencontrez des problèmes avec la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="3163a-147">Alternatively, see the [CLI approach](#cli) if you have problems with the PMC.</span></span>

<span data-ttu-id="3163a-148">La commande `Add-Migration` crée le code nécessaire à la création du schéma de base de données initial.</span><span class="sxs-lookup"><span data-stu-id="3163a-148">The `Add-Migration` command creates code to create the initial database schema.</span></span> <span data-ttu-id="3163a-149">Le schéma est basé sur le modèle spécifié dans le fichier `DbContext` (dans *Data/MvcMovieContext.cs*).</span><span class="sxs-lookup"><span data-stu-id="3163a-149">The schema is based on the model specified in the `DbContext`(In the *Data/MvcMovieContext.cs* file).</span></span> <span data-ttu-id="3163a-150">L’argument `Initial` est utilisé pour nommer les migrations.</span><span class="sxs-lookup"><span data-stu-id="3163a-150">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="3163a-151">Vous pouvez utiliser n’importe quel nom, mais par convention, choisissez un nom qui décrit la migration.</span><span class="sxs-lookup"><span data-stu-id="3163a-151">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="3163a-152">Pour plus d’informations, consultez [Présentation des migrations](xref:data/ef-mvc/migrations#introduction-to-migrations).</span><span class="sxs-lookup"><span data-stu-id="3163a-152">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="3163a-153">La commande `Update-Database` exécute la méthode `Up` dans le fichier *Migrations/\<date et heure>_Initial.cs*, ce qui entraîne la création de la base de données.</span><span class="sxs-lookup"><span data-stu-id="3163a-153">The `Update-Database` command runs the `Up` method in the *Migrations/\<time-stamp>_Initial.cs* file, which creates the database.</span></span>

<a name="cli"></a> <span data-ttu-id="3163a-154">Vous pouvez effectuer les étapes qui précèdent à l’aide de l’interface de ligne de commande (CLI) plutôt que la console du Gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="3163a-154">You can perform the preceeding steps using the command-line interface (CLI) rather than the PMC:</span></span>

* <span data-ttu-id="3163a-155">Ajoutez les [outils EF Core](xref:data/ef-mvc/migrations#entity-framework-core-nuget-packages-for-migrations) au fichier *.csproj*.</span><span class="sxs-lookup"><span data-stu-id="3163a-155">Add [EF Core tooling](xref:data/ef-mvc/migrations#entity-framework-core-nuget-packages-for-migrations) to the *.csproj* file.</span></span>
* <span data-ttu-id="3163a-156">Exécutez les commandes suivantes à partir de la console (dans le répertoire du projet) :</span><span class="sxs-lookup"><span data-stu-id="3163a-156">Run the following commands from the console (in the project directory):</span></span>

  ```console
  dotnet ef migrations add Initial
  dotnet ef database update
  ```     
  

[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model3.md)]

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=ConfigureServices&highlight=6-7)]

[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model4.md)]

![Menu contextuel d’IntelliSense sur un élément de modèle qui répertorie les propriétés disponibles pour ID, Price, Release Date et Title.](adding-model/_static/ints.png)

## <a name="additional-resources"></a><span data-ttu-id="3163a-158">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3163a-158">Additional resources</span></span>

* [<span data-ttu-id="3163a-159">Tag Helpers</span><span class="sxs-lookup"><span data-stu-id="3163a-159">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="3163a-160">Globalisation et localisation</span><span class="sxs-lookup"><span data-stu-id="3163a-160">Globalization and localization</span></span>](xref:fundamentals/localization)

>[!div class="step-by-step"]
<span data-ttu-id="3163a-161">[Précédent : Ajout d’une vue](adding-view.md)
[Suivant : Utilisation de SQL](working-with-sql.md)</span><span class="sxs-lookup"><span data-stu-id="3163a-161">[Previous Adding a View](adding-view.md)
[Next Working with SQL](working-with-sql.md)</span></span>  