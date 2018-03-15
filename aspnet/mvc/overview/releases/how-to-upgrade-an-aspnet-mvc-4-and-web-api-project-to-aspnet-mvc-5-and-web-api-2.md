---
uid: mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
title: "Comment mettre à niveau un ASP.NET MVC 4 et Web de projet d’API à ASP.NET MVC 5 et Web API 2 | Documents Microsoft"
author: Rick-Anderson
description: "ASP.NET MVC 5 et Web API 2 mettre un ordinateur hôte de nouvelles fonctionnalités, y compris le routage d’attributs, des filtres de l’authentification et bien plus encore."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: db0d02d9-58e8-4a0b-8d7d-b8df8ea97b88
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 05a3189cf105d1230b96e90b46ea5ab60fef1bf1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2"></a><span data-ttu-id="e0db7-103">Comment mettre à niveau un ASP.NET MVC 4 et le projet d’API Web ASP.NET MVC 5 et API Web 2</span><span class="sxs-lookup"><span data-stu-id="e0db7-103">How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2</span></span>
====================
<span data-ttu-id="e0db7-104">Par [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="e0db7-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="e0db7-105">ASP.NET MVC 5 et Web API 2 mettre un ordinateur hôte de nouvelles fonctionnalités, y compris le routage d’attributs, des filtres de l’authentification et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e0db7-105">ASP.NET MVC 5 and Web API 2 bring a host of new features, including attribute routing, authentication filters, and much more.</span></span> <span data-ttu-id="e0db7-106">Consultez [https://www.asp.net/vnext](https://www.asp.net/core) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e0db7-106">See [https://www.asp.net/vnext](https://www.asp.net/core) for more details.</span></span>
> 
> <span data-ttu-id="e0db7-107">Cette procédure pas à pas vous guide avec les étapes requises pour mettre à niveau votre application vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="e0db7-107">This walkthrough will guide you with the steps required to upgrade your application to the latest version.</span></span>  
> 
> > [!NOTE]
> > <span data-ttu-id="e0db7-108">Consultez [ASP.NET et Web Tools pour Visual Studio 2013 Release Notes](../../../visual-studio/overview/2013/release-notes.md) pour plus d’informations sur les modifications avec rupture des API Web et de MVC 4 vers la version suivante.</span><span class="sxs-lookup"><span data-stu-id="e0db7-108">Please see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../visual-studio/overview/2013/release-notes.md) for information on breaking changes from MVC 4 and Web API to the next version.</span></span>
> 
>   
> 
> <span data-ttu-id="e0db7-109">Cet article a été écrit par Youngjune Hong et Rick Anderson ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )</span><span class="sxs-lookup"><span data-stu-id="e0db7-109">This article was written by Youngjune Hong and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>


## <a name="upgrade-steps"></a><span data-ttu-id="e0db7-110">Étapes de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="e0db7-110">Upgrade Steps</span></span>

1. <span data-ttu-id="e0db7-111">Sauvegarde de votre projet.</span><span class="sxs-lookup"><span data-stu-id="e0db7-111">Backup your project.</span></span> <span data-ttu-id="e0db7-112">Cette procédure pas à pas vous obligent à apporter des modifications à votre fichier projet, les configuration de package et les fichiers web.config.</span><span class="sxs-lookup"><span data-stu-id="e0db7-112">This walkthrough will require you to make changes to your project file, package configuration, and web.config files.</span></span>
2. <span data-ttu-id="e0db7-113">Pour mettre à niveau à partir de l’API Web API Web 2, dans global.asax, modifier :</span><span class="sxs-lookup"><span data-stu-id="e0db7-113">For upgrading from Web API to Web API 2, in global.asax, change:</span></span>

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample1.cs)]

 <span data-ttu-id="e0db7-114">par celle-ci :</span><span class="sxs-lookup"><span data-stu-id="e0db7-114">to</span></span>

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample2.cs)]
3. <span data-ttu-id="e0db7-115">Assurez-vous que tous les packages qui utilisent de vos projets sont compatibles avec MVC 5 et des API Web 2.</span><span class="sxs-lookup"><span data-stu-id="e0db7-115">Make sure all the packages that your projects use are compatible with MVC 5 and Web API 2.</span></span> <span data-ttu-id="e0db7-116">Le tableau indique le MVC 4 et les API Web suivantes liées packages que doivent être modifiées.</span><span class="sxs-lookup"><span data-stu-id="e0db7-116">The following table shows the MVC 4 and Web API related packages than need to be changed.</span></span> <span data-ttu-id="e0db7-117">Si vous avez un package qui est dépendant d’un des packages répertoriés ci-dessous, veuillez contacter les serveurs de publication pour obtenir les versions plus récentes qui sont compatibles avec MVC 5 et Web API 2.</span><span class="sxs-lookup"><span data-stu-id="e0db7-117">If you have a package that is dependent on one of the packages listed below, please contact the publishers to get the newer versions that are compatible with MVC 5 and Web API 2.</span></span> <span data-ttu-id="e0db7-118">Si vous avez le code source pour ces packages, vous devez les recompiler avec les nouveaux assemblys de MVC 5 et Web API 2.</span><span class="sxs-lookup"><span data-stu-id="e0db7-118">If you have the source code for those packages, you should recompile them with the new assemblies of MVC 5 and Web API 2.</span></span>   

    | <span data-ttu-id="e0db7-119">**Id de package**</span><span class="sxs-lookup"><span data-stu-id="e0db7-119">**Package Id**</span></span> | <span data-ttu-id="e0db7-120">**Ancienne version**</span><span class="sxs-lookup"><span data-stu-id="e0db7-120">**Old version**</span></span> | <span data-ttu-id="e0db7-121">**Nouvelle version**</span><span class="sxs-lookup"><span data-stu-id="e0db7-121">**New version**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="e0db7-122">Microsoft.AspNet.Razor</span><span class="sxs-lookup"><span data-stu-id="e0db7-122">Microsoft.AspNet.Razor</span></span> | <span data-ttu-id="e0db7-123">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-123">2.0.x.x</span></span> | <span data-ttu-id="e0db7-124">3.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-124">3.0.0</span></span> |
    | <span data-ttu-id="e0db7-125">Microsoft.AspNet.WebPages</span><span class="sxs-lookup"><span data-stu-id="e0db7-125">Microsoft.AspNet.WebPages</span></span> | <span data-ttu-id="e0db7-126">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-126">2.0.x.x</span></span> | <span data-ttu-id="e0db7-127">3.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-127">3.0.0</span></span> |
    | <span data-ttu-id="e0db7-128">Microsoft.AspNet.WebPages.WebData</span><span class="sxs-lookup"><span data-stu-id="e0db7-128">Microsoft.AspNet.WebPages.WebData</span></span> | <span data-ttu-id="e0db7-129">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-129">2.0.x.x</span></span> | <span data-ttu-id="e0db7-130">3.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-130">3.0.0</span></span> |
    | <span data-ttu-id="e0db7-131">Microsoft.AspNet.WebPages.OAuth</span><span class="sxs-lookup"><span data-stu-id="e0db7-131">Microsoft.AspNet.WebPages.OAuth</span></span> | <span data-ttu-id="e0db7-132">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-132">2.0.x.x</span></span> | <span data-ttu-id="e0db7-133">3.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-133">3.0.0</span></span> |
    | <span data-ttu-id="e0db7-134">Microsoft.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="e0db7-134">Microsoft.AspNet.Mvc</span></span> | <span data-ttu-id="e0db7-135">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-135">4.0.x.x</span></span> | <span data-ttu-id="e0db7-136">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-136">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-137">Microsoft.AspNet.Mvc.Facebook</span><span class="sxs-lookup"><span data-stu-id="e0db7-137">Microsoft.AspNet.Mvc.Facebook</span></span> | <span data-ttu-id="e0db7-138">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-138">4.0.x.x</span></span> | <span data-ttu-id="e0db7-139">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-139">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-140">Microsoft.AspNet.WebApi.Core</span><span class="sxs-lookup"><span data-stu-id="e0db7-140">Microsoft.AspNet.WebApi.Core</span></span> | <span data-ttu-id="e0db7-141">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-141">4.0.x.x</span></span> | <span data-ttu-id="e0db7-142">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-142">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-143">Microsoft.AspNet.WebApi.SelfHost</span><span class="sxs-lookup"><span data-stu-id="e0db7-143">Microsoft.AspNet.WebApi.SelfHost</span></span> | <span data-ttu-id="e0db7-144">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-144">4.0.x.x</span></span> | <span data-ttu-id="e0db7-145">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-145">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-146">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="e0db7-146">Microsoft.AspNet.WebApi.Client</span></span> | <span data-ttu-id="e0db7-147">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-147">4.0.x.x</span></span> | <span data-ttu-id="e0db7-148">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-148">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-149">Microsoft.AspNet.WebApi.OData</span><span class="sxs-lookup"><span data-stu-id="e0db7-149">Microsoft.AspNet.WebApi.OData</span></span> | <span data-ttu-id="e0db7-150">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-150">4.0.x.x</span></span> | <span data-ttu-id="e0db7-151">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-151">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-152">Microsoft.AspNet.WebApi</span><span class="sxs-lookup"><span data-stu-id="e0db7-152">Microsoft.AspNet.WebApi</span></span> | <span data-ttu-id="e0db7-153">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-153">4.0.x.x</span></span> | <span data-ttu-id="e0db7-154">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-154">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-155">Microsoft.AspNet.WebApi.WebHost</span><span class="sxs-lookup"><span data-stu-id="e0db7-155">Microsoft.AspNet.WebApi.WebHost</span></span> | <span data-ttu-id="e0db7-156">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-156">4.0.x.x</span></span> | <span data-ttu-id="e0db7-157">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-157">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-158">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="e0db7-158">Microsoft.AspNet.WebApi.Tracing</span></span> | <span data-ttu-id="e0db7-159">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-159">4.0.x.x</span></span> | <span data-ttu-id="e0db7-160">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-160">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-161">Microsoft.AspNet.WebApi.HelpPage</span><span class="sxs-lookup"><span data-stu-id="e0db7-161">Microsoft.AspNet.WebApi.HelpPage</span></span> | <span data-ttu-id="e0db7-162">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-162">4.0.x.x</span></span> | <span data-ttu-id="e0db7-163">5.0.0</span><span class="sxs-lookup"><span data-stu-id="e0db7-163">5.0.0</span></span> |
    | <span data-ttu-id="e0db7-164">Microsoft.Net.Http</span><span class="sxs-lookup"><span data-stu-id="e0db7-164">Microsoft.Net.Http</span></span> | <span data-ttu-id="e0db7-165">2.0.x.</span><span class="sxs-lookup"><span data-stu-id="e0db7-165">2.0.x.</span></span> | <span data-ttu-id="e0db7-166">2.2.x.</span><span class="sxs-lookup"><span data-stu-id="e0db7-166">2.2.x.</span></span> |
    | <span data-ttu-id="e0db7-167">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="e0db7-167">Microsoft.Data.OData</span></span> | <span data-ttu-id="e0db7-168">5.2.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-168">5.2.x</span></span> | <span data-ttu-id="e0db7-169">5.6.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-169">5.6.x</span></span> |
    | <span data-ttu-id="e0db7-170">System.Spatial</span><span class="sxs-lookup"><span data-stu-id="e0db7-170">System.Spatial</span></span> | <span data-ttu-id="e0db7-171">5.2.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-171">5.2.x</span></span> | <span data-ttu-id="e0db7-172">5.6.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-172">5.6.x</span></span> |
    | <span data-ttu-id="e0db7-173">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="e0db7-173">Microsoft.Data.Edm</span></span> | <span data-ttu-id="e0db7-174">5.2.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-174">5.2.x</span></span> | <span data-ttu-id="e0db7-175">5.6.x</span><span class="sxs-lookup"><span data-stu-id="e0db7-175">5.6.x</span></span> |
    | <span data-ttu-id="e0db7-176">Microsoft.AspNet.Mvc.FixedDisplayModes</span><span class="sxs-lookup"><span data-stu-id="e0db7-176">Microsoft.AspNet.Mvc.FixedDisplayModes</span></span> | <span data-ttu-id="e0db7-177">< o : p >< / o : p ></span><span class="sxs-lookup"><span data-stu-id="e0db7-177"><o:p> </o:p></span></span> | <span data-ttu-id="e0db7-178">Supprimé</span><span class="sxs-lookup"><span data-stu-id="e0db7-178">Removed</span></span> |
    | <span data-ttu-id="e0db7-179">Microsoft.AspNet.WebPages.Administration</span><span class="sxs-lookup"><span data-stu-id="e0db7-179">Microsoft.AspNet.WebPages.Administration</span></span> | <span data-ttu-id="e0db7-180">< o : p >< / o : p ></span><span class="sxs-lookup"><span data-stu-id="e0db7-180"><o:p> </o:p></span></span> | <span data-ttu-id="e0db7-181">Supprimé</span><span class="sxs-lookup"><span data-stu-id="e0db7-181">Removed</span></span> |
    | <span data-ttu-id="e0db7-182">Applications auxiliaires Web de Microsoft</span><span class="sxs-lookup"><span data-stu-id="e0db7-182">Microsoft-Web-Helpers</span></span> | <span data-ttu-id="e0db7-183">< o : p >< / o : p ></span><span class="sxs-lookup"><span data-stu-id="e0db7-183"><o:p> </o:p></span></span> | <span data-ttu-id="e0db7-184">Microsoft.AspNet.WebHelpers</span><span class="sxs-lookup"><span data-stu-id="e0db7-184">Microsoft.AspNet.WebHelpers</span></span> |

    > [!NOTE]
    > <span data-ttu-id="e0db7-185">Applications auxiliaires Web de Microsoft a été remplacée par Microsoft.AspNet.WebHelpers.</span><span class="sxs-lookup"><span data-stu-id="e0db7-185">Microsoft-Web-Helpers has been replaced with Microsoft.AspNet.WebHelpers.</span></span> <span data-ttu-id="e0db7-186">Vous devez d’abord supprimer l’ancien package et puis installer le package plus récente.</span><span class="sxs-lookup"><span data-stu-id="e0db7-186">You should remove the old package first, and then install the newer package.</span></span>   
    >   
    > <span data-ttu-id="e0db7-187">Il n’existe aucune compatibilité entre versions parmi les principaux packages d’ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e0db7-187">There is no cross version compatibility among major ASP.NET packages.</span></span> <span data-ttu-id="e0db7-188">Par exemple, MVC 5 est compatible uniquement avec Razor 3 et non de 2 Razor.</span><span class="sxs-lookup"><span data-stu-id="e0db7-188">For example, MVC 5 is compatible with only Razor 3, and not Razor 2.</span></span>
4. <span data-ttu-id="e0db7-189">Ouvrez votre projet dans Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="e0db7-189">Open your project in Visual Studio 2013.</span></span>
5. <span data-ttu-id="e0db7-190">Supprimez l’un des packages NuGet ASP.NET suivants qui sont installés.</span><span class="sxs-lookup"><span data-stu-id="e0db7-190">Remove any of the following ASP.NET NuGet packages that are installed.</span></span> <span data-ttu-id="e0db7-191">Vous allez supprimer à l’aide de la Console Gestionnaire de Package (PMC).</span><span class="sxs-lookup"><span data-stu-id="e0db7-191">You will remove these using the Package Manager Console (PMC).</span></span> <span data-ttu-id="e0db7-192">Pour ouvrir le PMC, sélectionnez le **outils** , puis sélectionnez **Gestionnaire de Package de bibliothèque,** puis sélectionnez **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e0db7-192">To open the PMC, select the **Tools** menu and then select **Library Package Manager,** then select **Package Manager Console**.</span></span> <span data-ttu-id="e0db7-193">Votre projet ne peut pas inclure tous ces éléments.</span><span class="sxs-lookup"><span data-stu-id="e0db7-193">Your project might not include all of these.</span></span>

    1. `Microsoft.AspNet.WebPages.Administration`  
 <span data-ttu-id="e0db7-194">Ce package est en principe ajouté lors de la mise à niveau à partir de MVC 3 vers MVC 4.</span><span class="sxs-lookup"><span data-stu-id="e0db7-194">This package is typically added when upgrading from MVC 3 to MVC 4.</span></span> <span data-ttu-id="e0db7-195">Pour le supprimer, exécutez la commande suivante dans le PMC :</span><span class="sxs-lookup"><span data-stu-id="e0db7-195">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft.AspNet.WebPages.Administration`
    2. `Microsoft-Web-Helpers`   
 <span data-ttu-id="e0db7-196">Ce package a été renommé `Microsoft.AspNet.WebHelpers`.</span><span class="sxs-lookup"><span data-stu-id="e0db7-196">This package has been rebranded as `Microsoft.AspNet.WebHelpers`.</span></span> <span data-ttu-id="e0db7-197">Pour le supprimer, exécutez la commande suivante dans le PMC :</span><span class="sxs-lookup"><span data-stu-id="e0db7-197">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft-Web-Helpers`
    3. `Microsoft.AspNet.Mvc.FixedDisplayMode`  
 <span data-ttu-id="e0db7-198">Ce package contient une solution de contournement pour un bogue dans MVC 4 qui a été résolu dans MVC 5.</span><span class="sxs-lookup"><span data-stu-id="e0db7-198">This package contains a work around for a bug in MVC 4 that has been fixed in MVC 5.</span></span> <span data-ttu-id="e0db7-199">Pour le supprimer, exécutez la commande suivante dans le PMC :</span><span class="sxs-lookup"><span data-stu-id="e0db7-199">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft.AspNet.Mvc.FixedDisplayModes`
6. <span data-ttu-id="e0db7-200">Mettre à niveau tous les packages NuGet ASP.NET à l’aide de la PMC.</span><span class="sxs-lookup"><span data-stu-id="e0db7-200">Upgrade all the ASP.NET NuGet packages using the PMC.</span></span> <span data-ttu-id="e0db7-201">Dans le CFP, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e0db7-201">In the PMC, run the following command:</span></span>  
    `Update-Package`  
 <span data-ttu-id="e0db7-202">Le `Update-Package` de commande sans aucun paramètre met à jour chaque package.</span><span class="sxs-lookup"><span data-stu-id="e0db7-202">The `Update-Package` command without any parameters will update every package.</span></span> <span data-ttu-id="e0db7-203">Vous pouvez mettre à jour individuellement des packages à l’aide de l’argument ID.</span><span class="sxs-lookup"><span data-stu-id="e0db7-203">You can update packages individually by using the ID argument.</span></span> <span data-ttu-id="e0db7-204">Pour plus d’informations sur la commande de mise à jour, exécutez `get-help update-package` .</span><span class="sxs-lookup"><span data-stu-id="e0db7-204">For more information about the update command, run     `get-help update-package` .</span></span>

## <a name="update-the-application-webconfig-file"></a><span data-ttu-id="e0db7-205">Mettre à jour de l’Application *web.config* fichier</span><span class="sxs-lookup"><span data-stu-id="e0db7-205">Update the Application *web.config* File</span></span>

<span data-ttu-id="e0db7-206">Veillez à effectuer ces modifications dans l’application *web.config* impossible dans le fichier, le *web.config* de fichiers dans le *vues* dossier.</span><span class="sxs-lookup"><span data-stu-id="e0db7-206">Be sure to make these changes in the app *web.config* file, not the *web.config* file in the *Views* folder.</span></span>

<span data-ttu-id="e0db7-207">Recherchez la `<runtime>/<assemblyBinding>` section et apportez les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0db7-207">Locate the `<runtime>/<assemblyBinding>` section, and make the following changes:</span></span>

1. <span data-ttu-id="e0db7-208">Dans les éléments avec l’attribut de nom « System.Web.Mvc », modifiez le numéro de version à partir de « 4.0.0.0 » à « 5.0.0.0 ».</span><span class="sxs-lookup"><span data-stu-id="e0db7-208">In the elements with the name attribute "System.Web.Mvc", change the version number from "4.0.0.0" to "5.0.0.0".</span></span> <span data-ttu-id="e0db7-209">(Deux modifications dans cet élément.)</span><span class="sxs-lookup"><span data-stu-id="e0db7-209">(Two changes in that element.)</span></span>
2. <span data-ttu-id="e0db7-210">Dans les éléments avec l’attribut de nom &quot;System.Web.Helpers » et &quot;System.Web.WebPages&quot; modifier le numéro de version à partir de « 2.0.0.0 » à « 3.0.0.0 ».</span><span class="sxs-lookup"><span data-stu-id="e0db7-210">In elements with the name attribute &quot;System.Web.Helpers" and &quot;System.Web.WebPages&quot; change the version number from "2.0.0.0" to "3.0.0.0".</span></span> <span data-ttu-id="e0db7-211">Quatre modifications se produira, deux dans chacun des éléments.</span><span class="sxs-lookup"><span data-stu-id="e0db7-211">Four changes will occur, two in each of the elements.</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample3.xml?highlight=6,10,14)]
3. <span data-ttu-id="e0db7-212">Recherchez la `<appSettings>` section et mettre à jour le webpages:version de 2.0.0.0.0 à 3.0.0.0, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e0db7-212">Locate the `<appSettings>` section and update the webpages:version from 2.0.0.0.0 to 3.0.0.0 as shown below:</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample4.xml?highlight=2)]
4. <span data-ttu-id="e0db7-213">Supprimez tous les niveaux de confiance qu’intégral.</span><span class="sxs-lookup"><span data-stu-id="e0db7-213">Remove any trust levels other than Full.</span></span> <span data-ttu-id="e0db7-214">Exemple :</span><span class="sxs-lookup"><span data-stu-id="e0db7-214">For example:</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample5.xml?highlight=2)]

## <a name="update-the-webconfig-files-under-the-views-folder"></a><span data-ttu-id="e0db7-215">Mise à jour la *web.config* fichiers sous le dossier Views</span><span class="sxs-lookup"><span data-stu-id="e0db7-215">Update the *web.config* files under the Views folder</span></span>

<span data-ttu-id="e0db7-216">Si votre application est à l’aide de zones, vous devez également mettre à jour chacun *web.config* de fichiers dans le *vues* sous-dossier du dossier de chaque zone.</span><span class="sxs-lookup"><span data-stu-id="e0db7-216">If your application is using areas, you will also need to update each *web.config* file in the *Views* sub-folder of each Area folder.</span></span>

1. <span data-ttu-id="e0db7-217">Mettre à jour tous les éléments qui contiennent « System.Web.Mvc » à partir de la version « 4.0.0.0 » version « 5.0.0.0 ».</span><span class="sxs-lookup"><span data-stu-id="e0db7-217">Update all elements that contain "System.Web.Mvc" from version "4.0.0.0" to version "5.0.0.0".</span></span>  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample6.xml?highlight=2)]

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample7.xml?highlight=4-6,8)]
2. <span data-ttu-id="e0db7-218">Mettre à jour tous les éléments qui contiennent « System.Web.WebPages.Razor » à partir de la version « 2.0.0.0 » version « 3.0.0.0 ».</span><span class="sxs-lookup"><span data-stu-id="e0db7-218">Update all elements that contain "System.Web.WebPages.Razor" from version "2.0.0.0" to version"3.0.0.0".</span></span> <span data-ttu-id="e0db7-219">Si cette section contient « System.Web.WebPages », mettre à jour ces éléments à partir de la version « 2.0.0.0 » version « 3.0.0.0 »</span><span class="sxs-lookup"><span data-stu-id="e0db7-219">If this section contains "System.Web.WebPages", update those elements from version "2.0.0.0" to version"3.0.0.0"</span></span>  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="e0db7-220">Si vous avez supprimé le `Microsoft-Web-Helpers` installation du package NuGet à l’étape précédente, `Microsoft.AspNet.WebHelpers` avec la commande suivante dans le PMC :</span><span class="sxs-lookup"><span data-stu-id="e0db7-220">If you removed the `Microsoft-Web-Helpers` NuGet package in a previous step, install `Microsoft.AspNet.WebHelpers` with the following command in the PMC:</span></span>  
    `Install-Package -Id Microsoft.AspNet.WebHelpers`
4. <span data-ttu-id="e0db7-221">Si votre application utilise le [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) (méthode), ajoutez le code suivant à la *Web.config* fichier.</span><span class="sxs-lookup"><span data-stu-id="e0db7-221">If your app uses the [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) method, add the following to the *Web.config* file.</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample9.xml)]

## <a name="final-steps"></a><span data-ttu-id="e0db7-222">Dernières étapes</span><span class="sxs-lookup"><span data-stu-id="e0db7-222">Final Steps</span></span>

<span data-ttu-id="e0db7-223">Générez et testez l’application.</span><span class="sxs-lookup"><span data-stu-id="e0db7-223">Build and test the application.</span></span>

<span data-ttu-id="e0db7-224">Supprimer le type de projet MVC 4 GUID à partir des fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="e0db7-224">Remove the MVC 4 project type GUID from the project files.</span></span>

1. <span data-ttu-id="e0db7-225">Dans l’Explorateur de solutions, cliquez sur le nom du projet, puis sélectionnez **décharger le projet**.</span><span class="sxs-lookup"><span data-stu-id="e0db7-225">In Solution Explorer, right-click the project name and then select **Unload Project**.</span></span>
2. <span data-ttu-id="e0db7-226">Cliquez sur le projet, puis sélectionnez Modifier NomProjet.csproj.</span><span class="sxs-lookup"><span data-stu-id="e0db7-226">Right-click the project and select Edit ProjectName.csproj.</span></span>
3. <span data-ttu-id="e0db7-227">Recherchez le `ProjectTypeGuids` élément, puis supprimer le MVC 4 GUID du projet `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`.</span><span class="sxs-lookup"><span data-stu-id="e0db7-227">Locate the `ProjectTypeGuids` element and then remove the MVC 4 project GUID, `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`.</span></span>
4. <span data-ttu-id="e0db7-228">Enregistrez et fermez le fichier de projet ouvert.</span><span class="sxs-lookup"><span data-stu-id="e0db7-228">Save and close the open project file.</span></span>
5. <span data-ttu-id="e0db7-229">Cliquez sur le projet et sélectionnez **recharger le projet**.</span><span class="sxs-lookup"><span data-stu-id="e0db7-229">Right-click the project and select **Reload Project**.</span></span>