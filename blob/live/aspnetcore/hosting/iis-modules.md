---
title: "À l’aide des modules IIS avec ASP.NET Core"
author: guardrex
description: "Document de référence décrivant les modules IIS actifs et inactifs pour les applications ASP.NET Core."
keywords: "ASP.NET Core, iis, module, proxy inversé"
ms.author: riande
manager: wpickett
ms.date: 03/08/2017
ms.topic: article
ms.assetid: 492b3a7e-04c5-461b-b96a-38ecee5c64bc
ms.technology: aspnet
ms.prod: aspnet-core
uid: hosting/iis-modules
ms.openlocfilehash: fee8e830ab43f731de9c90fad06b577662760f87
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
# <a name="using-iis-modules-with-aspnet-core"></a><span data-ttu-id="96c21-104">À l’aide des Modules IIS avec ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="96c21-104">Using IIS Modules with ASP.NET Core</span></span>

<span data-ttu-id="96c21-105">Par [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="96c21-105">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="96c21-106">Les applications ASP.NET Core sont hébergées par IIS dans une configuration de proxy inverse.</span><span class="sxs-lookup"><span data-stu-id="96c21-106">ASP.NET Core applications are hosted by IIS in a reverse-proxy configuration.</span></span> <span data-ttu-id="96c21-107">Certains des modules IIS natifs et tous les modules IIS gérés ne sont pas disponibles pour traiter les demandes pour les applications ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="96c21-107">Some of the native IIS modules and all of the IIS managed modules are not available to process requests for ASP.NET Core apps.</span></span> <span data-ttu-id="96c21-108">Dans de nombreux cas, ASP.NET Core offre une alternative aux fonctionnalités des modules natifs et managés d’IIS.</span><span class="sxs-lookup"><span data-stu-id="96c21-108">In many cases, ASP.NET Core offers an alternative to the features of IIS native and managed modules.</span></span>

## <a name="native-modules"></a><span data-ttu-id="96c21-109">Modules natifs</span><span class="sxs-lookup"><span data-stu-id="96c21-109">Native Modules</span></span>
<span data-ttu-id="96c21-110">Module</span><span class="sxs-lookup"><span data-stu-id="96c21-110">Module</span></span> | <span data-ttu-id="96c21-111">.NET core actif</span><span class="sxs-lookup"><span data-stu-id="96c21-111">.NET Core Active</span></span> | <span data-ttu-id="96c21-112">Option ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="96c21-112">ASP.NET Core Option</span></span>
--- | :---: | ---
<span data-ttu-id="96c21-113">**Authentification anonyme**</span><span class="sxs-lookup"><span data-stu-id="96c21-113">**Anonymous Authentication**</span></span><br>`AnonymousAuthenticationModule` | <span data-ttu-id="96c21-114">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-114">Yes</span></span> | 
<span data-ttu-id="96c21-115">**Authentification de base**</span><span class="sxs-lookup"><span data-stu-id="96c21-115">**Basic Authentication**</span></span><br>`BasicAuthenticationModule` | <span data-ttu-id="96c21-116">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-116">Yes</span></span> | 
<span data-ttu-id="96c21-117">**Authentification par mappage de Certification de client**</span><span class="sxs-lookup"><span data-stu-id="96c21-117">**Client Certification Mapping Authentication**</span></span><br>`CertificateMappingAuthenticationModule` | <span data-ttu-id="96c21-118">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-118">Yes</span></span> | 
<span data-ttu-id="96c21-119">**CGI**</span><span class="sxs-lookup"><span data-stu-id="96c21-119">**CGI**</span></span><br>`CgiModule` | <span data-ttu-id="96c21-120">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-120">No</span></span> | 
<span data-ttu-id="96c21-121">**Validation de la configuration**</span><span class="sxs-lookup"><span data-stu-id="96c21-121">**Configuration Validation**</span></span><br>`ConfigurationValidationModule` | <span data-ttu-id="96c21-122">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-122">Yes</span></span> | 
<span data-ttu-id="96c21-123">**Erreurs HTTP**</span><span class="sxs-lookup"><span data-stu-id="96c21-123">**HTTP Errors**</span></span><br>`CustomErrorModule` | <span data-ttu-id="96c21-124">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-124">No</span></span> | [<span data-ttu-id="96c21-125">Intergiciel (middleware) Pages de Code état</span><span class="sxs-lookup"><span data-stu-id="96c21-125">Status Code Pages Middleware</span></span>](xref:fundamentals/error-handling#configuring-status-code-pages)
<span data-ttu-id="96c21-126">**Journalisation personnalisée**</span><span class="sxs-lookup"><span data-stu-id="96c21-126">**Custom Logging**</span></span><br>`CustomLoggingModule` | <span data-ttu-id="96c21-127">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-127">Yes</span></span> | 
<span data-ttu-id="96c21-128">**Document par défaut**</span><span class="sxs-lookup"><span data-stu-id="96c21-128">**Default Document**</span></span><br>`DefaultDocumentModule` | <span data-ttu-id="96c21-129">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-129">No</span></span> | [<span data-ttu-id="96c21-130">Intergiciel de fichiers par défaut</span><span class="sxs-lookup"><span data-stu-id="96c21-130">Default Files Middleware</span></span>](xref:fundamentals/static-files#serving-a-default-document)
<span data-ttu-id="96c21-131">**Authentification Digest**</span><span class="sxs-lookup"><span data-stu-id="96c21-131">**Digest Authentication**</span></span><br>`DigestAuthenticationModule` | <span data-ttu-id="96c21-132">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-132">Yes</span></span> | 
<span data-ttu-id="96c21-133">**Exploration des répertoires**</span><span class="sxs-lookup"><span data-stu-id="96c21-133">**Directory Browsing**</span></span><br>`DirectoryListingModule` | <span data-ttu-id="96c21-134">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-134">No</span></span> | [<span data-ttu-id="96c21-135">Intergiciel (middleware) exploration de répertoire</span><span class="sxs-lookup"><span data-stu-id="96c21-135">Directory Browsing Middleware</span></span>](xref:fundamentals/static-files#enabling-directory-browsing)
<span data-ttu-id="96c21-136">**Compression dynamique**</span><span class="sxs-lookup"><span data-stu-id="96c21-136">**Dynamic Compression**</span></span><br>`DynamicCompressionModule` | <span data-ttu-id="96c21-137">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-137">Yes</span></span> | [<span data-ttu-id="96c21-138">Intergiciel (middleware) de compression des réponses</span><span class="sxs-lookup"><span data-stu-id="96c21-138">Response Compression Middleware</span></span>](xref:performance/response-compression)
<span data-ttu-id="96c21-139">**Suivi**</span><span class="sxs-lookup"><span data-stu-id="96c21-139">**Tracing**</span></span><br>`FailedRequestsTracingModule` | <span data-ttu-id="96c21-140">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-140">Yes</span></span> | [<span data-ttu-id="96c21-141">Enregistrement d’ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="96c21-141">ASP.NET Core Logging</span></span>](xref:fundamentals/logging/index#the-tracesource-provider)
<span data-ttu-id="96c21-142">**La mise en cache du fichier**</span><span class="sxs-lookup"><span data-stu-id="96c21-142">**File Caching**</span></span><br>`FileCacheModule` | <span data-ttu-id="96c21-143">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-143">No</span></span> | [<span data-ttu-id="96c21-144">Intergiciel de mise en cache des réponses</span><span class="sxs-lookup"><span data-stu-id="96c21-144">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="96c21-145">**Mise en cache HTTP**</span><span class="sxs-lookup"><span data-stu-id="96c21-145">**HTTP Caching**</span></span><br>`HttpCacheModule` | <span data-ttu-id="96c21-146">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-146">No</span></span> | [<span data-ttu-id="96c21-147">Intergiciel de mise en cache des réponses</span><span class="sxs-lookup"><span data-stu-id="96c21-147">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="96c21-148">**Journalisation HTTP**</span><span class="sxs-lookup"><span data-stu-id="96c21-148">**HTTP Logging**</span></span><br>`HttpLoggingModule` | <span data-ttu-id="96c21-149">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-149">Yes</span></span> | [<span data-ttu-id="96c21-150">Enregistrement d’ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="96c21-150">ASP.NET Core Logging</span></span>](xref:fundamentals/logging/index)<br><span data-ttu-id="96c21-151">Implémentations : [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging), [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging), [NLog](https://github.com/NLog/NLog.Extensions.Logging), [Serilog](https://github.com/serilog/serilog-extensions-logging)</span><span class="sxs-lookup"><span data-stu-id="96c21-151">Implementations: [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging), [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging), [NLog](https://github.com/NLog/NLog.Extensions.Logging), [Serilog](https://github.com/serilog/serilog-extensions-logging)</span></span>
<span data-ttu-id="96c21-152">**Redirection HTTP**</span><span class="sxs-lookup"><span data-stu-id="96c21-152">**HTTP Redirection**</span></span><br>`HttpRedirectionModule` | <span data-ttu-id="96c21-153">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-153">Yes</span></span> | [<span data-ttu-id="96c21-154">Intergiciel de réécriture d’URL</span><span class="sxs-lookup"><span data-stu-id="96c21-154">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="96c21-155">**Authentification par mappage de certificat Client IIS**</span><span class="sxs-lookup"><span data-stu-id="96c21-155">**IIS Client Certificate Mapping Authentication**</span></span><br>`IISCertificateMappingAuthenticationModule` | <span data-ttu-id="96c21-156">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-156">Yes</span></span> | 
<span data-ttu-id="96c21-157">**Restrictions IP et de domaine**</span><span class="sxs-lookup"><span data-stu-id="96c21-157">**IP and Domain Restrictions**</span></span><br>`IpRestrictionModule` | <span data-ttu-id="96c21-158">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-158">Yes</span></span> | 
<span data-ttu-id="96c21-159">**Filtres ISAPI**</span><span class="sxs-lookup"><span data-stu-id="96c21-159">**ISAPI Filters**</span></span><br>`IsapiFilterModule` | <span data-ttu-id="96c21-160">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-160">Yes</span></span> | [<span data-ttu-id="96c21-161">Intergiciel (middleware)</span><span class="sxs-lookup"><span data-stu-id="96c21-161">Middleware</span></span>](xref:fundamentals/middleware)
<span data-ttu-id="96c21-162">**ISAPI**</span><span class="sxs-lookup"><span data-stu-id="96c21-162">**ISAPI**</span></span><br>`IsapiModule` | <span data-ttu-id="96c21-163">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-163">Yes</span></span> | [<span data-ttu-id="96c21-164">Intergiciel (middleware)</span><span class="sxs-lookup"><span data-stu-id="96c21-164">Middleware</span></span>](xref:fundamentals/middleware)
<span data-ttu-id="96c21-165">**Prise en charge du protocole**</span><span class="sxs-lookup"><span data-stu-id="96c21-165">**Protocol Support**</span></span><br>`ProtocolSupportModule` | <span data-ttu-id="96c21-166">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-166">Yes</span></span> | 
<span data-ttu-id="96c21-167">**Filtrage des demandes**</span><span class="sxs-lookup"><span data-stu-id="96c21-167">**Request Filtering**</span></span><br>`RequestFilteringModule` | <span data-ttu-id="96c21-168">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-168">Yes</span></span> | [<span data-ttu-id="96c21-169">Intergiciel (middleware) réécriture d’URL`IRule`</span><span class="sxs-lookup"><span data-stu-id="96c21-169">URL Rewriting Middleware `IRule`</span></span>](xref:fundamentals/url-rewriting#irule-based-rule)
<span data-ttu-id="96c21-170">**Observateur de demandes**</span><span class="sxs-lookup"><span data-stu-id="96c21-170">**Request Monitor**</span></span><br>`RequestMonitorModule` | <span data-ttu-id="96c21-171">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-171">Yes</span></span> | 
<span data-ttu-id="96c21-172">**Réécriture d’URL**</span><span class="sxs-lookup"><span data-stu-id="96c21-172">**URL Rewriting**</span></span><br>`RewriteModule` | <span data-ttu-id="96c21-173">Yes†</span><span class="sxs-lookup"><span data-stu-id="96c21-173">Yes†</span></span> | [<span data-ttu-id="96c21-174">Intergiciel de réécriture d’URL</span><span class="sxs-lookup"><span data-stu-id="96c21-174">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="96c21-175">**Fichiers Include côté serveur**</span><span class="sxs-lookup"><span data-stu-id="96c21-175">**Server Side Includes**</span></span><br>`ServerSideIncludeModule` | <span data-ttu-id="96c21-176">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-176">No</span></span> | 
<span data-ttu-id="96c21-177">**Compression statique**</span><span class="sxs-lookup"><span data-stu-id="96c21-177">**Static Compression**</span></span><br>`StaticCompressionModule` | <span data-ttu-id="96c21-178">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-178">No</span></span> | [<span data-ttu-id="96c21-179">Intergiciel (middleware) de compression des réponses</span><span class="sxs-lookup"><span data-stu-id="96c21-179">Response Compression Middleware</span></span>](xref:performance/response-compression)
<span data-ttu-id="96c21-180">**Contenu statique**</span><span class="sxs-lookup"><span data-stu-id="96c21-180">**Static Content**</span></span><br>`StaticFileModule` | <span data-ttu-id="96c21-181">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-181">No</span></span> | [<span data-ttu-id="96c21-182">Intergiciel (middleware) de fichiers statiques</span><span class="sxs-lookup"><span data-stu-id="96c21-182">Static File Middleware</span></span>](xref:fundamentals/static-files)
<span data-ttu-id="96c21-183">**Mise en cache de jeton**</span><span class="sxs-lookup"><span data-stu-id="96c21-183">**Token Caching**</span></span><br>`TokenCacheModule` | <span data-ttu-id="96c21-184">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-184">Yes</span></span> | 
<span data-ttu-id="96c21-185">**La mise en cache URI**</span><span class="sxs-lookup"><span data-stu-id="96c21-185">**URI Caching**</span></span><br>`UriCacheModule` | <span data-ttu-id="96c21-186">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-186">Yes</span></span> | 
<span data-ttu-id="96c21-187">**Autorisation URL**</span><span class="sxs-lookup"><span data-stu-id="96c21-187">**URL Authorization**</span></span><br>`UrlAuthorizationModule` | <span data-ttu-id="96c21-188">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-188">Yes</span></span> | [<span data-ttu-id="96c21-189">Identité de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="96c21-189">ASP.NET Core Identity</span></span>](xref:security/authentication/identity)
<span data-ttu-id="96c21-190">**Authentification Windows**</span><span class="sxs-lookup"><span data-stu-id="96c21-190">**Windows Authentication**</span></span><br>`WindowsAuthenticationModule` | <span data-ttu-id="96c21-191">Oui</span><span class="sxs-lookup"><span data-stu-id="96c21-191">Yes</span></span> | 

<span data-ttu-id="96c21-192">†The Module de réécriture d’URL `isFile` et `isDirectory` ne fonctionnent pas avec les applications ASP.NET Core en raison de modifications dans [structure de répertoires](xref:hosting/directory-structure).</span><span class="sxs-lookup"><span data-stu-id="96c21-192">†The URL Rewrite Module's `isFile` and `isDirectory` do not work with ASP.NET Core applications due to the changes in [directory structure](xref:hosting/directory-structure).</span></span>

## <a name="managed-modules"></a><span data-ttu-id="96c21-193">Modules managés</span><span class="sxs-lookup"><span data-stu-id="96c21-193">Managed Modules</span></span>
<span data-ttu-id="96c21-194">Module</span><span class="sxs-lookup"><span data-stu-id="96c21-194">Module</span></span> | <span data-ttu-id="96c21-195">.NET core actif</span><span class="sxs-lookup"><span data-stu-id="96c21-195">.NET Core Active</span></span> | <span data-ttu-id="96c21-196">Option ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="96c21-196">ASP.NET Core Option</span></span>
--- | :---: | ---
<span data-ttu-id="96c21-197">AnonymousIdentification</span><span class="sxs-lookup"><span data-stu-id="96c21-197">AnonymousIdentification</span></span> | <span data-ttu-id="96c21-198">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-198">No</span></span> | 
<span data-ttu-id="96c21-199">DefaultAuthentication</span><span class="sxs-lookup"><span data-stu-id="96c21-199">DefaultAuthentication</span></span> | <span data-ttu-id="96c21-200">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-200">No</span></span> | 
<span data-ttu-id="96c21-201">FileAuthorization</span><span class="sxs-lookup"><span data-stu-id="96c21-201">FileAuthorization</span></span> | <span data-ttu-id="96c21-202">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-202">No</span></span> | 
<span data-ttu-id="96c21-203">FormsAuthentication</span><span class="sxs-lookup"><span data-stu-id="96c21-203">FormsAuthentication</span></span> | <span data-ttu-id="96c21-204">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-204">No</span></span> | [<span data-ttu-id="96c21-205">Intergiciel (middleware) de cookie d’authentification</span><span class="sxs-lookup"><span data-stu-id="96c21-205">Cookie Authentication Middleware</span></span>](xref:security/authentication/cookie)
<span data-ttu-id="96c21-206">OutputCache</span><span class="sxs-lookup"><span data-stu-id="96c21-206">OutputCache</span></span> | <span data-ttu-id="96c21-207">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-207">No</span></span> | [<span data-ttu-id="96c21-208">Intergiciel de mise en cache des réponses</span><span class="sxs-lookup"><span data-stu-id="96c21-208">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="96c21-209">Profil</span><span class="sxs-lookup"><span data-stu-id="96c21-209">Profile</span></span> | <span data-ttu-id="96c21-210">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-210">No</span></span> | 
<span data-ttu-id="96c21-211">RoleManager</span><span class="sxs-lookup"><span data-stu-id="96c21-211">RoleManager</span></span> | <span data-ttu-id="96c21-212">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-212">No</span></span> | 
<span data-ttu-id="96c21-213">ScriptModule-4.0</span><span class="sxs-lookup"><span data-stu-id="96c21-213">ScriptModule-4.0</span></span> | <span data-ttu-id="96c21-214">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-214">No</span></span> | 
<span data-ttu-id="96c21-215">Session</span><span class="sxs-lookup"><span data-stu-id="96c21-215">Session</span></span> | <span data-ttu-id="96c21-216">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-216">No</span></span> | [<span data-ttu-id="96c21-217">Intergiciel (middleware) de session</span><span class="sxs-lookup"><span data-stu-id="96c21-217">Session Middleware</span></span>](xref:fundamentals/app-state)
<span data-ttu-id="96c21-218">UrlAuthorization</span><span class="sxs-lookup"><span data-stu-id="96c21-218">UrlAuthorization</span></span> | <span data-ttu-id="96c21-219">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-219">No</span></span> | 
<span data-ttu-id="96c21-220">UrlMappingsModule</span><span class="sxs-lookup"><span data-stu-id="96c21-220">UrlMappingsModule</span></span> | <span data-ttu-id="96c21-221">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-221">No</span></span> | [<span data-ttu-id="96c21-222">Intergiciel de réécriture d’URL</span><span class="sxs-lookup"><span data-stu-id="96c21-222">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="96c21-223">UrlRoutingModule-4.0</span><span class="sxs-lookup"><span data-stu-id="96c21-223">UrlRoutingModule-4.0</span></span> | <span data-ttu-id="96c21-224">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-224">No</span></span> | [<span data-ttu-id="96c21-225">Identité de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="96c21-225">ASP.NET Core  Identity</span></span>](xref:security/authentication/identity)
<span data-ttu-id="96c21-226">WindowsAuthentication</span><span class="sxs-lookup"><span data-stu-id="96c21-226">WindowsAuthentication</span></span> | <span data-ttu-id="96c21-227">Non</span><span class="sxs-lookup"><span data-stu-id="96c21-227">No</span></span> | 

## <a name="iis-manager-application-changes"></a><span data-ttu-id="96c21-228">Modification de l’application Gestionnaire des services Internet</span><span class="sxs-lookup"><span data-stu-id="96c21-228">IIS Manager application changes</span></span>
<span data-ttu-id="96c21-229">Lorsque vous utilisez le Gestionnaire des services Internet pour configurer les paramètres, vous modifiez directement le *web.config* fichier de l’application.</span><span class="sxs-lookup"><span data-stu-id="96c21-229">When you use IIS Manager to configure settings, you're directly changing the *web.config* file of the app.</span></span> <span data-ttu-id="96c21-230">Si vous déployez votre application et que vous incluez *web.config*, toutes les modifications apportées à IIS Manager seront remplacées par la version déployée *fichier web.config*.</span><span class="sxs-lookup"><span data-stu-id="96c21-230">If you deploy your app and include *web.config*, any changes you made with IIS Manger will be overwritten by the deployed *web.config file*.</span></span> <span data-ttu-id="96c21-231">Par conséquent, si vous apportez des modifications sur le serveur *web.config* de fichiers, copiez la mise à jour *web.config* fichier à votre projet local immédiatement.</span><span class="sxs-lookup"><span data-stu-id="96c21-231">Therefore if you make changes to the server's *web.config* file, copy the updated *web.config* file to your local project immediately.</span></span>

## <a name="disabling-iis-modules"></a><span data-ttu-id="96c21-232">La désactivation des modules IIS</span><span class="sxs-lookup"><span data-stu-id="96c21-232">Disabling IIS modules</span></span>
<span data-ttu-id="96c21-233">Si vous avez un module IIS configuré au niveau du serveur que vous voulez désactiver pour une application, vous pouvez le faire avec un ajout à votre *web.config* fichier.</span><span class="sxs-lookup"><span data-stu-id="96c21-233">If you have an IIS module configured at the server level that you would like to disable for an application, you can do so with an addition to your *web.config* file.</span></span> <span data-ttu-id="96c21-234">Conservez le module en place et désactiver à l’aide d’un paramètre de configuration (si disponible) ou supprimez le module de l’application.</span><span class="sxs-lookup"><span data-stu-id="96c21-234">Either leave the module in place and deactivate it using a configuration setting (if available) or remove the module from the app.</span></span>

### <a name="module-deactivation"></a><span data-ttu-id="96c21-235">Désactivation du module</span><span class="sxs-lookup"><span data-stu-id="96c21-235">Module deactivation</span></span>
<span data-ttu-id="96c21-236">Nombre de modules offre un paramètre de configuration qui vous permet de les désactiver sans les supprimer à partir de l’application.</span><span class="sxs-lookup"><span data-stu-id="96c21-236">Many modules offer a configuration setting that will allow you to disable them without removing them from the application.</span></span> <span data-ttu-id="96c21-237">Il s’agit de la façon la plus simple et plus rapide pour désactiver un module.</span><span class="sxs-lookup"><span data-stu-id="96c21-237">This is the simplest and quickest way to deactivate a module.</span></span> <span data-ttu-id="96c21-238">Par exemple, si vous souhaitez désactiver le Module de réécriture d’URL IIS, utilisez le `<httpRedirect>` comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="96c21-238">For example if you wish to disable the IIS URL Rewrite Module, use the `<httpRedirect>` element as shown below.</span></span> <span data-ttu-id="96c21-239">Pour plus d’informations sur la désactivation de modules avec les paramètres de configuration, suivez les liens dans le *des éléments enfants* section de [IIS `<system.webServer>` ](https://docs.microsoft.com/iis/configuration/system.webServer/).</span><span class="sxs-lookup"><span data-stu-id="96c21-239">For more information on disabling modules with configuration settings, follow the links in the *Child Elements* section of [IIS `<system.webServer>`](https://docs.microsoft.com/iis/configuration/system.webServer/).</span></span>

```xml
<configuration>
  <system.webServer>
     <httpRedirect enabled="false" />
  </system.webServer>
</configuration>
```

### <a name="module-removal"></a><span data-ttu-id="96c21-240">Retrait du module</span><span class="sxs-lookup"><span data-stu-id="96c21-240">Module removal</span></span>
<span data-ttu-id="96c21-241">Si vous optez pour supprimer un module avec un paramètre dans *web.config*, vous devez déverrouiller le module et déverrouiller le `<modules>` section de *web.config* première.</span><span class="sxs-lookup"><span data-stu-id="96c21-241">If you opt to remove a module with a setting in *web.config*, you must unlock the module and unlock the `<modules>` section of *web.config* first.</span></span> <span data-ttu-id="96c21-242">Les étapes sont décrites ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="96c21-242">The steps are outlined below:</span></span>

1. <span data-ttu-id="96c21-243">Déverrouiller le module au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="96c21-243">Unlock the module at the server level.</span></span> <span data-ttu-id="96c21-244">Cliquez sur le serveur IIS dans le Gestionnaire IIS **connexions** barre latérale.</span><span class="sxs-lookup"><span data-stu-id="96c21-244">Click on the IIS server in the IIS Manager **Connections** sidebar.</span></span> <span data-ttu-id="96c21-245">Ouvrez le **Modules** dans les **IIS** zone.</span><span class="sxs-lookup"><span data-stu-id="96c21-245">Open the **Modules** in the **IIS** area.</span></span> <span data-ttu-id="96c21-246">Cliquez sur le module dans la liste.</span><span class="sxs-lookup"><span data-stu-id="96c21-246">Click on the module in the list.</span></span> <span data-ttu-id="96c21-247">Dans le **Actions** encadré à droite, cliquez sur **Unlock**.</span><span class="sxs-lookup"><span data-stu-id="96c21-247">In the **Actions** sidebar on the right, click **Unlock**.</span></span> <span data-ttu-id="96c21-248">Déverrouiller autant de modules que vous souhaitez supprimer avec *web.config* plus tard.</span><span class="sxs-lookup"><span data-stu-id="96c21-248">Unlock as many modules as you plan to remove with *web.config* later.</span></span>

2. <span data-ttu-id="96c21-249">Déployer votre application sans un `<modules>` section *web.config*. Si vous déployez une application avec un *web.config* contenant le `<modules>` section sans avoir déverrouillé la section tout d’abord dans le Gestionnaire des services Internet, le Gestionnaire de Configuration lève une exception lorsque vous essayez de déverrouiller la section.</span><span class="sxs-lookup"><span data-stu-id="96c21-249">Deploy your application without a `<modules>` section in *web.config*. If you deploy an app with a *web.config* containing the `<modules>` section without having unlocked the section first in the IIS Manager, the Configuration Manager will throw an exception when you try to unlock the section.</span></span> <span data-ttu-id="96c21-250">Par conséquent, de déployer votre application sans un `<modules>` section.</span><span class="sxs-lookup"><span data-stu-id="96c21-250">Therefore, deploy your application without a `<modules>` section.</span></span>

3. <span data-ttu-id="96c21-251">Déverrouiller le `<modules>` section de *web.config*. Dans le **connexions** barre latérale, cliquez sur le site Web dans **Sites**.</span><span class="sxs-lookup"><span data-stu-id="96c21-251">Unlock the `<modules>` section of *web.config*. In the **Connections** sidebar, click the website in **Sites**.</span></span> <span data-ttu-id="96c21-252">Dans le **gestion** zone, ouvrez le **l’éditeur de Configuration**.</span><span class="sxs-lookup"><span data-stu-id="96c21-252">In the **Management** area, open the **Configuration Editor**.</span></span> <span data-ttu-id="96c21-253">Utilisez les contrôles de navigation pour sélectionner le `system.webServer/modules` section.</span><span class="sxs-lookup"><span data-stu-id="96c21-253">Use the navigation controls to select the `system.webServer/modules` section.</span></span> <span data-ttu-id="96c21-254">Dans le **Actions** encadré à droite, cliquez sur **Unlock** la section.</span><span class="sxs-lookup"><span data-stu-id="96c21-254">In the **Actions** sidebar on the right, click to **Unlock** the section.</span></span>

4. <span data-ttu-id="96c21-255">À ce stade, vous serez en mesure d’ajouter un `<modules>` section à votre *web.config* de fichiers avec un `<remove>` élément à supprimer le module de l’application.</span><span class="sxs-lookup"><span data-stu-id="96c21-255">At this point, you will be able to add a `<modules>` section to your *web.config* file with a `<remove>` element to remove the module from the application.</span></span> <span data-ttu-id="96c21-256">Vous pouvez ajouter plusieurs `<remove>` éléments à supprimer de plusieurs modules.</span><span class="sxs-lookup"><span data-stu-id="96c21-256">You can add multiple `<remove>` elements to remove multiple modules.</span></span> <span data-ttu-id="96c21-257">N’oubliez pas que si vous apportez *web.config* modifications sur le serveur pour les rendre immédiatement dans le projet localement.</span><span class="sxs-lookup"><span data-stu-id="96c21-257">Don't forget that if you make *web.config* changes on the server to make them immediately in the project locally.</span></span> <span data-ttu-id="96c21-258">Retrait d’un module de cette manière n’affecte pas votre utilisation du module avec d’autres applications sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="96c21-258">Removing a module this way won't affect your use of the module with other apps on the server.</span></span>

  ```xml
  <configuration> 
    <system.webServer> 
      <modules> 
        <remove name="MODULE_NAME" /> 
      </modules> 
    </system.webServer> 
  </configuration>
  ```

<span data-ttu-id="96c21-259">Pour une installation d’IIS avec les modules par défaut installé, vous pouvez utiliser les éléments suivants `<module>` section pour supprimer les modules par défaut.</span><span class="sxs-lookup"><span data-stu-id="96c21-259">For an IIS installation with the default modules installed, you can use the following `<module>` section to remove the default modules.</span></span>

```xml
<modules>
  <remove name="CustomErrorModule" />
  <remove name="DefaultDocumentModule" />
  <remove name="DirectoryListingModule" />
  <remove name="HttpCacheModule" />
  <remove name="HttpLoggingModule" />
  <remove name="ProtocolSupportModule" />
  <remove name="RequestFilteringModule" />
  <remove name="StaticCompressionModule" /> 
  <remove name="StaticFileModule" /> 
</modules>
```

<span data-ttu-id="96c21-260">Vous pouvez également supprimer un module IIS avec *Appcmd.exe*.</span><span class="sxs-lookup"><span data-stu-id="96c21-260">You can also remove an IIS module with *Appcmd.exe*.</span></span> <span data-ttu-id="96c21-261">Fournir le `MODULE_NAME` et `APPLICATION_NAME` dans la commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="96c21-261">Provide the `MODULE_NAME` and `APPLICATION_NAME` in the command shown below:</span></span>

```console
Appcmd.exe delete module MODULE_NAME /app.name:APPLICATION_NAME
```

<span data-ttu-id="96c21-262">Voici comment supprimer le `DynamicCompressionModule` à partir du Site Web par défaut :</span><span class="sxs-lookup"><span data-stu-id="96c21-262">Here's how to remove the `DynamicCompressionModule` from the Default Web Site:</span></span>

```console
%windir%\system32\inetsrv\appcmd.exe delete module DynamicCompressionModule /app.name:"Default Web Site"
```

## <a name="minimal-module-configuration"></a><span data-ttu-id="96c21-263">Configuration du module minimale</span><span class="sxs-lookup"><span data-stu-id="96c21-263">Minimal module configuration</span></span>
<span data-ttu-id="96c21-264">Les modules uniquement requis pour exécuter une application ASP.NET Core sont le Module d’authentification anonyme et le Module de base ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="96c21-264">The only modules required to run an ASP.NET Core application are the Anonymous Authentication Module and the ASP.NET Core Module.</span></span>

![Ouvrir le Gestionnaire des services Internet aux Modules avec la configuration de modules minimale indiquée](iis-modules/_static/modules.png)

## <a name="resources"></a><span data-ttu-id="96c21-266">Ressources</span><span class="sxs-lookup"><span data-stu-id="96c21-266">Resources</span></span>
* [<span data-ttu-id="96c21-267">Publication dans IIS</span><span class="sxs-lookup"><span data-stu-id="96c21-267">Publishing to IIS</span></span>](xref:publishing/iis)
* [<span data-ttu-id="96c21-268">Vue d’ensemble des Modules IIS</span><span class="sxs-lookup"><span data-stu-id="96c21-268">IIS Modules Overview</span></span>](https://docs.microsoft.com/iis/get-started/introduction-to-iis/iis-modules-overview)
* [<span data-ttu-id="96c21-269">Personnalisation de IIS 7.0 rôles et des Modules</span><span class="sxs-lookup"><span data-stu-id="96c21-269">Customizing IIS 7.0 Roles and Modules</span></span>](https://technet.microsoft.com/library/cc627313.aspx)
* [<span data-ttu-id="96c21-270">IIS`<system.webServer>`</span><span class="sxs-lookup"><span data-stu-id="96c21-270">IIS `<system.webServer>`</span></span>](https://docs.microsoft.com/iis/configuration/system.webServer/)