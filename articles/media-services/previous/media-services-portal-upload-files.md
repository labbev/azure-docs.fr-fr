---
title: Charger des fichiers vers un compte Media Services dans le portail Azure | Microsoft Docs
description: Ce didacticiel vous indique les étapes à suivre pour charger des fichiers vers un compte Media Services dans le portail Azure.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/08/2019
ms.author: juliako
ms.openlocfilehash: 7730d15b0d3be9c0ffc7c7fbafe40fece713afbd
ms.sourcegitcommit: 943af92555ba640288464c11d84e01da948db5c0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2019
ms.locfileid: "55976790"
---
# <a name="upload-files-to-a-media-services-account-in-the-azure-portal-legacy"></a>Charger des fichiers vers un compte Media Services dans le portail Azure (hérité)

> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> Pour suivre ce tutoriel, vous avez besoin d’un compte Azure. Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 

Dans Azure Media Services, vous chargez vos fichiers numériques vers une ressource. Cette ressource peut contenir des fichiers vidéo, des fichiers audio, des images, des collections de miniatures, des pistes textuelles et des fichiers de sous-titres (ainsi que les métadonnées concernant ces fichiers). Une fois les fichiers chargés, votre contenu est stocké en toute sécurité dans le cloud, à des fins de traitement approfondi et de diffusion en continu.

> [!NOTE]
> Media Services définit une taille de fichier maximale pour le traitement des fichiers. Pour obtenir des informations détaillées sur les limites de taille de fichier, voir [Quotas et limitations](media-services-quotas-and-limitations.md).
>

## <a name="upload-files"></a>Charger des fichiers
1. Dans le [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Sélectionnez **Paramètres** > **Éléments multimédias**. Ensuite, cliquez sur le bouton **Charger**.
   
    ![Charger des fichiers](./media/media-services-portal-vod-get-started/media-services-upload.png)
   
    La fenêtre **Upload a video asset** (Charger un élément multimédia vidéo) s’affiche.
   
   > [!NOTE]
   > Media Services ne limite pas la taille de fichier des vidéos chargées.
 
3. Sur votre ordinateur, accédez à la vidéo que vous souhaitez charger. Sélectionnez la vidéo, puis cliquez sur **OK**.  
   
    Le chargement démarre. La progression s’affiche sous le nom du fichier.  

Une fois le chargement terminé, la nouvelle ressource est répertoriée dans le volet **Ressources**. 

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Étapes suivantes
* Vous pouvez désormais [encoder vos ressources chargées](media-services-portal-encode.md).

* Vous pouvez également utiliser Azure Functions pour déclencher une tâche de codage lorsqu’un fichier arrive dans le conteneur configuré. Pour plus d’informations, consultez l’exemple dans [Media Services : Intégration d’Azure Media Services dans Azure Functions et Logic Apps](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/).


