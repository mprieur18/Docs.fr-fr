---
title: Introduction à l’autorisation dans ASP.NET Core
author: rick-anderson
description: Découvrez les principes fondamentaux de l’autorisation et le fonctionnement des autorisations dans les applications ASP.NET Core.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/introduction
ms.openlocfilehash: 7ba1966dcaf1ce0510f489cfe0ff11501faffa56
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
---
# <a name="introduction-to-authorization-in-aspnet-core"></a>Introduction à l’autorisation dans ASP.NET Core

<a name="security-authorization-introduction"></a>

Le terme Autorisation désigne le processus qui détermine ce qu’un utilisateur est en mesure d’effectuer. Par exemple, un utilisateur administratif est autorisé à créer une bibliothèque de documents, ajoutez les documents, modifier des documents et les supprimer. Un utilisateur non-administrateur, utilisant la bibliothèque est uniquement autorisé à lire les documents.

L’autorisation est orthogonale et indépendante de l’authentification, qui est le processus d’évaluation de qui est l'utilisateur. L’authentification peut créer une ou plusieurs identités pour l’utilisateur actuel.

## <a name="authorization-types"></a>Types d’autorisation

L'autorisation de ASP.NET Core fournit un simple [rôle](xref:security/authorization/roles) déclaratif et un [modèle enrichie basée sur la stratégie](xref:security/authorization/policies). L’autorisation est exprimée dans les exigences et les gestionnaires évaluent les revendications d’un utilisateur par rapport aux exigences. Les vérifications impératives peuvent reposer sur des stratégies simples ou des stratégies qui évaluent l’identité de l’utilisateur et les propriétés de la ressource à laquelle l’utilisateur tente d’accéder.

## <a name="namespaces"></a>Espaces de noms

Les composants d’autorisation, y compris les attributs `AuthorizeAttribute` et `AllowAnonymousAttribute` se trouvent dans l'espace de noms `Microsoft.AspNetCore.Authorization`.

Consultez la documentation sur [une autorisation simple](xref:security/authorization/simple).
