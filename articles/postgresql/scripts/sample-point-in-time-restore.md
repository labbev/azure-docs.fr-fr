---
title: 'Script Azure CLI : Restaurer un serveur Azure Database pour PostgreSQL'
description: Cet exemple de script Azure CLI montre comment restaurer un serveur Azure Database pour PostgreSQL et ses bases de données à un point antérieur dans le temps.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.devlang: azurecli
ms.topic: sample
ms.custom: mvc
ms.date: 02/28/2018
ms.openlocfilehash: 1f772f710f0146048fcde04d884fbe3458722743
ms.sourcegitcommit: 039263ff6271f318b471c4bf3dbc4b72659658ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55754521"
---
# <a name="restore-an-azure-database-for-postgresql-server-using-azure-cli"></a>Restaurer un serveur Azure Database pour PostgreSQL avec Azure CLI
Cet exemple de script Azure CLI permet de restaurer un seul serveur Azure Database pour PostgreSQL à un point antérieur dans le temps.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez d’exécuter l’interface CLI localement, Azure CLI 2.0 ou ultérieur est indispensable pour poursuivre la procédure décrite dans cet article. Pour vérifier la version, exécutez `az --version`. Consultez [Installer Azure CLI]( /cli/azure/install-azure-cli) pour installer ou mettre à niveau votre version d’Azure CLI.

## <a name="sample-script"></a>Exemple de script
Dans cet exemple de script, modifiez les lignes en surbrillance pour mettre à jour le nom d’utilisateur et le mot de passe d’administrateur et utiliser les vôtres. Remplacez l’ID d’abonnement utilisé dans les commandes `az monitor` par votre propre ID d’abonnement.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/backup-restore/backup-restore.sh?highlight=15-16 "Restore Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement
Utilisez la commande suivante pour supprimer le groupe de ressources et toutes les ressources associées après l’exécution du script. 
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/backup-restore/delete-postgresql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a>Explication du script
Ce script utilise les commandes décrites dans le tableau suivant :

| **Commande** | **Remarques** |
|---|---|
| [az group create](/cli/azure/group) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az postgresql server create](/cli/azure/postgres/server#az-postgres-server-create) | Crée un serveur PostgreSQL qui héberge les bases de données. |
| [az postgresql server restore](/cli/azure/postgres/server#az-postgres-server-restore) | Restaure un serveur à partir de la sauvegarde. |
| [az group delete](/cli/azure/group) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes
- Découvrez-en plus sur Azure CLI : [Documentation d’Azure CLI](/cli/azure).
- Essayez d’autres scripts : [Exemples Azure CLI pour base de données pour PostgreSQL](../sample-scripts-azure-cli.md)
- [Comment sauvegarder et restaurer un serveur Azure Database pour PostgreSQL à l’aide du portail Azure](../howto-restore-server-portal.md)
