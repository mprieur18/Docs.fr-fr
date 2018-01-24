---
title: "Prévention des attaques de redirection ouvert dans une application ASP.NET Core | Documents Microsoft"
author: ardalis
description: "Montre comment empêcher des attaques de redirection ouvert par rapport à une application ASP.NET Core"
ms.author: riande
manager: wpickett
ms.date: 07/07/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/preventing-open-redirects
ms.openlocfilehash: e57ae429e9af54ade74485361ba591cb75c16752
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="preventing-open-redirect-attacks-in-an-aspnet-core-app"></a><span data-ttu-id="cceab-103">Prévention des attaques de redirection ouvert dans une application ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cceab-103">Preventing Open Redirect Attacks in an ASP.NET Core app</span></span>

<span data-ttu-id="cceab-104">Une application web qui effectue une redirection vers une URL qui est spécifiée via la demande tels que les données de chaîne de requête ou un formulaire peut potentiellement être falsifiée rediriger les utilisateurs vers une URL externe, malveillante.</span><span class="sxs-lookup"><span data-stu-id="cceab-104">A web app that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="cceab-105">Cette manipulation est appelée une attaque de redirection ouvert.</span><span class="sxs-lookup"><span data-stu-id="cceab-105">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="cceab-106">Chaque fois que votre logique d’application redirige vers une URL spécifiée, vous devez vérifier que l’URL de redirection n’a pas été falsifié.</span><span class="sxs-lookup"><span data-stu-id="cceab-106">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="cceab-107">ASP.NET Core intègre des fonctionnalités pour aider à protéger les applications contre les attaques de redirection ouvert (également appelé open redirection).</span><span class="sxs-lookup"><span data-stu-id="cceab-107">ASP.NET Core has built-in functionality to help protect apps from open redirect (also known as open redirection) attacks.</span></span>

## <a name="what-is-an-open-redirect-attack"></a><span data-ttu-id="cceab-108">Qu’est une attaque de redirection ouvrir ?</span><span class="sxs-lookup"><span data-stu-id="cceab-108">What is an open redirect attack?</span></span>

<span data-ttu-id="cceab-109">Les applications Web rediriger fréquemment les utilisateurs vers une page de connexion lorsqu’ils accèdent aux ressources qui requièrent une authentification.</span><span class="sxs-lookup"><span data-stu-id="cceab-109">Web applications frequently redirect users to a login page when they access resources that require authentication.</span></span> <span data-ttu-id="cceab-110">La redirection typlically inclut un `returnUrl` paramètre querystring afin que l’utilisateur peut être retourné à l’URL demandée à l’origine une fois qu’ils ont connecté avec succès.</span><span class="sxs-lookup"><span data-stu-id="cceab-110">The redirection typlically includes a `returnUrl` querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span> <span data-ttu-id="cceab-111">Une fois que l’utilisateur s’authentifie, ils sont redirigés vers l’URL qui avait initialement demandée.</span><span class="sxs-lookup"><span data-stu-id="cceab-111">After the user authenticates, they are redirected to the URL they had originally requested.</span></span>

<span data-ttu-id="cceab-112">Étant donné que l’URL de destination est spécifié dans la chaîne de requête de la demande, un utilisateur malveillant peut falsifier la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="cceab-112">Because the destination URL is specified in the querystring of the request, a malicious user could tamper with the querystring.</span></span> <span data-ttu-id="cceab-113">Une chaîne de requête falsifiée pourrait permettre au site pour rediriger l’utilisateur vers un site externe, malveillant.</span><span class="sxs-lookup"><span data-stu-id="cceab-113">A tampered querystring could allow the site to redirect the user to an external, malicious site.</span></span> <span data-ttu-id="cceab-114">Cette technique est appelée une attaque de redirection (ou une redirection) ouverte.</span><span class="sxs-lookup"><span data-stu-id="cceab-114">This technique is called an open redirect (or redirection) attack.</span></span>

### <a name="an-example-attack"></a><span data-ttu-id="cceab-115">Une attaque de l’exemple</span><span class="sxs-lookup"><span data-stu-id="cceab-115">An example attack</span></span>

<span data-ttu-id="cceab-116">Un utilisateur malveillant peut développer une attaque conçue pour permettre l’accès utilisateur malveillant pour les informations d’identification d’un utilisateur ou les informations sensibles sur votre application.</span><span class="sxs-lookup"><span data-stu-id="cceab-116">A malicious user could develop an attack intended to allow the malicious user access to a user's credentials or sensitive information on your app.</span></span> <span data-ttu-id="cceab-117">Pour lancer l’attaque, elles convaincre l’utilisateur clique sur un lien vers la page de connexion de votre site, avec un `returnUrl` valeur de chaîne de requête ajoutée à l’URL.</span><span class="sxs-lookup"><span data-stu-id="cceab-117">To begin the attack, they convince the user to click a link to your site's login page, with a `returnUrl` querystring value added to the URL.</span></span> <span data-ttu-id="cceab-118">Par exemple, le [NerdDinner.com](http://nerddinner.com) exemple d’application (écrite pour ASP.NET MVC) inclut ce une page de connexion ici : ``http://nerddinner.com/Account/LogOn?returnUrl=/Home/About``.</span><span class="sxs-lookup"><span data-stu-id="cceab-118">For example, the [NerdDinner.com](http://nerddinner.com) sample application (written for ASP.NET MVC) includes such a login page here: ``http://nerddinner.com/Account/LogOn?returnUrl=/Home/About``.</span></span> <span data-ttu-id="cceab-119">L’attaque puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cceab-119">The attack then follows these steps:</span></span>

1. <span data-ttu-id="cceab-120">Utilisateur clique sur un lien vers ``http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn`` (Notez que la deuxième URL est nerddi**n**er, pas nerddi**nn**er).</span><span class="sxs-lookup"><span data-stu-id="cceab-120">User clicks a link to ``http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn`` (note, second URL is nerddi**n**er, not nerddi**nn**er).</span></span>
2. <span data-ttu-id="cceab-121">L’utilisateur parvient à se connecter.</span><span class="sxs-lookup"><span data-stu-id="cceab-121">The user logs in successfully.</span></span>
3. <span data-ttu-id="cceab-122">L’utilisateur est redirigé (par le site) à ``http://nerddiner.com/Account/LogOn`` (site malveillant qui ressemble à un site réel).</span><span class="sxs-lookup"><span data-stu-id="cceab-122">The user is redirected (by the site) to ``http://nerddiner.com/Account/LogOn`` (malicious site that looks like real site).</span></span>
4. <span data-ttu-id="cceab-123">L’utilisateur se connecte à nouveau (donnant malveillant leurs informations d’identification de site) et est redirigé vers le site réel.</span><span class="sxs-lookup"><span data-stu-id="cceab-123">The user logs in again (giving malicious site their credentials) and is redirected back to the real site.</span></span>

<span data-ttu-id="cceab-124">L’utilisateur sera pensez probablement de leur première tentative de connexion a échoué, et leur autre a réussi.</span><span class="sxs-lookup"><span data-stu-id="cceab-124">The user will likely believe their first attempt to log in failed, and their second one was successful.</span></span> <span data-ttu-id="cceab-125">Ils allez restent très probablement pas au courant leurs informations d’identification ont été compromises.</span><span class="sxs-lookup"><span data-stu-id="cceab-125">They'll most likely remain unaware their credentials have been compromised.</span></span>

![Processus d’attaque Redirection ouvert](preventing-open-redirects/_static/open-redirection-attack-process.png)

<span data-ttu-id="cceab-127">En plus des pages de connexion, certains sites fournissent des points de terminaison ou des pages de redirection.</span><span class="sxs-lookup"><span data-stu-id="cceab-127">In addition to login pages, some sites provide redirect pages or endpoints.</span></span> <span data-ttu-id="cceab-128">Imaginez que votre application comprend une page avec une redirection d’ouvrir, ``/Home/Redirect``.</span><span class="sxs-lookup"><span data-stu-id="cceab-128">Imagine your app has a page with an open redirect, ``/Home/Redirect``.</span></span> <span data-ttu-id="cceab-129">Un attaquant pourrait créer, par exemple, un lien dans un message électronique qui accède à ``[yoursite]/Home/Redirect?url=http://phishingsite.com/Home/Login``.</span><span class="sxs-lookup"><span data-stu-id="cceab-129">An attacker could create, for example, a link in an email that goes to ``[yoursite]/Home/Redirect?url=http://phishingsite.com/Home/Login``.</span></span> <span data-ttu-id="cceab-130">Un utilisateur à l’URL et voir qu'il commence par le nom de votre site.</span><span class="sxs-lookup"><span data-stu-id="cceab-130">A typical user will look at the URL and see it begins with your site name.</span></span> <span data-ttu-id="cceab-131">Approbation qui, elles devra cliquer sur le lien.</span><span class="sxs-lookup"><span data-stu-id="cceab-131">Trusting that, they will click the link.</span></span> <span data-ttu-id="cceab-132">La redirection ouvrir envoie ensuite l’utilisateur vers le site de hameçonnage, qui est identique à la vôtre, et l’utilisateur aurait probablement connexion pour qu’ils pensent est votre site.</span><span class="sxs-lookup"><span data-stu-id="cceab-132">The open redirect would then send the user to the phishing site, which looks identical to yours, and the user would likely login to what they believe is your site.</span></span>

## <a name="protecting-against-open-redirect-attacks"></a><span data-ttu-id="cceab-133">Protection contre les attaques de redirection ouvert</span><span class="sxs-lookup"><span data-stu-id="cceab-133">Protecting against open redirect attacks</span></span>

<span data-ttu-id="cceab-134">Lorsque vous développez des applications web, traiter toutes les données fournies par l’utilisateur comme non fiables.</span><span class="sxs-lookup"><span data-stu-id="cceab-134">When developing web applications, treat all user-provided data as untrustworthy.</span></span> <span data-ttu-id="cceab-135">Si votre application possède des fonctionnalités qui redirige l’utilisateur en fonction du contenu de l’URL, vérifiez que ces redirections sont effectuées uniquement localement dans votre application (ou à une URL connue, pas une URL qui peut être fournie dans la chaîne de requête).</span><span class="sxs-lookup"><span data-stu-id="cceab-135">If your application has functionality that redirects the user based on the contents of the URL,  ensure that such redirects are only done locally within your app (or to a known URL, not any URL that may be supplied in the querystring).</span></span>

### <a name="localredirect"></a><span data-ttu-id="cceab-136">LocalRedirect</span><span class="sxs-lookup"><span data-stu-id="cceab-136">LocalRedirect</span></span>

<span data-ttu-id="cceab-137">Utilisez le ``LocalRedirect`` méthode d’assistance à partir de la base de `Controller` classe :</span><span class="sxs-lookup"><span data-stu-id="cceab-137">Use the ``LocalRedirect`` helper method from the base `Controller` class:</span></span>

```csharp
public IActionResult SomeAction(string redirectUrl)
{
    return LocalRedirect(redirectUrl);
}
```

<span data-ttu-id="cceab-138">``LocalRedirect``lève une exception si une URL non local est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="cceab-138">``LocalRedirect`` will throw an exception if a non-local URL is specified.</span></span> <span data-ttu-id="cceab-139">Dans le cas contraire, il se comporte comme le ``Redirect`` (méthode).</span><span class="sxs-lookup"><span data-stu-id="cceab-139">Otherwise, it behaves just like the ``Redirect`` method.</span></span>

### <a name="islocalurl"></a><span data-ttu-id="cceab-140">IsLocalUrl</span><span class="sxs-lookup"><span data-stu-id="cceab-140">IsLocalUrl</span></span>

<span data-ttu-id="cceab-141">Utilisez le [IsLocalUrl](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.iurlhelper#Microsoft_AspNetCore_Mvc_IUrlHelper_IsLocalUrl_System_String_) méthode pour tester l’URL avant de rediriger les :</span><span class="sxs-lookup"><span data-stu-id="cceab-141">Use the [IsLocalUrl](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.iurlhelper#Microsoft_AspNetCore_Mvc_IUrlHelper_IsLocalUrl_System_String_) method to test URLs before redirecting:</span></span>

<span data-ttu-id="cceab-142">L’exemple suivant montre comment vérifier si une URL est locale avant de rediriger.</span><span class="sxs-lookup"><span data-stu-id="cceab-142">The following example shows how to check whether a URL is local before redirecting.</span></span>

```csharp
private IActionResult RedirectToLocal(string returnUrl)
{
    if (Url.IsLocalUrl(returnUrl))
    {
        return Redirect(returnUrl);
    }
    else
    {
        return RedirectToAction(nameof(HomeController.Index), "Home");
    }
}
```

<span data-ttu-id="cceab-143">Le `IsLocalUrl` méthode protège les utilisateurs en cours par inadvertance redirigés vers un site malveillant.</span><span class="sxs-lookup"><span data-stu-id="cceab-143">The `IsLocalUrl` method protects users from being inadvertently redirected to a malicious site.</span></span> <span data-ttu-id="cceab-144">Vous pouvez consigner les détails de l’URL qui a été fourni lorsqu’une URL non local est fournie dans une situation dans laquelle vous vous attendiez une URL locale.</span><span class="sxs-lookup"><span data-stu-id="cceab-144">You can log the details of the URL that was provided when a non-local URL is supplied in a situation where you expected a local URL.</span></span> <span data-ttu-id="cceab-145">Journalisation de redirection URL peuvent faciliter le diagnostic des attaques de redirection.</span><span class="sxs-lookup"><span data-stu-id="cceab-145">Logging redirect URLs may help in diagnosing redirection attacks.</span></span>