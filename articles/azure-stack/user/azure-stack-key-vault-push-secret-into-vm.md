---
title: Déployer une machine virtuelle avec un certificat stocké de façon sécurisée sur Azure Stack | Microsoft Docs
description: Découvrez comment déployer une machine virtuelle et y placer un certificat avec un coffre de clés dans Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/27/2018
ms.author: sethm
ms.lastreviewed: 12/27/2018
ms.openlocfilehash: 3e2ef77e0932c81746e24efecad020bd567a1fd5
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55250399"
---
# <a name="create-a-virtual-machine-and-install-a-certificate-retrieved-from-an-azure-stack-key-vault"></a>Créer une machine virtuelle et installer un certificat récupéré auprès d’un coffre de clés Azure Stack

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

Découvrez comment créer une machine virtuelle Azure Stack avec un certificat de coffre de clés installé.

## <a name="overview"></a>Vue d’ensemble

Les certificats sont utilisés dans de nombreux scénarios, comme l’authentification auprès d’Active Directory ou le chiffrement du trafic web. Vous pouvez stocker de manière sécurisée des certificats en tant que secrets dans un coffre de clés Azure Stack. Les avantages de l’utilisation d’un coffre de clés Azure Stack sont :

* Les certificats ne sont pas exposés dans un script, un historique de ligne de commande ou un modèle.
* Le processus de gestion des certificats est simple.
* Vous pouvez contrôler des clés qui accèdent aux certificats.

### <a name="process-description"></a>Description du processus

Les étapes suivantes décrivent le processus permettant de placer un certificat sur la machine virtuelle :

1. Créer un secret Key Vault.
2. Mettre à jour le fichier azuredeploy.parameters.json.
3. Déployez le modèle.

> [!NOTE]
> Vous pouvez utiliser ces étapes à partir du Kit de développement Azure Stack, ou à partir d’un client externe si vous êtes connecté via un VPN.

## <a name="prerequisites"></a>Prérequis

* Les utilisateurs doivent s’abonner à une offre qui inclut le service Key Vault.
* [Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).
* [Configurez l’environnement PowerShell de l’utilisateur Azure Stack](azure-stack-powershell-configure-user.md).

## <a name="create-a-key-vault-secret"></a>Créer un secret Key Vault

Le script suivant crée un certificat au format .pfx et un coffre de clés, puis stocke le certificat dans le coffre de clés en tant que secret.

> [!IMPORTANT]
> Vous devez utiliser le paramètre `-EnabledForDeployment` lors de la création du coffre de clés. Il garantit que le coffre de clés peut être référencé à partir de modèles Azure Resource Manager.

```powershell
# Create a certificate in the .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used to export the certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in the previous step>" `
  -FilePath "<Fully qualified path where the exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload the certificate into the key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where the exported certificate can be stored>"
$certPassword = "<Password used to export the certificate>"

$fileContentBytes = get-content $fileName `
  -Encoding Byte

$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
$jsonObject = @"
{
"data": "$filecontentencoded",
"dataType" :"pfx",
"password": "$certPassword"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -sku standard `
  -EnabledForDeployment

$secret = ConvertTo-SecureString `
  -String $jsonEncoded `
  -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
   -SecretValue $secret
```

À l’exécution du script précédent, la sortie inclut l’URI du secret. Notez cet URI. Vous devez le référencer dans le [modèle Placer le certificat dans Windows Resource Manager](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate). Téléchargez le dossier de modèles [vm-push-certificate-windows](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/201-vm-windows-pushcertificate) sur votre ordinateur de développement. Ce dossier contient les fichiers `azuredeploy.json` et `azuredeploy.parameters.json` dont vous avez besoin aux étapes suivantes.

Modifiez le fichier `azuredeploy.parameters.json` en fonction des valeurs de votre environnement. Les paramètres les plus intéressants sont le nom du coffre, le groupe de ressources du coffre et l’URI du secret (généré par le script précédent). La section suivante montre un exemple de fichier de paramètres.

## <a name="update-the-azuredeployparametersjson-file"></a>Mettre à jour le fichier azuredeploy.parameters.json

Mettez à jour le fichier `azuredeploy.parameters.json` avec `vaultName`, l’URI secret, `VmName` et d’autres valeurs en fonction de votre environnement. Le fichier JSON suivant est un exemple de fichier de paramètres du modèle :

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "newStorageAccountName": {
      "value": "kvstorage01"
    },
    "vmName": {
      "value": "VM1"
    },
    "vmSize": {
      "value": "Standard_D1_v2"
    },
    "adminUserName": {
      "value": "demouser"
    },
    "adminPassword": {
      "value": "demouser@123"
    },
    "vaultName": {
      "value": "contosovault"
    },
    "vaultResourceGroup": {
      "value": "contosovaultrg"
    },
    "secretUrlWithVersion": {
      "value": "https://testkv001.vault.local.azurestack.external/secrets/testcert002/82afeeb84f4442329ce06593502e7840"
    }
  }
}
```

## <a name="deploy-the-template"></a>Déployer le modèle

Déployez le modèle avec le script PowerShell suivant :

```powershell
# Deploy a Resource Manager template to create a VM and push the secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```

Une fois le modèle déployé, la sortie suivante est générée :

![Résultats du déploiement du modèle](media/azure-stack-key-vault-push-secret-into-vm/deployment-output.png)

Azure Stack envoie (push) le certificat sur la machine virtuelle lors du déploiement. L’emplacement du certificat dépend du système d’exploitation de la machine virtuelle :

* Sous Windows, le certificat est ajouté à l’emplacement de certificat **LocalMachine**, avec le magasin de certificats fourni par l’utilisateur.
* Sous Linux, le certificat est placé sous `/var/lib/waagent directory`, avec le nom de fichier &lt;UppercaseThumbprint&gt;.crt pour le fichier de certificat X509 et &lt;UppercaseThumbprint&gt;.prv pour la clé privée.

## <a name="retire-certificates"></a>Mettre hors service des certificats

La mise hors service de certificats fait partie du processus de gestion des certificats. Vous ne pouvez pas supprimer l’ancienne version d’un certificat, mais vous pouvez la désactiver en utilisant la cmdlet `Set-AzureKeyVaultSecretAttribute`.

L’exemple suivant montre comment désactiver un certificat. Utilisez vos propres valeurs pour les paramètres **VaultName**, **Name** et **Version**.

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a>Étapes suivantes

* [Déployer une machine virtuelle avec un mot de passe Key Vault](azure-stack-key-vault-deploy-vm-with-secret.md)
* [Autoriser une application à accéder à Key Vault](azure-stack-key-vault-sample-app.md)
