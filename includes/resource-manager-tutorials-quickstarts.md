---
title: Fichier Include
description: Fichier Include
services: azure-resource-manager
documentationcenter: ''
author: mumian
manager: dougeby
editor: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 01/15/2019
ms.author: jgao
ms.custom: include file
ms.openlocfilehash: 11bcfa1b4719d6def5bfc4a6a189bd2b58896b5b
ms.sourcegitcommit: dede0c5cbb2bd975349b6286c48456cfd270d6e9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54334355"
---
## <a name="quickstarts-and-tutorials"></a>Guides de démarrages rapides et tutoriels

Utilisez les guides de démarrage rapide et les didacticiels suivants pour apprendre comment développer des modèles Resource Manager :

- Démarrages rapides

    |Intitulé|Description|
    |------|-----|
    |[Utiliser le portail Azure](../articles/azure-resource-manager/resource-manager-quickstart-create-templates-use-the-portal.md)|Générez un modèle à l’aide du portail et comprenez le processus de modification et de déploiement du modèle.|
    |[Utiliser Visual Studio Code](../articles/azure-resource-manager/resource-manager-quickstart-create-templates-use-visual-studio-code.md)|Utilisez Visual Studio Code pour créer et modifier les modèles et comment utiliser Azure Cloud Shell pour déployer des modèles.|
    |[Utiliser Visual Studio](../articles/azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)|Utilisez Visual Studio pour créer, modifier et déployer des modèles.|

- Didacticiels

    |Intitulé|Description|
    |------|-----|
    |[Utiliser la référence de modèle](../articles/azure-resource-manager/resource-manager-tutorial-create-encrypted-storage-accounts.md)|Utilisez la documentation de référence du modèle pour développer des modèles. Dans ce didacticiel, trouvez le schéma de compte de stockage et utilisez ces informations pour créer un compte de stockage chiffré.|
    |[Créer plusieurs instances](../articles/azure-resource-manager/resource-manager-tutorial-create-multiple-instances.md)|Créez plusieurs instances de ressources Azure. Dans ce didacticiel, vous créez plusieurs instances de compte de stockage.|
    |[Déplacer des ressources](../articles/azure-resource-manager/resource-manager-tutorial-move-resources.md)|Déplacez des ressources d’un groupe de ressources vers un autre groupe de ressources. Dans le didacticiel, vous exécutez un modèle pour créer deux groupes de ressources et un compte de stockage, puis exécutez un cmdlet Azure PowerShell pour déplacer le compte de stockage vers l’autre groupe de ressources.|
    |[Définir l’ordre de déploiement des ressources](../articles/azure-resource-manager/resource-manager-tutorial-create-templates-with-dependent-resources.md)|Définir les dépendances des ressources. Dans ce didacticiel, vous créez un réseau virtuel, une machine virtuelle et les ressources Azure dépendantes. Vous découvrez comment les dépendances sont définies.|
    |[Utiliser des conditions](../articles/azure-resource-manager/resource-manager-tutorial-use-conditions.md)|Déployer des ressources basées sur certaines valeurs de paramètres. Dans ce didacticiel, vous définissez un modèle pour créer un nouveau compte de stockage ou utilisez un compte de stockage existant basé sur la valeur d’un paramètre.|
    |[Intégrer Key Vault](../articles/azure-resource-manager/resource-manager-tutorial-use-key-vault.md)|Récupérer des données secrètes/mots de passe depuis Azure Key Vault. Dans ce didacticiel, vous créez une machine virtuelle.  Le mot de passe d’administrateur de la machine virtuelle est récupéré depuis un Key Vault.|
    |[Créer des modèles liés](../articles/azure-resource-manager/resource-manager-tutorial-create-linked-templates.md)|Modulariser des modèles et appeler d’autres modèles depuis un modèle. Dans ce didacticiel, vous créez un réseau virtuel, une machine virtuelle et les ressources dépendantes.  Le compte de stockage dépendant est défini dans un modèle lié. |
    |[Déployer des extensions de machine virtuelle](../articles/azure-resource-manager/resource-manager-tutorial-deploy-vm-extensions.md)|Effectuez les tâches de post-déploiement à l’aide des extensions. Dans le tutoriel, vous déployez une extension de script client pour installer le serveur web sur la machine virtuelle. |
    |[Déployer des extensions SQL](../articles/azure-resource-manager/resource-manager-tutorial-deploy-sql-extensions-bacpac.md)|Effectuez les tâches de post-déploiement à l’aide des extensions. Dans le tutoriel, vous déployez une extension de script client pour installer le serveur web sur la machine virtuelle. |
    |[Sécuriser des artefacts](../articles/azure-resource-manager/resource-manager-tutorial-secure-artifacts.md)|Sécurisez les artefacts nécessaires pour effectuer les déploiements. Ce tutoriel explique comment sécuriser l’artefact utilisé dans le tutoriel Déployer des extensions SQL. |
    |[Utiliser des pratiques de déploiement sécurisé](../articles/azure-resource-manager/deployment-manager-tutorial.md)|Utiliser Azure Deployment Manager. |
    |[Tutoriel : Résoudre les problèmes liés aux déploiements de modèles Resource Manager](../articles/azure-resource-manager/resource-manager-tutorial-troubleshoot.md)|Résoudre les problèmes de déploiement de modèles.|

Ces tutoriels peuvent être utilisés individuellement ou en tant que série pour en savoir plus les principaux concepts de développement de modèle Resource Manager.