---
title: "Règle de Protection des données à l’échelle de l’ordinateur prend en charge dans ASP.NET Core"
author: rick-anderson
description: "En savoir plus sur la prise en charge pour la définition d’une stratégie d’ordinateur à l’échelle par défaut pour toutes les applications qui utilisent la Protection des données ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/configuration/machine-wide-policy
ms.openlocfilehash: 4c3ae3b628ebe17c7926c71f1fad664d719d1706
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="data-protection-machine-wide-policy-support-in-aspnet-core"></a><span data-ttu-id="ab06c-103">Règle de Protection des données à l’échelle de l’ordinateur prend en charge dans ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ab06c-103">Data Protection machine-wide policy support in ASP.NET Core</span></span>

<span data-ttu-id="ab06c-104">Par [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ab06c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ab06c-105">Lors de l’exécution sur Windows, le système de Protection des données prend en charge limitée pour la définition d’une stratégie d’ordinateur à l’échelle par défaut pour toutes les applications qui utilisent la Protection des données ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ab06c-105">When running on Windows, the Data Protection system has limited support for setting a default machine-wide policy for all apps that consume ASP.NET Core Data Protection.</span></span> <span data-ttu-id="ab06c-106">L’idée générale est qu’un administrateur peut souhaiter de modifier un paramètre par défaut, tels que les algorithmes utilisés ou la durée de vie, sans avoir besoin de mettre à jour manuellement chaque application sur l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ab06c-106">The general idea is that an administrator might wish to change a default setting, such as the algorithms used or key lifetime, without the need to manually update every app on the machine.</span></span>

> [!WARNING]
> <span data-ttu-id="ab06c-107">L’administrateur système peut définir la stratégie par défaut, mais ils ne peuvent pas l’appliquer.</span><span class="sxs-lookup"><span data-stu-id="ab06c-107">The system administrator can set default policy, but they can't enforce it.</span></span> <span data-ttu-id="ab06c-108">Le développeur d’application peut toujours remplacer n’importe quelle valeur avec l’un de leurs propres choix.</span><span class="sxs-lookup"><span data-stu-id="ab06c-108">The app developer can always override any value with one of their own choosing.</span></span> <span data-ttu-id="ab06c-109">La stratégie par défaut affecte uniquement les applications où le développeur n’a pas encore spécifié une valeur explicite pour un paramètre.</span><span class="sxs-lookup"><span data-stu-id="ab06c-109">The default policy only affects apps where the developer hasn't specified an explicit value for a setting.</span></span>

## <a name="setting-default-policy"></a><span data-ttu-id="ab06c-110">Définition de la stratégie par défaut</span><span class="sxs-lookup"><span data-stu-id="ab06c-110">Setting default policy</span></span>

<span data-ttu-id="ab06c-111">Pour définir la stratégie par défaut, un administrateur peut définir les valeurs connues dans le Registre système sous la clé de Registre suivante :</span><span class="sxs-lookup"><span data-stu-id="ab06c-111">To set default policy, an administrator can set known values in the system registry under the following registry key:</span></span>

<span data-ttu-id="ab06c-112">**HKLM\SOFTWARE\Microsoft\DotNetPackages\Microsoft.AspNetCore.DataProtection**</span><span class="sxs-lookup"><span data-stu-id="ab06c-112">**HKLM\SOFTWARE\Microsoft\DotNetPackages\Microsoft.AspNetCore.DataProtection**</span></span>

<span data-ttu-id="ab06c-113">Si vous êtes sur un système d’exploitation de 64 bits et que vous souhaitez affecter le comportement des applications 32 bits, n’oubliez pas de configurer l’équivalent Wow6432Node de la clé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ab06c-113">If you're on a 64-bit operating system and want to affect the behavior of 32-bit apps, remember to configure the Wow6432Node equivalent of the above key.</span></span>

<span data-ttu-id="ab06c-114">Les valeurs prises en charge sont indiquées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ab06c-114">The supported values are shown below.</span></span>

| <span data-ttu-id="ab06c-115">Value</span><span class="sxs-lookup"><span data-stu-id="ab06c-115">Value</span></span>              | <span data-ttu-id="ab06c-116">Type</span><span class="sxs-lookup"><span data-stu-id="ab06c-116">Type</span></span>   | <span data-ttu-id="ab06c-117">Description</span><span class="sxs-lookup"><span data-stu-id="ab06c-117">Description</span></span> |
| ------------------ | :----: | ----------- |
| <span data-ttu-id="ab06c-118">EncryptionType</span><span class="sxs-lookup"><span data-stu-id="ab06c-118">EncryptionType</span></span>     | <span data-ttu-id="ab06c-119">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-119">string</span></span> | <span data-ttu-id="ab06c-120">Spécifie les algorithmes qui doivent être utilisés pour la protection des données.</span><span class="sxs-lookup"><span data-stu-id="ab06c-120">Specifies which algorithms should be used for data protection.</span></span> <span data-ttu-id="ab06c-121">La valeur doit être CNG-CBC, GCM-CNG ou géré et est décrite plus en détail ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ab06c-121">The value must be CNG-CBC, CNG-GCM, or Managed and is described in more detail below.</span></span> |
| <span data-ttu-id="ab06c-122">DefaultKeyLifetime</span><span class="sxs-lookup"><span data-stu-id="ab06c-122">DefaultKeyLifetime</span></span> | <span data-ttu-id="ab06c-123">DWORD</span><span class="sxs-lookup"><span data-stu-id="ab06c-123">DWORD</span></span>  | <span data-ttu-id="ab06c-124">Spécifie la durée de vie des clés qui vient d’être générées.</span><span class="sxs-lookup"><span data-stu-id="ab06c-124">Specifies the lifetime for newly-generated keys.</span></span> <span data-ttu-id="ab06c-125">La valeur est spécifiée en jours et doit être > = 7.</span><span class="sxs-lookup"><span data-stu-id="ab06c-125">The value is specified in days and must be >= 7.</span></span> |
| <span data-ttu-id="ab06c-126">KeyEscrowSinks</span><span class="sxs-lookup"><span data-stu-id="ab06c-126">KeyEscrowSinks</span></span>     | <span data-ttu-id="ab06c-127">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-127">string</span></span> | <span data-ttu-id="ab06c-128">Spécifie les types qui sont utilisés pour le dépôt de clé.</span><span class="sxs-lookup"><span data-stu-id="ab06c-128">Specifies the types that are used for key escrow.</span></span> <span data-ttu-id="ab06c-129">La valeur est une liste délimitée par des points-virgules de récepteurs de clé (Key escrow), où chaque élément dans la liste est le nom qualifié d’assembly d’un type qui implémente [IKeyEscrowSink](/dotnet/api/microsoft.aspnetcore.dataprotection.keymanagement.ikeyescrowsink).</span><span class="sxs-lookup"><span data-stu-id="ab06c-129">The value is a semicolon-delimited list of key escrow sinks, where each element in the list is the assembly-qualified name of a type that implements [IKeyEscrowSink](/dotnet/api/microsoft.aspnetcore.dataprotection.keymanagement.ikeyescrowsink).</span></span> |

## <a name="encryption-types"></a><span data-ttu-id="ab06c-130">Types de chiffrement</span><span class="sxs-lookup"><span data-stu-id="ab06c-130">Encryption types</span></span>

<span data-ttu-id="ab06c-131">Si EncryptionType est CNG-CBC, le système est configuré pour utiliser un chiffrement par blocs symétrique en mode CBC à la confidentialité et HMAC authenticité avec les services fournis par CNG de Windows (voir [spécifiant les algorithmes CNG de Windows personnalisés](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) pour plus de détails.)</span><span class="sxs-lookup"><span data-stu-id="ab06c-131">If EncryptionType is CNG-CBC, the system is configured to use a CBC-mode symmetric block cipher for confidentiality and HMAC for authenticity with services provided by Windows CNG (see [Specifying custom Windows CNG algorithms](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) for more details).</span></span> <span data-ttu-id="ab06c-132">Les valeurs supplémentaires suivantes sont prises en charge, chacune d’elles correspondant à une propriété sur le type CngCbcAuthenticatedEncryptionSettings.</span><span class="sxs-lookup"><span data-stu-id="ab06c-132">The following additional values are supported, each of which corresponds to a property on the CngCbcAuthenticatedEncryptionSettings type.</span></span>

| <span data-ttu-id="ab06c-133">Value</span><span class="sxs-lookup"><span data-stu-id="ab06c-133">Value</span></span>                       | <span data-ttu-id="ab06c-134">Type</span><span class="sxs-lookup"><span data-stu-id="ab06c-134">Type</span></span>   | <span data-ttu-id="ab06c-135">Description</span><span class="sxs-lookup"><span data-stu-id="ab06c-135">Description</span></span> |
| --------------------------- | :----: | ----------- |
| <span data-ttu-id="ab06c-136">EncryptionAlgorithm</span><span class="sxs-lookup"><span data-stu-id="ab06c-136">EncryptionAlgorithm</span></span>         | <span data-ttu-id="ab06c-137">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-137">string</span></span> | <span data-ttu-id="ab06c-138">Le nom d’un algorithme de chiffrement symétrique compris par CNG.</span><span class="sxs-lookup"><span data-stu-id="ab06c-138">The name of a symmetric block cipher algorithm understood by CNG.</span></span> <span data-ttu-id="ab06c-139">Cet algorithme est ouvert en mode CBC.</span><span class="sxs-lookup"><span data-stu-id="ab06c-139">This algorithm is opened in CBC mode.</span></span> |
| <span data-ttu-id="ab06c-140">EncryptionAlgorithmProvider</span><span class="sxs-lookup"><span data-stu-id="ab06c-140">EncryptionAlgorithmProvider</span></span> | <span data-ttu-id="ab06c-141">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-141">string</span></span> | <span data-ttu-id="ab06c-142">Le nom de l’implémentation du fournisseur CNG qui permet de créer l’algorithme EncryptionAlgorithm.</span><span class="sxs-lookup"><span data-stu-id="ab06c-142">The name of the CNG provider implementation that can produce the algorithm EncryptionAlgorithm.</span></span> |
| <span data-ttu-id="ab06c-143">EncryptionAlgorithmKeySize</span><span class="sxs-lookup"><span data-stu-id="ab06c-143">EncryptionAlgorithmKeySize</span></span>  | <span data-ttu-id="ab06c-144">DWORD</span><span class="sxs-lookup"><span data-stu-id="ab06c-144">DWORD</span></span>  | <span data-ttu-id="ab06c-145">La longueur (en bits) de la clé à dériver pour l’algorithme de chiffrement symétrique.</span><span class="sxs-lookup"><span data-stu-id="ab06c-145">The length (in bits) of the key to derive for the symmetric block cipher algorithm.</span></span> |
| <span data-ttu-id="ab06c-146">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="ab06c-146">HashAlgorithm</span></span>               | <span data-ttu-id="ab06c-147">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-147">string</span></span> | <span data-ttu-id="ab06c-148">Le nom d’un algorithme de hachage compris par CNG.</span><span class="sxs-lookup"><span data-stu-id="ab06c-148">The name of a hash algorithm understood by CNG.</span></span> <span data-ttu-id="ab06c-149">Cet algorithme est ouvert en mode HMAC.</span><span class="sxs-lookup"><span data-stu-id="ab06c-149">This algorithm is opened in HMAC mode.</span></span> |
| <span data-ttu-id="ab06c-150">HashAlgorithmProvider</span><span class="sxs-lookup"><span data-stu-id="ab06c-150">HashAlgorithmProvider</span></span>       | <span data-ttu-id="ab06c-151">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-151">string</span></span> | <span data-ttu-id="ab06c-152">Le nom de l’implémentation du fournisseur CNG qui permet de créer l’algorithme HashAlgorithm.</span><span class="sxs-lookup"><span data-stu-id="ab06c-152">The name of the CNG provider implementation that can produce the algorithm HashAlgorithm.</span></span> |

<span data-ttu-id="ab06c-153">Si EncryptionType est CNG-GCM, le système est configuré pour utiliser un chiffrement par blocs symétrique Mode Galois/compteur pour la confidentialité et l’authenticité avec les services fournis par CNG de Windows (voir [spécifiant les algorithmes CNG de Windows personnalisés](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) Pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="ab06c-153">If EncryptionType is CNG-GCM, the system is configured to use a Galois/Counter Mode symmetric block cipher for confidentiality and authenticity with services provided by Windows CNG (see [Specifying custom Windows CNG algorithms](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) for more details).</span></span> <span data-ttu-id="ab06c-154">Les valeurs supplémentaires suivantes sont prises en charge, chacune d’elles correspondant à une propriété sur le type CngGcmAuthenticatedEncryptionSettings.</span><span class="sxs-lookup"><span data-stu-id="ab06c-154">The following additional values are supported, each of which corresponds to a property on the CngGcmAuthenticatedEncryptionSettings type.</span></span>

| <span data-ttu-id="ab06c-155">Value</span><span class="sxs-lookup"><span data-stu-id="ab06c-155">Value</span></span>                       | <span data-ttu-id="ab06c-156">Type</span><span class="sxs-lookup"><span data-stu-id="ab06c-156">Type</span></span>   | <span data-ttu-id="ab06c-157">Description</span><span class="sxs-lookup"><span data-stu-id="ab06c-157">Description</span></span> |
| --------------------------- | :----: | ----------- |
| <span data-ttu-id="ab06c-158">EncryptionAlgorithm</span><span class="sxs-lookup"><span data-stu-id="ab06c-158">EncryptionAlgorithm</span></span>         | <span data-ttu-id="ab06c-159">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-159">string</span></span> | <span data-ttu-id="ab06c-160">Le nom d’un algorithme de chiffrement symétrique compris par CNG.</span><span class="sxs-lookup"><span data-stu-id="ab06c-160">The name of a symmetric block cipher algorithm understood by CNG.</span></span> <span data-ttu-id="ab06c-161">Cet algorithme est ouvert en Mode de compteur/Galois.</span><span class="sxs-lookup"><span data-stu-id="ab06c-161">This algorithm is opened in Galois/Counter Mode.</span></span> |
| <span data-ttu-id="ab06c-162">EncryptionAlgorithmProvider</span><span class="sxs-lookup"><span data-stu-id="ab06c-162">EncryptionAlgorithmProvider</span></span> | <span data-ttu-id="ab06c-163">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-163">string</span></span> | <span data-ttu-id="ab06c-164">Le nom de l’implémentation du fournisseur CNG qui permet de créer l’algorithme EncryptionAlgorithm.</span><span class="sxs-lookup"><span data-stu-id="ab06c-164">The name of the CNG provider implementation that can produce the algorithm EncryptionAlgorithm.</span></span> |
| <span data-ttu-id="ab06c-165">EncryptionAlgorithmKeySize</span><span class="sxs-lookup"><span data-stu-id="ab06c-165">EncryptionAlgorithmKeySize</span></span>  | <span data-ttu-id="ab06c-166">DWORD</span><span class="sxs-lookup"><span data-stu-id="ab06c-166">DWORD</span></span>  | <span data-ttu-id="ab06c-167">La longueur (en bits) de la clé à dériver pour l’algorithme de chiffrement symétrique.</span><span class="sxs-lookup"><span data-stu-id="ab06c-167">The length (in bits) of the key to derive for the symmetric block cipher algorithm.</span></span> |

<span data-ttu-id="ab06c-168">Si EncryptionType est géré, le système est configuré pour utiliser un SymmetricAlgorithm managé pour la confidentialité et KeyedHashAlgorithm authenticité (voir [spécification personnalisé géré algorithmes](xref:security/data-protection/configuration/overview#specifying-custom-managed-algorithms) pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="ab06c-168">If EncryptionType is Managed, the system is configured to use a managed SymmetricAlgorithm for confidentiality and KeyedHashAlgorithm for authenticity (see [Specifying custom managed algorithms](xref:security/data-protection/configuration/overview#specifying-custom-managed-algorithms) for more details).</span></span> <span data-ttu-id="ab06c-169">Les valeurs supplémentaires suivantes sont prises en charge, chacune d’elles correspondant à une propriété sur le type ManagedAuthenticatedEncryptionSettings.</span><span class="sxs-lookup"><span data-stu-id="ab06c-169">The following additional values are supported, each of which corresponds to a property on the ManagedAuthenticatedEncryptionSettings type.</span></span>

| <span data-ttu-id="ab06c-170">Value</span><span class="sxs-lookup"><span data-stu-id="ab06c-170">Value</span></span>                      | <span data-ttu-id="ab06c-171">Type</span><span class="sxs-lookup"><span data-stu-id="ab06c-171">Type</span></span>   | <span data-ttu-id="ab06c-172">Description</span><span class="sxs-lookup"><span data-stu-id="ab06c-172">Description</span></span> |
| -------------------------- | :----: | ----------- |
| <span data-ttu-id="ab06c-173">EncryptionAlgorithmType</span><span class="sxs-lookup"><span data-stu-id="ab06c-173">EncryptionAlgorithmType</span></span>    | <span data-ttu-id="ab06c-174">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-174">string</span></span> | <span data-ttu-id="ab06c-175">Le nom qualifié d’assembly d’un type qui implémente SymmetricAlgorithm.</span><span class="sxs-lookup"><span data-stu-id="ab06c-175">The assembly-qualified name of a type that implements SymmetricAlgorithm.</span></span> |
| <span data-ttu-id="ab06c-176">EncryptionAlgorithmKeySize</span><span class="sxs-lookup"><span data-stu-id="ab06c-176">EncryptionAlgorithmKeySize</span></span> | <span data-ttu-id="ab06c-177">DWORD</span><span class="sxs-lookup"><span data-stu-id="ab06c-177">DWORD</span></span>  | <span data-ttu-id="ab06c-178">La longueur (en bits) de la clé à dériver pour l’algorithme de chiffrement symétrique.</span><span class="sxs-lookup"><span data-stu-id="ab06c-178">The length (in bits) of the key to derive for the symmetric encryption algorithm.</span></span> |
| <span data-ttu-id="ab06c-179">ValidationAlgorithmType</span><span class="sxs-lookup"><span data-stu-id="ab06c-179">ValidationAlgorithmType</span></span>    | <span data-ttu-id="ab06c-180">chaîne</span><span class="sxs-lookup"><span data-stu-id="ab06c-180">string</span></span> | <span data-ttu-id="ab06c-181">Le nom qualifié d’assembly d’un type qui implémente l’élément KeyedHashAlgorithm impossible.</span><span class="sxs-lookup"><span data-stu-id="ab06c-181">The assembly-qualified name of a type that implements KeyedHashAlgorithm.</span></span> |

<span data-ttu-id="ab06c-182">Si EncryptionType a toute autre valeur différente de null ou vide, le système de Protection de données lève une exception au démarrage.</span><span class="sxs-lookup"><span data-stu-id="ab06c-182">If EncryptionType has any other value other than null or empty, the Data Protection system throws an exception at startup.</span></span>

> [!WARNING]
> <span data-ttu-id="ab06c-183">Lorsque vous configurez un paramètre de stratégie par défaut qui implique des noms de type (EncryptionAlgorithmType, ValidationAlgorithmType, KeyEscrowSinks), les types doivent être disponibles pour l’application.</span><span class="sxs-lookup"><span data-stu-id="ab06c-183">When configuring a default policy setting that involves type names (EncryptionAlgorithmType, ValidationAlgorithmType, KeyEscrowSinks), the types must be available to the app.</span></span> <span data-ttu-id="ab06c-184">Cela signifie que pour les applications qui s’exécutent sur le CLR de bureau, les assemblys qui contiennent ces types doivent figurer dans le Global Assembly Cache (GAC).</span><span class="sxs-lookup"><span data-stu-id="ab06c-184">This means that for apps running on Desktop CLR, the assemblies that contain these types should be present in the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="ab06c-185">Pour les applications ASP.NET Core s’exécutant sur [.NET Core](https://www.microsoft.com/net/core), les packages qui contiennent ces types doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="ab06c-185">For ASP.NET Core apps running on [.NET Core](https://www.microsoft.com/net/core), the packages that contain these types should be installed.</span></span>