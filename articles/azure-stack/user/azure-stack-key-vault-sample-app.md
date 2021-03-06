---
title: Autoriser les applications à récupérer les secrets d’un coffre de clés dans Azure Stack | Microsoft Docs
description: Utiliser un exemple d’application à utiliser avec Azure Stack Key Vault
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/27/2018
ms.author: sethm
ms.lastreviewed: 12/27/2018
ms.openlocfilehash: e395b3f24ac525ce226d5520ff483b07d23636b5
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55241965"
---
# <a name="a-sample-application-that-uses-keys-and-secrets-stored-in-a-key-vault"></a>Exemple d’application qui utilise des clés et des secrets stockés dans un coffre de clés

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

Suivez les étapes de cet article pour exécuter un exemple d’application nommé **HelloKeyVault**, qui récupère les clés et les secrets d’un coffre de clés dans Azure Stack.

## <a name="prerequisites"></a>Prérequis

Vous pouvez installer les prérequis suivants à partir du [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) Azure Stack ou à partir d’un client externe Windows si vous êtes [connecté via un VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) :

* Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).
* Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).

## <a name="create-and-get-the-key-vault-and-application-settings"></a>Créer et obtenir les paramètres du coffre de clés et de l’application

Pour préparer l’exemple d’application :

* Créez un coffre de clés dans Azure Stack.
* Inscrivez une application dans Azure Active Directory (Azure AD).

Pour préparer l’exemple d’application, vous pouvez utiliser le portail Azure ou PowerShell. Cet article explique comment créer un coffre de clés et inscrire une application avec PowerShell.

>[!NOTE]
>Par défaut, le script PowerShell crée une application dans Active Directory. Cependant, vous pouvez inscrire une de vos applications existantes.

Avant d’exécuter le script suivant, veillez à fournir des valeurs pour les variables `aadTenantName` et `applicationPassword`. Si vous ne spécifiez pas de valeur pour `applicationPassword`, ce script génère un mot de passe aléatoire.

```powershell
$vaultName           = 'myVault'
$resourceGroupName   = 'myResourceGroup'
$applicationName     = 'myApp'
$location            = 'local'

# Password for the application. If not specified, this script will generate a random password during app creation.
$applicationPassword = ''

# Function to generate a random password for the application.
Function GenerateSymmetricKey()
{
    $key = New-Object byte[](32)
    $rng = [System.Security.Cryptography.RNGCryptoServiceProvider]::Create()
    $rng.GetBytes($key)
    return [System.Convert]::ToBase64String($key)
}

Write-Host 'Please log into your Azure Stack user environment' -foregroundcolor Green

$tenantARM = "https://management.local.azurestack.external"
$aadTenantName = "FILL THIS IN WITH YOUR AAD TENANT NAME. FOR EXAMPLE: myazurestack.onmicrosoft.com"

# Configure the Azure Stack operator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackUser" `
  -ArmEndpoint $tenantARM

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $aadTenantName `
  -EnvironmentName AzureStackUser

# Sign in to the user portal.
Add-AzureRmAccount `
  -EnvironmentName "AzureStackUser" `
  -TenantId $TenantID `

$now = [System.DateTime]::Now
$oneYearFromNow = $now.AddYears(1)

$applicationPassword = GenerateSymmetricKey

# Create a new Azure AD application.
$identifierUri = [string]::Format("http://localhost:8080/{0}",[Guid]::NewGuid().ToString("N"))
$homePage = "http://contoso.com"

Write-Host "Creating a new AAD Application"
$ADApp = New-AzureRmADApplication `
  -DisplayName $applicationName `
  -HomePage $homePage `
  -IdentifierUris $identifierUri `
  -StartDate $now `
  -EndDate $oneYearFromNow `
  -Password $applicationPassword

Write-Host "Creating a new AAD service principal"
$servicePrincipal = New-AzureRmADServicePrincipal `
  -ApplicationId $ADApp.ApplicationId

# Create a new resource group and a key vault in that resource group.
New-AzureRmResourceGroup `
  -Name $resourceGroupName `
  -Location $location

Write-Host "Creating vault $vaultName"
$vault = New-AzureRmKeyVault -VaultName $vaultName `
  -ResourceGroupName $resourceGroupName `
  -Sku standard `
  -Location $location

# Specify full privileges to the vault for the application.
Write-Host "Setting access policy"
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName `
  -ObjectId $servicePrincipal.Id `
  -PermissionsToKeys all `
  -PermissionsToSecrets all

Write-Host "Paste the following settings into the app.config file for the HelloKeyVault project:"
'<add key="VaultUrl" value="' + $vault.VaultUri + '"/>'
'<add key="AuthClientId" value="' + $servicePrincipal.ApplicationId + '"/>'
'<add key="AuthClientSecret" value="' + $applicationPassword + '"/>'
Write-Host
```

L’image suivante montre la sortie du script utilisé pour créer le coffre de clés :

![Coffre de clés avec des clés d’accès](media/azure-stack-key-vault-sample-app/settingsoutput.png)

Prenez note des valeurs de **VaultUrl**, **AuthClientId** et **AuthClientSecret** renvoyées par le script précédent. Vous utiliserez ces valeurs pour exécuter l’application HelloKeyVault.

## <a name="download-and-configure-the-sample-application"></a>Télécharger et configurer l’exemple d’application

Téléchargez l’exemple de coffre de clés à partir de la page [Azure Key Vault client samples](https://www.microsoft.com/download/details.aspx?id=45343). Extrayez le contenu du fichier .zip sur votre station de travail de développement. Il existe deux applications dans le dossier d’exemples. Cet article utilise **HelloKeyVault**.

Pour charger l’exemple **HelloKeyVault** :

* Accédez au dossier **Microsoft.Azure.KeyVault.Samples** > **samples** > **HelloKeyVault**.
* Ouvrez l’application **HelloKeyVault** dans Visual Studio.

### <a name="configure-the-sample-application"></a>Configurer l’exemple d’application

Dans Visual Studio :

* Ouvrez le fichier HelloKeyVault\App.config et accédez à l’élément &lt;**appSettings**&gt;.
* Mettez à jour les clés **VaultUrl**, **AuthClientId** et **AuthClientSecret** avec les valeurs renvoyées par celles utilisées pour créer le coffre de clés. Par défaut, le fichier App.config a un espace réservé pour `AuthCertThumbprint`. Remplacez cet espace réservé par `AuthClientSecret`.

  ![Paramètres de l’application](media/azure-stack-key-vault-sample-app/appconfig.png)

* Régénérez la solution.

## <a name="run-the-application"></a>Exécution de l'application

Quand vous exécutez HelloKeyVault, l’application se connecte à Azure AD, puis utilise le jeton AuthClientSecret pour s’authentifier auprès du coffre de clés dans Azure Stack.

Vous pouvez utiliser l’exemple HelloKeyVault pour :

* Effectuer des opérations de base comme créer, chiffrer, wrapper et supprimer des clés et des secrets.
* Transmettre des paramètres comme `encrypt` et `decrypt` à HelloKeyVault, et appliquer les modifications spécifiées à un coffre de clés.

## <a name="next-steps"></a>Étapes suivantes

- [Déployer une machine virtuelle avec un mot de passe Key Vault](azure-stack-key-vault-deploy-vm-with-secret.md)
- [Déployer une machine virtuelle avec un certificat Key Vault](azure-stack-key-vault-push-secret-into-vm.md)
