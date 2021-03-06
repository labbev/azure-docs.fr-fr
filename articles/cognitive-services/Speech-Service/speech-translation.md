---
title: À propos de la traduction vocale - Services Speech
titlesuffix: Azure Cognitive Services
description: L’API du service Speech vous permet d’ajouter une traduction de bout en bout, en temps réel et multilingue de la parole à vos applications, outils et appareils. La même API peut être utilisée pour la traduction de parole en parole et de parole en texte.
services: cognitive-services
author: erhopf
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 12/06/2018
ms.author: erhopf
ms.custom: seodec18
ms.openlocfilehash: e77bfcdf2e037c7f6221b6761df708dac01924dd
ms.sourcegitcommit: 90cec6cccf303ad4767a343ce00befba020a10f6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55879239"
---
# <a name="about-the-speech-translation-api"></a>À propos de l’API Traduction vocale

L’API du service Speech vous permet d’ajouter une traduction de bout en bout, en temps réel et multilingue de la parole à vos applications, outils et appareils. La même API peut être utilisée pour la traduction de parole en parole et de parole en texte.

Avec l’API de traduction de conversation Translator Speech, les applications clientes diffusent l’audio de la parole vers le service, et reçoivent un flux de résultats. Ces résultats incluent le texte reconnu dans la langue source et sa traduction dans la langue cible. Des traductions intermédiaires peuvent être fournies jusqu’à ce qu’un énoncé soit complet, moment auquel une traduction finale est fournie.

Si vous le souhaitez, une version audio synthétisée de la traduction finale peut être préparée, qui permet une véritable traduction de parole en parole.

L’API Traduction vocale utilise un protocole WebSocket pour fournir un canal de communication en duplex intégral entre le client et le serveur. Mais vous n’avez pas besoin de gérer les WebSockets. Le Kit de développement logiciel (SDK) pour Speech gère cela pour vous.

L’API Traduction vocale utilise des technologies qui soutiennent différents produits et services Microsoft. Des milliers d’entreprises dans le monde utilisent déjà ce service dans leurs applications et flux de travail.

## <a name="about-the-technology"></a>À propos de la technologie

Deux approches sont sous-jacentes au moteur de traduction de Microsoft : la traduction automatique statistique (SMT) et la traduction automatique neuronale (NMT). La deuxième, une approche d’intelligence artificielle utilisant des réseaux neuronaux, est l’approche plus moderne de la traduction automatique. La NMT fournit de meilleures traductions, pas simplement plus précises, mais également plus fluides et naturelles. La cause principale de cette fluidité est que la NMT utilise le contexte entier d’une phrase pour traduire des mots.

Aujourd’hui, Microsoft a migré vers la NMT pour les langues les plus répandues, et n’utilise la SMT que pour les langues moins fréquemment utilisées. Tous les [langues disponibles pour la traduction de parole en parole](language-support.md#speech-translation) sont alimentées par la NMT. La traduction de parole en texte peut utiliser la SMT ou la NMT en fonction de la paire de langues. Si la langue cible est prise en charge par la NMT, la traduction complète s’appuie sur NMT. Si la langue cible n’est pas prise en charge par la NMT, la traduction est un hybride de NMT et SMT, utilisant l’anglais comme langue « pivot » entre les deux langues.

Les différences entre les modèles sont internes au moteur de traduction. Les utilisateurs finaux constatent uniquement la meilleure qualité de la traduction, en particulier pour le chinois, le japonais et l’arabe.

> [!NOTE]
> Vous souhaitez en savoir plus sur la technologie du moteur de traduction de Microsoft ? Voir [Traduction automatique](https://www.microsoft.com/en-us/translator/mt.aspx).

## <a name="next-steps"></a>Étapes suivantes

* [Obtenir votre abonnement d’essai gratuit au service Speech](https://azure.microsoft.com/try/cognitive-services/)
* [Découvrir comment traduire une entrée vocale dans C#](how-to-translate-speech-csharp.md)
* [Découvrir comment traduire une entrée vocale dans C++](how-to-translate-speech-cpp.md)
* [Découvrir comment traduire une entrée vocale dans Java](how-to-translate-speech-java.md)
