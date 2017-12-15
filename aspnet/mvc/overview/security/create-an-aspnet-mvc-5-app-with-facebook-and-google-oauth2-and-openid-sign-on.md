---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: "Créer MVC 5 application avec Facebook, Twitter, LinkedIn et Google OAuth2 Sign-on (c#) | Documents Microsoft"
author: Rick-Anderson
description: "Ce didacticiel vous montre comment générer une application web ASP.NET MVC 5 qui permet aux utilisateurs de se connecter en utilisant OAuth 2.0 avec les informations d’identification à partir d’un authenti externe..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/03/2015
ms.topic: article
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: aaa061e61b9bab5b33083851624f0487b2cf6473
ms.sourcegitcommit: ccf08615ad59bc6f654560de33b93396113a2eb0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2017
---
<a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="5d241-103">Créer une application ASP.NET MVC 5 avec Facebook, Twitter, LinkedIn et Google OAuth2 Sign-on (c#)</span><span class="sxs-lookup"><span data-stu-id="5d241-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>
====================
<span data-ttu-id="5d241-104">Par [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="5d241-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="5d241-105">Ce didacticiel vous montre comment créer une application web ASP.NET MVC 5 qui permet aux utilisateurs de se connecter à l’aide de [OAuth 2.0](http://oauth.net/2/) avec les informations d’identification d’un fournisseur d’authentification externes, tels que Facebook, Twitter, LinkedIn, Microsoft ou Google.</span><span class="sxs-lookup"><span data-stu-id="5d241-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="5d241-106">Par souci de simplicité, ce didacticiel se concentre sur l’utilisation des informations d’identification à partir de Facebook et Google.</span><span class="sxs-lookup"><span data-stu-id="5d241-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="5d241-107">L’activation de ces informations d’identification dans les sites web fournit des avantages significatifs, car des millions d’utilisateurs disposent déjà de comptes avec ces fournisseurs externes.</span><span class="sxs-lookup"><span data-stu-id="5d241-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="5d241-108">Ces utilisateurs peuvent être plus de chances de souscrire à votre site, si elles n’ont pas à créer et à mémoriser un nouvel ensemble d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="5d241-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="5d241-109">Voir aussi [application ASP.NET MVC 5 avec SMS et par courrier électronique d’authentification à deux facteurs](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5d241-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="5d241-110">Le didacticiel montre également comment ajouter des données de profil pour l’utilisateur et comment utiliser l’API d’appartenance pour ajouter des rôles.</span><span class="sxs-lookup"><span data-stu-id="5d241-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="5d241-111">Ce didacticiel a été écrit par [Rick Anderson](https://blogs.msdn.com/rickAndy) (suivez me sur Twitter : [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="5d241-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="5d241-112">Commencer</span><span class="sxs-lookup"><span data-stu-id="5d241-112">Getting Started</span></span>

<span data-ttu-id="5d241-113">Commencez par installer et exécuter [Visual Studio Express 2013 pour le Web](https://go.microsoft.com/fwlink/?LinkId=299058) ou [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="5d241-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="5d241-114">Installation de Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5d241-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="5d241-115">Pour Dropbox, GitHub, Linkedin, Instagram, mémoire tampon, force de vente, le flux, pile Exchange, Tripit, twitch, Twitter, Yahoo et bien plus encore l’aide, consultez ce [un guide qui](http://www.oauthforaspnet.com/).</span><span class="sxs-lookup"><span data-stu-id="5d241-115">For help with Dropbox, GitHub, Linkedin, Instagram, buffer, salesforce, STEAM, Stack Exchange, Tripit, twitch, Twitter, Yahoo and more, see this [one stop guide](http://www.oauthforaspnet.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="5d241-116">Vous devez installer Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) ou une version ultérieure pour utiliser Google OAuth 2 et déboguer localement sans avertissements de SSL.</span><span class="sxs-lookup"><span data-stu-id="5d241-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>


<span data-ttu-id="5d241-117">Cliquez sur **nouveau projet** à partir de la **Démarrer** page, ou vous pouvez utiliser le menu et sélectionnez **fichier**, puis **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="5d241-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  
 

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="5d241-118">Créer votre première Application</span><span class="sxs-lookup"><span data-stu-id="5d241-118">Creating Your First Application</span></span>

<span data-ttu-id="5d241-119">Cliquez sur **nouveau projet**, puis sélectionnez **Visual C#** sur la gauche, puis **Web** , puis sélectionnez **Application Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="5d241-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="5d241-120">Nommez votre projet « MvcAuth », puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d241-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="5d241-121">Dans le **nouveau projet ASP.NET** boîte de dialogue, cliquez sur **MVC**.</span><span class="sxs-lookup"><span data-stu-id="5d241-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="5d241-122">Si l’authentification n’est pas **comptes d’utilisateur individuels**, cliquez sur le **modifier l’authentification** sélectionnez **comptes d’utilisateur individuels**.</span><span class="sxs-lookup"><span data-stu-id="5d241-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="5d241-123">En vérifiant **hôte dans le cloud**, l’application sera très facile à héberger dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5d241-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="5d241-124">Si vous avez sélectionné **hôte dans le cloud**, terminez la boîte de dialogue Configurer.</span><span class="sxs-lookup"><span data-stu-id="5d241-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)


### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="5d241-125">Utilisez NuGet pour mettre à jour vers la dernière intergiciel (middleware) OWIN</span><span class="sxs-lookup"><span data-stu-id="5d241-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="5d241-126">Utilisez le Gestionnaire de package NuGet pour mettre à jour le [intergiciel (middleware) OWIN](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span><span class="sxs-lookup"><span data-stu-id="5d241-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="5d241-127">Sélectionnez **mises à jour** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="5d241-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="5d241-128">Vous pouvez cliquer sur le **tout mettre à jour** bouton ou vous pouvez rechercher uniquement les packages OWIN (illustrés dans l’image suivante) :</span><span class="sxs-lookup"><span data-stu-id="5d241-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="5d241-129">Dans l’image ci-dessous, seuls les packages OWIN sont affichés :</span><span class="sxs-lookup"><span data-stu-id="5d241-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="5d241-130">À partir de Package Manager Console (PMC), vous pouvez entrer le `Update-Package` commande qui met à jour tous les packages.</span><span class="sxs-lookup"><span data-stu-id="5d241-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="5d241-131">Appuyez sur **F5** ou **Ctrl + F5** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="5d241-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="5d241-132">Dans l’image ci-dessous, le numéro de port est 1234.</span><span class="sxs-lookup"><span data-stu-id="5d241-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="5d241-133">Lorsque vous exécutez l’application, vous verrez un numéro de port différent.</span><span class="sxs-lookup"><span data-stu-id="5d241-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="5d241-134">Selon la taille de la fenêtre du navigateur, vous devrez peut-être cliquer sur l’icône de navigation pour afficher les **accueil**, **sur**, **Contact**, **inscrire**et **connecter** des liens.</span><span class="sxs-lookup"><span data-stu-id="5d241-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="5d241-135">Configuration de SSL dans le projet</span><span class="sxs-lookup"><span data-stu-id="5d241-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="5d241-136">Pour vous connecter à des fournisseurs d’authentification tels que Google et Facebook, vous devez configurer IIS Express pour utiliser SSL.</span><span class="sxs-lookup"><span data-stu-id="5d241-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="5d241-137">Il est important de garder à l’aide de SSL après l’ouverture de session et pas effacer HTTP, le cookie de connexion est uniquement en tant que secret en tant que votre nom d’utilisateur et un mot de passe et sans l’utilisation de SSL, vous l’envoyez en texte clair sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="5d241-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="5d241-138">En outre, vous avez déjà pris le temps d’effectuer le protocole de transfert et sécurisez le canal (qui est le bloc de ce qui rend HTTPS plus lent que HTTP) avant l’exécution, le pipeline MVC donc rediriger vers HTTP une fois que vous êtes connecté ne sont pas rendre la requête actuelle ou futur demandes beaucoup plus rapides.</span><span class="sxs-lookup"><span data-stu-id="5d241-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="5d241-139">Dans **l’Explorateur de solutions**, cliquez sur le **MvcAuth** projet.</span><span class="sxs-lookup"><span data-stu-id="5d241-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="5d241-140">Appuyez sur la touche F4 pour afficher les propriétés du projet.</span><span class="sxs-lookup"><span data-stu-id="5d241-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="5d241-141">Également, dans le **vue** menu que vous pouvez sélectionner **fenêtre Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="5d241-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="5d241-142">Modification **SSL activé** sur True.</span><span class="sxs-lookup"><span data-stu-id="5d241-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="5d241-143">Copiez l’URL SSL (qui sera `https://localhost:44300/` , sauf si vous avez créé d’autres projets SSL).</span><span class="sxs-lookup"><span data-stu-id="5d241-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="5d241-144">Dans **l’Explorateur de solutions**, bouton droit sur le **MvcAuth** de projet et sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="5d241-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="5d241-145">Sélectionnez le **Web** onglet et collez l’URL SSL dans le **Url Project** boîte.</span><span class="sxs-lookup"><span data-stu-id="5d241-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="5d241-146">Enregistrez le fichier (CTRL + S).</span><span class="sxs-lookup"><span data-stu-id="5d241-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="5d241-147">Vous aurez besoin de cette URL à configurer des applications de l’authentification Facebook et Google.</span><span class="sxs-lookup"><span data-stu-id="5d241-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="5d241-148">Ajouter le [RequireHttps](https://msdn.microsoft.com/en-us/library/system.web.mvc.requirehttpsattribute.aspx) attribut le `Home` contrôleur pour toutes les demandes doit utiliser HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5d241-148">Add the [RequireHttps](https://msdn.microsoft.com/en-us/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="5d241-149">Une approche la plus sûre consiste à ajouter la [RequireHttps](https://msdn.microsoft.com/en-us/library/system.web.mvc.requirehttpsattribute.aspx) filtre à l’application.</span><span class="sxs-lookup"><span data-stu-id="5d241-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/en-us/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="5d241-150">Consultez la section &quot;protéger l’Application avec SSL et de l’attribut autoriser&quot; dans mon tutoral [créer une application ASP.NET MVC avec l’authentification et de la base de données SQL et le déployer vers Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="5d241-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutoral [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="5d241-151">Vous trouverez ci-dessous une partie du contrôleur Home.</span><span class="sxs-lookup"><span data-stu-id="5d241-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="5d241-152">Appuyez sur CTRL+F5 pour exécuter l'application.</span><span class="sxs-lookup"><span data-stu-id="5d241-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="5d241-153">Si vous avez installé le certificat dans le passé, vous pouvez ignorer le reste de cette section et atteindre [création d’une application de Google OAuth 2 et la connexion de l’application au projet](#goog), dans le cas contraire, suivez les instructions pour approbation auto-signé certificat IIS Express a généré.</span><span class="sxs-lookup"><span data-stu-id="5d241-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="5d241-154">Lecture la **avertissement de sécurité** boîte de dialogue, puis cliquez sur **Oui** si vous souhaitez installer le certificat de localhost.</span><span class="sxs-lookup"><span data-stu-id="5d241-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="5d241-155">Internet Explorer affiche la *accueil* page et aucun avertissement de SSL.</span><span class="sxs-lookup"><span data-stu-id="5d241-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="5d241-156">Google Chrome également accepte le certificat et affiche le contenu HTTPS sans avertissement.</span><span class="sxs-lookup"><span data-stu-id="5d241-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="5d241-157">Firefox utilise son propre magasin de certificats, il affiche un avertissement.</span><span class="sxs-lookup"><span data-stu-id="5d241-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="5d241-158">Pour notre application vous pouvez cliquer en toute sécurité sur **conscient des risques de**.</span><span class="sxs-lookup"><span data-stu-id="5d241-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="5d241-159">Création d’une application de Google OAuth 2 et la connexion de l’application au projet</span><span class="sxs-lookup"><span data-stu-id="5d241-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

1. <span data-ttu-id="5d241-160">Accédez à la [Console des développeurs Google](https://console.developers.google.com/).</span><span class="sxs-lookup"><span data-stu-id="5d241-160">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
1. <span data-ttu-id="5d241-161">Si vous n’avez pas créé un projet, sélectionnez **informations d’identification** dans l’onglet gauche, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="5d241-161">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
1. <span data-ttu-id="5d241-162">Dans l’onglet gauche, cliquez sur **informations d’identification**.</span><span class="sxs-lookup"><span data-stu-id="5d241-162">In the left tab, click **Credentials**.</span></span>
1. <span data-ttu-id="5d241-163">Cliquez sur **créer les informations d’identification** puis **ID de client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="5d241-163">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="5d241-164">Dans le **créer un identifiant Client** boîte de dialogue, conservez la valeur par défaut **application Web** pour le type d’application.</span><span class="sxs-lookup"><span data-stu-id="5d241-164">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="5d241-165">Définir le **autorisé de JavaScript** origine à l’URL SSL utilisée ci-dessus (`https://localhost:44300/` , sauf si vous avez créé d’autres projets SSL)</span><span class="sxs-lookup"><span data-stu-id="5d241-165">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="5d241-166">Définir le **l’URI de redirection autorisés** à :</span><span class="sxs-lookup"><span data-stu-id="5d241-166">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="5d241-167">Cliquez sur l’élément de menu écran consentement OAuth, puis nommez votre messagerie adresse et le produit.</span><span class="sxs-lookup"><span data-stu-id="5d241-167">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="5d241-168">Lorsque vous avez terminé la forme, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5d241-168">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="5d241-169">Cliquez sur l’élément de menu de bibliothèque, recherchez **Google + API**, cliquez dessus, puis appuyez sur Activer.</span><span class="sxs-lookup"><span data-stu-id="5d241-169">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
 <span data-ttu-id="5d241-170">L’image ci-dessous montre les API activées.</span><span class="sxs-lookup"><span data-stu-id="5d241-170">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="5d241-171">À partir du Gestionnaire d’API Google API, visitez le **informations d’identification** tab pour obtenir le **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="5d241-171">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="5d241-172">Téléchargement pour enregistrer un fichier JSON comportant des secrets de l’application.</span><span class="sxs-lookup"><span data-stu-id="5d241-172">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="5d241-173">Copiez et collez le **ClientId** et **ClientSecret** dans le `UseGoogleAuthentication` méthode trouvée dans le *Startup.Auth.cs* de fichiers dans le *App_Start* dossier.</span><span class="sxs-lookup"><span data-stu-id="5d241-173">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="5d241-174">Le **ClientId** et **ClientSecret** valeurs indiquées ci-dessous sont des exemples et ne fonctionnent pas.</span><span class="sxs-lookup"><span data-stu-id="5d241-174">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="5d241-175">Sécurité - magasin jamais des données sensibles dans votre code source.</span><span class="sxs-lookup"><span data-stu-id="5d241-175">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="5d241-176">Le compte et les informations d’identification sont ajoutées au code ci-dessus pour simplifier l’exemple.</span><span class="sxs-lookup"><span data-stu-id="5d241-176">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="5d241-177">Consultez [meilleures pratiques pour le déploiement des mots de passe et autres données sensibles sur ASP.NET et Service d’applications Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5d241-177">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="5d241-178">Appuyez sur **CTRL + F5** pour générer et exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="5d241-178">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="5d241-179">Cliquez sur le **connecter** lien.</span><span class="sxs-lookup"><span data-stu-id="5d241-179">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="5d241-180">Sous **utiliser un autre service pour vous connecter**, cliquez sur **Google**.</span><span class="sxs-lookup"><span data-stu-id="5d241-180">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="5d241-181">Si vous omettez une des étapes ci-dessus, vous obtiendrez une erreur HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="5d241-181">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="5d241-182">Revérifier les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="5d241-182">Recheck your steps above.</span></span> <span data-ttu-id="5d241-183">Si vous omettez un paramètre requis (par exemple **nom de produit**), ajouter manquants élément et d’enregistrer, peut prendre quelques minutes pour l’authentification à utiliser.</span><span class="sxs-lookup"><span data-stu-id="5d241-183">If you miss a required setting (for example **product name**), add the missing item and save, it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="5d241-184">Vous allez être redirigé vers le site de google où vous devrez entrer vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="5d241-184">You will be redirected to the google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="5d241-185">Après avoir entré vos informations d’identification, vous devez accorder des autorisations à l’application web que vous venez de créer :</span><span class="sxs-lookup"><span data-stu-id="5d241-185">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="5d241-186">Cliquez sur **accepter**.</span><span class="sxs-lookup"><span data-stu-id="5d241-186">Click **Accept**.</span></span> <span data-ttu-id="5d241-187">Vous allez maintenant être redirigé vers le **inscrire** page de l’application MvcAuth où vous pouvez inscrire votre compte Google.</span><span class="sxs-lookup"><span data-stu-id="5d241-187">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="5d241-188">Vous avez la possibilité de modifier le nom de l’inscription de messagerie local utilisé pour votre compte Gmail, mais vous souhaitez généralement conserver l’alias de messagerie électronique par défaut (autrement dit, celui vous avez utilisé pour l’authentification).</span><span class="sxs-lookup"><span data-stu-id="5d241-188">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="5d241-189">Cliquez sur **Register**.</span><span class="sxs-lookup"><span data-stu-id="5d241-189">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="5d241-190">Création de l’application de Facebook et la connexion de l’application au projet</span><span class="sxs-lookup"><span data-stu-id="5d241-190">Creating the app in Facebook and connecting the app to the project</span></span>

<span data-ttu-id="5d241-191">Pour l’authentification Facebook OAuth2, vous devez copier certains paramètres dans votre projet à partir d’une application que vous créez dans Facebook.</span><span class="sxs-lookup"><span data-stu-id="5d241-191">For Facebook OAuth2 authentication, you need to copy to your project some settings from an application that you create in Facebook.</span></span>

1. <span data-ttu-id="5d241-192">Dans votre navigateur, accédez à [https://developers.facebook.com/apps](https://developers.facebook.com/apps) et connectez-vous à entrer vos informations d’identification de Facebook.</span><span class="sxs-lookup"><span data-stu-id="5d241-192">In your browser, navigate to [https://developers.facebook.com/apps](https://developers.facebook.com/apps) and log in by entering your Facebook credentials.</span></span>
2. <span data-ttu-id="5d241-193">Si vous n’êtes pas déjà inscrit en tant qu’un développeur de Facebook, cliquez sur **enregistrer en tant que développeur** et suivez les instructions à inscrire.</span><span class="sxs-lookup"><span data-stu-id="5d241-193">If you aren't already registered as a Facebook developer, click **Register as a Developer** and follow the directions to register.</span></span>
3. <span data-ttu-id="5d241-194">Sur le **applications** , cliquez sur **créer une application**.</span><span class="sxs-lookup"><span data-stu-id="5d241-194">On the **Apps** tab, click **Create New App**.</span></span>

    ![Créer une application](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image22.png)
4. <span data-ttu-id="5d241-196">Entrez un **nom de l’application** et **catégorie**, puis cliquez sur **créer application**.</span><span class="sxs-lookup"><span data-stu-id="5d241-196">Enter an **App Name** and **Category**, then click **Create App**.</span></span>

    <span data-ttu-id="5d241-197">Cela doit être unique dans Facebook.</span><span class="sxs-lookup"><span data-stu-id="5d241-197">This must be unique across Facebook.</span></span> <span data-ttu-id="5d241-198">Le **application Namespace** est la partie de l’URL que votre application utilise pour accéder à l’application Facebook pour l’authentification (par exemple, https://apps.facebook.com/ {application Namespace}).</span><span class="sxs-lookup"><span data-stu-id="5d241-198">The **App Namespace** is the part of the URL that your App will use to access the Facebook application for authentication (for example, https://apps.facebook.com/{App Namespace}).</span></span> <span data-ttu-id="5d241-199">Si vous ne spécifiez pas un **application Namespace**, le **ID d’application** sera utilisé pour l’URL.</span><span class="sxs-lookup"><span data-stu-id="5d241-199">If you don't specify an **App Namespace**, the **App ID** will be used for the URL.</span></span> <span data-ttu-id="5d241-200">Le **ID d’application** est un nombre long généré par le système qui s’affiche dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="5d241-200">The **App ID** is a long system-generated number that you will see in the next step.</span></span>

    ![Créer la boîte de dialogue nouvelle application](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image23.png)
5. <span data-ttu-id="5d241-202">Envoyer la vérification de sécurité standard.</span><span class="sxs-lookup"><span data-stu-id="5d241-202">Submit the standard security check.</span></span>

    ![Vérification de sécurité](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image24.png)
6. <span data-ttu-id="5d241-204">Sélectionnez **paramètres** de la barre de menu de gauche.![ Barre de menus du développeur Facebook](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="5d241-204">Select **Settings** for the left menu bar.![Facebook Developer's menu bar](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image25.png)</span></span>
7. <span data-ttu-id="5d241-205">Sur le **base** section Paramètres de la page Sélectionnez **ajouter une plateforme** pour spécifier que vous ajoutez une application de site Web.</span><span class="sxs-lookup"><span data-stu-id="5d241-205">On the **Basic** settings section of the page select **Add Platform** to specify that you are adding a website application.</span></span> <span data-ttu-id="5d241-206">![Paramètres de base](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="5d241-206">![Basic Settings](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image26.png)</span></span>
8. <span data-ttu-id="5d241-207">Sélectionnez **site Web** parmi les choix de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="5d241-207">Select **Website** from the platform choices.</span></span>  
  
    ![Choix de la plateforme](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image27.png)
9. <span data-ttu-id="5d241-209">Prenez note de votre **ID d’application** et votre **Secret d’application** afin que vous pouvez ajouter à la fois dans votre application MVC plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5d241-209">Make a note of your **App ID** and your **App Secret** so that you can add both into your MVC application later in this tutorial.</span></span> <span data-ttu-id="5d241-210">En outre, ajoutez l’URL du Site (`https://localhost:44300/`) pour tester votre application MVC.</span><span class="sxs-lookup"><span data-stu-id="5d241-210">Also, Add your Site URL (`https://localhost:44300/`) to test your MVC application.</span></span> <span data-ttu-id="5d241-211">En outre, ajoutez un **messagerie du Contact**.</span><span class="sxs-lookup"><span data-stu-id="5d241-211">Also, add a **Contact Email**.</span></span> <span data-ttu-id="5d241-212">Ensuite, sélectionnez **enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="5d241-212">Then, select **Save Changes**.</span></span>   

    ![Page de détails de l’application de base](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image28.png)

    > [!NOTE]
    > <span data-ttu-id="5d241-214">Notez que vous serez uniquement en mesure de s’authentifier à l’aide de l’alias de messagerie que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="5d241-214">Note that you will only be able to authenticate using the email alias you have registered.</span></span> <span data-ttu-id="5d241-215">Autres utilisateurs et les comptes de test ne sera pas en mesure d’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="5d241-215">Other users and test accounts will not be able to register.</span></span> <span data-ttu-id="5d241-216">Vous pouvez accorder des accès aux autres comptes de Facebook à l’application sur Facebook **rôles de développeur** onglet.</span><span class="sxs-lookup"><span data-stu-id="5d241-216">You can grant other Facebook accounts access to the application on the Facebook **Developer Roles** tab.</span></span>
10. <span data-ttu-id="5d241-217">Dans Visual Studio, ouvrez *application\_Start\Startup.Auth.cs*.</span><span class="sxs-lookup"><span data-stu-id="5d241-217">In Visual Studio, open *App\_Start\Startup.Auth.cs*.</span></span>
11. <span data-ttu-id="5d241-218">Copiez et collez le **AppId** et **Secret d’application** dans le `UseFacebookAuthentication` (méthode).</span><span class="sxs-lookup"><span data-stu-id="5d241-218">Copy and paste the **AppId** and **App Secret** into the `UseFacebookAuthentication` method.</span></span> <span data-ttu-id="5d241-219">Le **AppId** et **Secret d’application** valeurs indiquées ci-dessous sont des exemples et ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="5d241-219">The **AppId** and **App Secret** values shown below are samples and will not work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample3.cs?highlight=33-35,38-39)]
12. <span data-ttu-id="5d241-220">Cliquez sur **enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="5d241-220">Click **Save Changes**.</span></span>
13. <span data-ttu-id="5d241-221">Appuyez sur **CTRL + F5** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="5d241-221">Press **CTRL+F5** to run the application.</span></span>


<span data-ttu-id="5d241-222">Sélectionnez **connecter** pour afficher la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="5d241-222">Select **Log in** to display the Login page.</span></span> <span data-ttu-id="5d241-223">Cliquez sur **Facebook** sous **utiliser un autre service pour vous connecter.**</span><span class="sxs-lookup"><span data-stu-id="5d241-223">Click **Facebook** under **Use another service to log in.**</span></span>

<span data-ttu-id="5d241-224">Entrez vos informations d’identification de Facebook.</span><span class="sxs-lookup"><span data-stu-id="5d241-224">Enter your Facebook credentials.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image29.png)

<span data-ttu-id="5d241-225">Vous devrez accorder l’autorisation de l’application pour accéder à votre profil public et la liste d’amis.</span><span class="sxs-lookup"><span data-stu-id="5d241-225">You will be prompted to grant permission for the application to access your public profile and friend list.</span></span>

![Détails de l’application Facebook](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image30.png)

<span data-ttu-id="5d241-227">Vous êtes désormais connecté.</span><span class="sxs-lookup"><span data-stu-id="5d241-227">You are now logged in.</span></span> <span data-ttu-id="5d241-228">Vous pouvez maintenant inscrire ce compte avec l’application.</span><span class="sxs-lookup"><span data-stu-id="5d241-228">You can now register this account with the application.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image31.png)

<span data-ttu-id="5d241-229">Lorsque vous inscrivez, une entrée est ajoutée à la *utilisateurs* table de la base de données d’appartenance.</span><span class="sxs-lookup"><span data-stu-id="5d241-229">When you register, an entry is added to the *Users* table of the membership database.</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="5d241-230">Examiner les données d’appartenance</span><span class="sxs-lookup"><span data-stu-id="5d241-230">Examine the Membership Data</span></span>

<span data-ttu-id="5d241-231">Dans le **vue** menu, cliquez sur **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="5d241-231">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="5d241-232">Développez **DefaultConnection (MvcAuth)**, développez **Tables**, cliquez droit **AspNetUsers** et cliquez sur **afficher les données de Table**.</span><span class="sxs-lookup"><span data-stu-id="5d241-232">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![données de la table aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="5d241-234">Ajout de données de profil à la classe d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="5d241-234">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="5d241-235">Dans cette section vous ajouterez date de naissance et ville d’origine pour les données utilisateur pendant l’inscription, comme indiqué dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="5d241-235">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![reg avec accueil ville et Anniv.](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="5d241-237">Ouvrez le *Models\IdentityModels.cs* de fichiers et d’ajouter des propriétés de zone urbaine accueil et de la date de naissance :</span><span class="sxs-lookup"><span data-stu-id="5d241-237">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="5d241-238">Ouvrez le *Models\AccountViewModels.cs* de fichiers et le jeu de propriétés de zone urbaine de date et d’accueil dans de naissance `ExternalLoginConfirmationViewModel`.</span><span class="sxs-lookup"><span data-stu-id="5d241-238">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="5d241-239">Ouvrez le *Controllers\AccountController.cs* et ajoutez le code pour la ville de date et d’accueil de naissance dans la `ExternalLoginConfirmation` méthode d’action comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="5d241-239">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="5d241-240">Ajouter la date de naissance et ville domestique à le *Views\Account\ExternalLoginConfirmation.cshtml* fichier :</span><span class="sxs-lookup"><span data-stu-id="5d241-240">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="5d241-241">Supprimer la base de données d’appartenance afin de pouvoir à nouveau enregistrer votre compte Facebook avec votre application et vérifiez que vous pouvez ajouter la nouvelle date de naissance et les informations de profil de ville d’origine.</span><span class="sxs-lookup"><span data-stu-id="5d241-241">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="5d241-242">À partir de **l’Explorateur de solutions**, cliquez sur le **afficher tous les fichiers** icône, puis cliquez sur droite *ajouter\_Data\aspnet-MvcAuth -&lt;dateStamp&gt;.mdf* et cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="5d241-242">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="5d241-243">À partir de la **outils** menu, cliquez sur **le Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console** (PMC).</span><span class="sxs-lookup"><span data-stu-id="5d241-243">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="5d241-244">Entrez les commandes suivantes dans le PMC.</span><span class="sxs-lookup"><span data-stu-id="5d241-244">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="5d241-245">Enable-Migrations</span><span class="sxs-lookup"><span data-stu-id="5d241-245">Enable-Migrations</span></span>
2. <span data-ttu-id="5d241-246">Migration ajouter Init</span><span class="sxs-lookup"><span data-stu-id="5d241-246">Add-Migration Init</span></span>
3. <span data-ttu-id="5d241-247">Base de données de mise à jour</span><span class="sxs-lookup"><span data-stu-id="5d241-247">Update-Database</span></span>

<span data-ttu-id="5d241-248">Exécutez l’application et utilisez FaceBook et Google pour vous connecter et d’inscrire certains utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5d241-248">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="5d241-249">Examiner les données d’appartenance</span><span class="sxs-lookup"><span data-stu-id="5d241-249">Examine the Membership Data</span></span>

<span data-ttu-id="5d241-250">Dans le **vue** menu, cliquez sur **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="5d241-250">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="5d241-251">Bouton droit sur **AspNetUsers** et cliquez sur **afficher les données de Table**.</span><span class="sxs-lookup"><span data-stu-id="5d241-251">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="5d241-252">Le `HomeTown` et `BirthDate` champs sont affichés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5d241-252">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="5d241-253">La déconnexion de votre application et se connecter avec un autre compte</span><span class="sxs-lookup"><span data-stu-id="5d241-253">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="5d241-254">Si vous ouvrez une session sur votre application avec Facebook et puis fermer la session et essayez de se connecter à nouveau avec un autre compte Facebook (à l’aide du même navigateur), vous serez immédiatement connecté pour le compte Facebook précédent, que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="5d241-254">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="5d241-255">Pour utiliser un autre compte, vous devez accéder à Facebook et fermez la session à Facebook.</span><span class="sxs-lookup"><span data-stu-id="5d241-255">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="5d241-256">La même règle s’applique à n’importe quel autre 3e partie fournisseur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="5d241-256">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="5d241-257">Ou bien, vous pouvez vous connecter avec un autre compte à l’aide d’un navigateur différent.</span><span class="sxs-lookup"><span data-stu-id="5d241-257">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d241-258">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5d241-258">Next Steps</span></span>

<span data-ttu-id="5d241-259">Consultez [présentation des fournisseurs de sécurité Yahoo et LinkedIn OAuth pour OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) par Jerrie Pelser pour obtenir des instructions Yahoo et LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="5d241-259">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="5d241-260">Consultez Jerrie boutons de connexion sociale pour ASP.NET MVC 5 obtenir des boutons de connexion sociale activer des trucs assez.</span><span class="sxs-lookup"><span data-stu-id="5d241-260">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="5d241-261">Suivez le didacticiel de mon [créer une application ASP.NET MVC avec l’authentification et de la base de données SQL et le déployer vers Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), qui continue de ce didacticiel et affiche les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5d241-261">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="5d241-262">Comment déployer votre application sur Azure.</span><span class="sxs-lookup"><span data-stu-id="5d241-262">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="5d241-263">Comment sécuriser votre application avec des rôles.</span><span class="sxs-lookup"><span data-stu-id="5d241-263">How to secure you app with roles.</span></span>
3. <span data-ttu-id="5d241-264">Comment sécuriser votre application avec le [RequireHttps](https://msdn.microsoft.com/en-us/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) et [Authorize](https://msdn.microsoft.com/en-us/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filtres.</span><span class="sxs-lookup"><span data-stu-id="5d241-264">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/en-us/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/en-us/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="5d241-265">Comment utiliser l’API d’appartenance pour ajouter des utilisateurs et des rôles.</span><span class="sxs-lookup"><span data-stu-id="5d241-265">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="5d241-266">Veuillez laisser des commentaires sur la façon dont vous avez aimé ce didacticiel et nous pouvons améliorer.</span><span class="sxs-lookup"><span data-stu-id="5d241-266">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="5d241-267">Vous pouvez également demander de nouvelles rubriques à [afficher Me comment avec le Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span><span class="sxs-lookup"><span data-stu-id="5d241-267">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="5d241-268">Vous pouvez même demander et voter sur les nouvelles fonctionnalités à ajouter à ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5d241-268">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="5d241-269">Par exemple, vous pouvez voter pour un outil [créer et gérer des utilisateurs et des rôles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="5d241-269">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="5d241-270">Pour une bonne explication du fonctionnement des Services d’authentification externe ASP.NET, consultez de Robert McMurray [des Services d’authentification externe](https://asp.net/web-api/overview/security/external-authentication-services).</span><span class="sxs-lookup"><span data-stu-id="5d241-270">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="5d241-271">Article de Robert va également dans les détails de l’activation de l’authentification de Microsoft et Twitter.</span><span class="sxs-lookup"><span data-stu-id="5d241-271">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="5d241-272">Tom Dykstra l’excellent [didacticiel d’EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) montre comment travailler avec Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="5d241-272">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>