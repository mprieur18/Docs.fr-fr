---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: "Didacticiel : Mise en route avec SignalR 1.x et MVC 4 | Documents Microsoft"
author: pfletcher
description: "Utilisez ASP.NET SignalR et ASP.NET MVC 4 pour créer une application de conversation en temps réel."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/29/2013
ms.topic: article
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: e678c85520613fea2a8d00de60aca04d895d6307
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="4b8bf-103">Didacticiel : Mise en route avec SignalR 1.x et MVC 4</span><span class="sxs-lookup"><span data-stu-id="4b8bf-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>
====================
<span data-ttu-id="4b8bf-104">par [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="4b8bf-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

> <span data-ttu-id="4b8bf-105">Ce didacticiel montre comment utiliser ASP.NET SignalR pour créer une application de conversation en temps réel.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="4b8bf-106">Vous ajoutez SignalR à une application MVC 4 et créer une vue de conversation pour envoyer et afficher les messages.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>


## <a name="overview"></a><span data-ttu-id="4b8bf-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4b8bf-107">Overview</span></span>

<span data-ttu-id="4b8bf-108">Ce didacticiel vous présente au développement d’applications web en temps réel avec ASP.NET SignalR et ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="4b8bf-109">Ce didacticiel utilise le même code d’application de conversation que la [SignalR prise en main de didacticiel](tutorial-getting-started-with-signalr.md), mais vous montre comment ajouter à une application MVC 4 basée sur le modèle d’Internet.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="4b8bf-110">Dans cette rubrique, vous allez apprendre les tâches de développement SignalR suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b8bf-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="4b8bf-111">Ajout de la bibliothèque de SignalR pour une application MVC 4.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="4b8bf-112">Création d’une classe de concentrateur pour transmettre le contenu aux clients.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="4b8bf-113">À l’aide de la bibliothèque jQuery SignalR dans une page web pour envoyer des messages et d’afficher les mises à jour à partir du concentrateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="4b8bf-114">La capture d’écran suivante montre l’application de conversation terminée en cours d’exécution dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![Instances de conversation](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="4b8bf-116">Sections :</span><span class="sxs-lookup"><span data-stu-id="4b8bf-116">Sections:</span></span>

- [<span data-ttu-id="4b8bf-117">Le projet</span><span class="sxs-lookup"><span data-stu-id="4b8bf-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="4b8bf-118">Exécuter l’exemple</span><span class="sxs-lookup"><span data-stu-id="4b8bf-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="4b8bf-119">Examinez le Code</span><span class="sxs-lookup"><span data-stu-id="4b8bf-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="4b8bf-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b8bf-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="4b8bf-121">Le projet</span><span class="sxs-lookup"><span data-stu-id="4b8bf-121">Set up the Project</span></span>

<span data-ttu-id="4b8bf-122">Conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="4b8bf-122">Prerequisites:</span></span>

- <span data-ttu-id="4b8bf-123">Visual Studio 2010 SP1, Visual Studio 2012 ou Visual Studio 2012 Express.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="4b8bf-124">Si vous n’avez pas Visual Studio, consultez [téléchargements ASP.NET](https://www.asp.net/downloads) pour obtenir le Visual Studio 2012 Express outil de développement gratuit.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="4b8bf-125">Pour Visual Studio 2010, installez [ASP.NET MVC 4](https://www.microsoft.com/en-us/download/details.aspx?id=30683).</span><span class="sxs-lookup"><span data-stu-id="4b8bf-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/en-us/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="4b8bf-126">Cette section montre comment créer une application ASP.NET MVC 4, ajoutez la bibliothèque SignalR et créer l’application de la conversation.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="4b8bf-127">Créer une application ASP.NET MVC 4 dans Visual Studio, nommez-le SignalRChat et cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4b8bf-128">Dans Visual Studio 2010, sélectionnez **.NET Framework 4** dans la liste déroulante version Framework.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="4b8bf-129">SignalR code s’exécute sur les versions du .NET Framework 4 et 4.5.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![Créer web mvc](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
    2. <span data-ttu-id="4b8bf-131">Sélectionnez le modèle d’Application Internet, décochez l’option de **créer un projet de test unitaire**, puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

        ![Créer un site internet de mvc](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
    3. <span data-ttu-id="4b8bf-133">Ouvrez le **outils | Gestionnaire de Package de bibliothèque | Console du Gestionnaire de package** et exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-133">Open the **Tools | Library Package Manager | Package Manager Console** and run the following command.</span></span> <span data-ttu-id="4b8bf-134">Cette étape ajoute au projet un ensemble de fichiers de script et les références d’assembly que vous activez la fonctionnalité de SignalR.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

        `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
    4. <span data-ttu-id="4b8bf-135">Dans **l’Explorateur de solutions** développez le dossier Scripts.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="4b8bf-136">Notez que les bibliothèques de scripts pour SignalR ont été ajoutés au projet.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-136">Note that script libraries for SignalR have been added to the project.</span></span>

        ![Références de bibliothèque](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
    5. <span data-ttu-id="4b8bf-138">Dans **l’Explorateur de solutions**, cliquez sur le projet, sélectionnez **ajouter | Nouveau dossier**, et ajouter un nouveau dossier nommé **concentrateurs**.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
    6. <span data-ttu-id="4b8bf-139">Cliquez sur le **concentrateurs** dossier, cliquez sur **ajouter | Classe**et créer une nouvelle classe c# nommée **ChatHub.cs**.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="4b8bf-140">Vous allez utiliser cette classe comme un concentrateur SignalR serveur qui envoie des messages à tous les clients.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="4b8bf-141">Si vous utilisez Visual Studio 2012 et que vous avez installé le [mise à jour ASP.NET et Web Tools 2012.2](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), vous pouvez utiliser le nouveau modèle d’élément SignalR pour créer la classe de concentrateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="4b8bf-142">Pour ce faire, cliquez sur le **concentrateurs** dossier, cliquez sur **ajouter | Un nouvel élément**, sélectionnez **classe de concentrateur SignalR (v1)**et le nom de la classe **ChatHub.cs**.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>


1. <span data-ttu-id="4b8bf-143">Remplacez le code dans le **ChatHub** classe par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="4b8bf-144">Ouvrez le **Global.asax** de fichier pour le projet et ajoutez un appel à la méthode `RouteTable.Routes.MapHubs();` comme première ligne de code dans le `Application_Start` (méthode).</span><span class="sxs-lookup"><span data-stu-id="4b8bf-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="4b8bf-145">Ce code enregistre l’itinéraire par défaut pour les concentrateurs SignalR et doit être appelé avant d’inscrire tous les autres itinéraires.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="4b8bf-146">Terminé `Application_Start` méthode ressemble à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="4b8bf-147">Modifier la `HomeController` classe trouvé dans **Controllers/HomeController.cs** et ajoutez la méthode suivante à la classe.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="4b8bf-148">Cette méthode retourne le **Chat** vue que vous allez créer dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="4b8bf-149">Avec le bouton droit dans le `Chat` méthode que vous venez de créer et cliquez sur **ajouter une vue** pour créer un nouveau fichier de vue.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="4b8bf-150">Dans le **ajouter une vue** boîte de dialogue, vérifiez que la case à cocher est sélectionnée pour **utiliser une disposition ou la page maître** (désactivez les autres cases à cocher), puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![Ajouter une vue](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="4b8bf-152">Modifiez le nouveau fichier de vue nommé **Chat.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="4b8bf-153">Après le &lt;h2&gt; de balise, collez le texte suivant &lt;div&gt; section et `@section scripts` bloc de code dans la page.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="4b8bf-154">Ce script permet à la page envoyer des messages de conversation et d’afficher des messages à partir du serveur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="4b8bf-155">Le code complet pour l’affichage de la conversation s’affiche dans le bloc de code suivant.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4b8bf-156">Lorsque vous ajoutez SignalR et autres bibliothèques de script à votre projet Visual Studio, le Gestionnaire de Package peut installer des versions des scripts qui sont plus récents que les versions présentées dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="4b8bf-157">Assurez-vous que les références de script dans votre code correspondent aux versions des bibliothèques de script installés dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="4b8bf-158">**Enregistrer tous les** pour le projet.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="4b8bf-159">Exécuter l’exemple</span><span class="sxs-lookup"><span data-stu-id="4b8bf-159">Run the Sample</span></span>

1. <span data-ttu-id="4b8bf-160">Appuyez sur F5 pour exécuter le projet en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="4b8bf-161">Dans la ligne d’adresse du navigateur, ajoutez **/home/chat** à l’URL de la page par défaut pour le projet.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="4b8bf-162">Chargement de la page de la conversation dans une instance du navigateur et les invite à entrer un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![Entrer un nom d'utilisateur](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="4b8bf-164">Entrez un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-164">Enter a user name.</span></span>
4. <span data-ttu-id="4b8bf-165">Copiez l’URL de la ligne d’adresse du navigateur et l’utiliser pour ouvrir les deux instances du navigateur plus.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="4b8bf-166">Dans chaque instance du navigateur, entrez un nom d’utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="4b8bf-167">Dans chaque instance du navigateur, ajoutez un commentaire, puis cliquez sur **envoyer**.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="4b8bf-168">Les commentaires doivent s’afficher dans toutes les instances du navigateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4b8bf-169">Cette application de conversation simple ne conserve pas le contexte de la discussion sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="4b8bf-170">Le concentrateur diffuse des commentaires à tous les utilisateurs actuels.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="4b8bf-171">Les utilisateurs qui participer à la conversation ultérieurement voient des messages ajoutés à partir du moment qu'ils se connectent.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="4b8bf-172">La capture d’écran suivante montre l’application de conversation en cours d’exécution dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![Navigateurs de conversation](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="4b8bf-174">Dans **l’Explorateur de solutions**, inspecter la **Documents de Script** nœud pour l’application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="4b8bf-175">Ce nœud est visible en mode débogage si vous utilisez Internet Explorer comme navigateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="4b8bf-176">Il existe un fichier de script nommé **concentrateurs** que la bibliothèque SignalR génère dynamiquement lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="4b8bf-177">Ce fichier gère la communication entre le script jQuery et le code côté serveur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="4b8bf-178">Si vous utilisez un navigateur autre qu’Internet Explorer, vous pouvez également accéder à la dynamique **concentrateurs** fichier en parcourant directement, par exemple http://mywebsite/signalr/hubs.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![Script de concentrateur généré](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="4b8bf-180">Examinez le Code</span><span class="sxs-lookup"><span data-stu-id="4b8bf-180">Examine the Code</span></span>

<span data-ttu-id="4b8bf-181">L’application de la conversation SignalR illustre deux tâches de développement SignalR base : création d’un hub en tant que l’objet principal de coordination sur le serveur et à l’aide de la bibliothèque jQuery SignalR pour envoyer et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="4b8bf-182">Concentrateurs SignalR</span><span class="sxs-lookup"><span data-stu-id="4b8bf-182">SignalR Hubs</span></span>

<span data-ttu-id="4b8bf-183">Dans l’exemple de code la **ChatHub** classe dérive de la **Microsoft.AspNet.SignalR.Hub** classe.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="4b8bf-184">Dérivation à partir de la **Hub** classe est une méthode utile pour générer une application SignalR.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="4b8bf-185">Vous pouvez créer des méthodes publiques sur votre classe de concentrateur et puis accéder à ces méthodes en les appelant à partir de scripts jQuery dans une page web.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="4b8bf-186">Dans le code de la conversation, les clients appellent le **ChatHub.Send** méthode pour envoyer un message.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="4b8bf-187">Le concentrateur à son tour envoie le message à tous les clients en appelant **Clients.All.addNewMessageToPage**.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="4b8bf-188">Le **envoyer** méthode illustre plusieurs concepts de hub :</span><span class="sxs-lookup"><span data-stu-id="4b8bf-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="4b8bf-189">Déclarer des méthodes publiques sur un concentrateur, afin que les clients peuvent appeler les.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="4b8bf-190">Utilisez le **Microsoft.AspNet.SignalR.Hub.Clients** propriété pour accéder à tous les clients connectés à ce concentrateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="4b8bf-191">Appeler une fonction de jQuery sur le client (telles que le `addNewMessageToPage` (fonction)) pour mettre à jour des clients.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="4b8bf-192">SignalR et jQuery</span><span class="sxs-lookup"><span data-stu-id="4b8bf-192">SignalR and jQuery</span></span>

<span data-ttu-id="4b8bf-193">Le **Chat.cshtml** afficher le fichier dans l’exemple de code montre comment utiliser la bibliothèque jQuery SignalR pour communiquer avec un concentrateur SignalR.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="4b8bf-194">Les tâches essentielles dans le code créez une référence pour le proxy généré automatiquement pour le concentrateur, déclarer une fonction que le serveur peut appeler pour envoyer aux clients et le démarrage d’une connexion pour envoyer des messages au concentrateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="4b8bf-195">Le code suivant déclare un proxy pour un concentrateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="4b8bf-196">Dans jQuery la référence à la classe de serveur et de ses membres est en casse mixte.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="4b8bf-197">L’exemple de code fait référence à c# **ChatHub** jQuery en tant que classe **chatHub**.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="4b8bf-198">Si vous souhaitez faire référence à la `ChatHub` classe dans jQuery avec Pascal conventionnel casse comme vous le feriez dans c#, modifier le fichier de classe ChatHub.cs.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="4b8bf-199">Ajouter un `using` instruction pour faire référence à la `Microsoft.AspNet.SignalR.Hubs` espace de noms.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="4b8bf-200">Ajoutez ensuite la `HubName` attribut le `ChatHub` de classe, par exemple `[HubName("ChatHub")]`.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="4b8bf-201">Enfin, mettre à jour votre référence de jQuery à la `ChatHub` classe.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>


<span data-ttu-id="4b8bf-202">Le code suivant montre comment créer une fonction de rappel dans le script.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="4b8bf-203">La classe de concentrateur sur le serveur appelle cette fonction pour transmettre les mises à jour à chaque client.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="4b8bf-204">L’appel facultatif à la `htmlEncode` affiche la fonction HTML permet de coder le contenu du message avant de les afficher dans la page, comme un moyen d’empêcher l’injection de script.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="4b8bf-205">Le code suivant montre comment ouvrir une connexion avec le concentrateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="4b8bf-206">Le code démarre la connexion et qu’il passe ensuite une fonction pour gérer l’événement de clic sur le **envoyer** bouton dans la page de la conversation.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="4b8bf-207">Cette approche garantit que la connexion est établie avant l’exécution du Gestionnaire d’événements.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-207">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="4b8bf-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b8bf-208">Next Steps</span></span>

<span data-ttu-id="4b8bf-209">Vous avez appris que SignalR est une infrastructure pour la génération d’applications web en temps réel.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="4b8bf-210">Vous avez également appris à plusieurs tâches de développement SignalR : comment ajouter SignalR pour une application ASP.NET, la création d’une classe de concentrateur et comment envoyer et recevoir des messages à partir du concentrateur.</span><span class="sxs-lookup"><span data-stu-id="4b8bf-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="4b8bf-211">Pour en savoir plus avancées concepts de développements SignalR, visitez les sites suivants pour le code source de SignalR et ressources :</span><span class="sxs-lookup"><span data-stu-id="4b8bf-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="4b8bf-212">Projet SignalR</span><span class="sxs-lookup"><span data-stu-id="4b8bf-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="4b8bf-213">SignalR Github et exemples</span><span class="sxs-lookup"><span data-stu-id="4b8bf-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="4b8bf-214">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="4b8bf-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)