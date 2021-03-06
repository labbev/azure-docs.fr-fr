---
title: Azure Front Door Service - Backends et pools de backends | Microsoft Docs
description: Cet article vous aide à comprendre à quoi servent les backends et les pools de backends dans une configuration de porte d’entrée.
services: front-door
documentationcenter: ''
author: sharad4u
ms.service: frontdoor
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/10/2018
ms.author: sharadag
ms.openlocfilehash: 64d96d54b323d634703301e48cdaa28fa875fbbc
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46958796"
---
# <a name="backends-and-backend-pools-in-azure-front-door-service"></a>Backends et pools de backends dans Azure Front Door Service
Cet article explique les différents concepts concernant la façon dont vous pouvez mapper le déploiement de votre application avec une porte d’entrée. De même, nous vous expliquons le sens des différents termes relatifs aux backends d’application rencontrés dans une configuration de porte d’entrée.

## <a name="backend-pool"></a>Pool de backends
Dans une porte d’entrée, un pool de backends désigne un ensemble de backends équivalents capables de recevoir le même type de trafic pour leur application. En d’autres termes, il s’agit d’un regroupement logique de vos instances d’application à travers le monde qui peuvent recevoir le même trafic et répondre avec le comportement attendu. Ces backends sont généralement déployés dans différentes régions ou dans une même région. Par ailleurs, ces backends peuvent tous être en mode de déploiement actif/actif ou bien être définis en tant que configuration active/passive.

Un pool de backends définit également la façon dont l’intégrité des différents backends doit être évaluée via des sondes d’intégrité et comment parallèlement leur charge doit être équilibrée.

### <a name="health-probes"></a>Sondes d’intégrité
La porte d’entrée envoie régulièrement des demandes d’analyse HTTP/HTTPS à chacun de vos backends configurés pour déterminer leur proximité et leur intégrité dans l’optique d’équilibrer la charge des demandes de vos utilisateurs finaux. Les paramètres de sonde d’intégrité d’un pool de backends définissent la façon dont l’état d’intégrité des backends d’application est demandé. Les paramètres de configuration de l’équilibrage de charge disponibles sont les suivants :

1. **Chemin d’accès** : chemin d’URL que suivront les demandes d’analyse pour tous les backends du pool de backends. Par exemple, si l’un de vos backends est `contoso-westus.azurewebsites.net` et que le chemin défini est `/probe/test.aspx`, les environnements de porte d’entrée enverront les demandes d’analyse d’intégrité à http://contoso-westus.azurewebsites.net/probe/test.aspx, en partant du principe que le protocole défini est HTTP. 
2. **Protocole** : détermine si les demandes d’analyse d’intégrité de la porte d’entrée vers vos backends sont envoyées via le protocole HTTP ou HTTPS.
3. **Intervalle (secondes)**  : ce champ définit la fréquence des analyses d’intégrité de vos backends, c’est-à-dire les intervalles au cours desquels une sonde est envoyée par chaque environnement de porte d’entrée. Remarque : si vous êtes en quête de bascules rapides, attribuez à ce champ une valeur inférieure. Cependant, sachez que plus la valeur est basse, plus vos backends recevront un volume important de sondes d’intégrité. Pour vous faire une idée du volume de sondes que la porte d’entrée générera sur vos backends, prenons un exemple. Supposons que l’intervalle défini est de 30 secondes et qu’il existe environ 90 environnements de porte d’entrée ou points de présence (POP) à l’échelon mondial. Ainsi, chaque backend recevra environ 3 à 5 demandes d’analyse par seconde.

Pour plus d’informations, lisez [sondes d’intégrité](front-door-health-probes.md).

### <a name="load-balancing-settings"></a>Paramètres d’équilibrage de charge
Les paramètres d’équilibrage de charge d’un pool de backends définissent la façon dont les sondes d’intégrité sont évaluées pour déterminer si un backend est sain ou pas, mais aussi comment la charge du trafic doit être équilibrée entre les différents backends du pool. Les paramètres de configuration de l’équilibrage de charge disponibles sont les suivants :

1. **Taille de l’échantillon** : cette propriété identifie le nombre d’échantillons de sondes d’intégrité à prendre en compte pour évaluer l’intégrité d’un backend.
2. **Taille de l’échantillon concluante** : par rapport à la « taille de l’échantillon » expliquée ci-dessus, cette propriété définit le nombre d’échantillons qui doivent être concluants pour que le backend soit considéré comme sain. 
</br>Par exemple, supposons que pour votre porte d’entrée, vous avez défini l’*intervalle* d’analyse d’intégrité à 30 secondes, la *taille de l’échantillon* à 5 et la *taille de l’échantillon concluante* à 3. Cette configuration signifie qu’à chaque évaluation de l’intégrité de votre backend, les cinq derniers échantillons sont examinés, ce qui correspond aux dernières 150 secondes (= 5*30 s) et à moins que 3 analyses ou plus ont été concluantes, le backend est déclaré défectueux. Donc, si seulement deux analyses sont concluantes, le backend est marqué comme étant défectueux. À l’évaluation suivante, si 3 des cinq dernières analyses sont concluantes, le backend est de nouveau marqué comme étant sain.
3. **Sensibilité de la latence (latence supplémentaire)**  : le champ de sensibilité de la latence définit si la porte d’entrée doit envoyer la demande aux backends qui se trouvent dans la plage de sensibilité en termes de mesure de latence ou si elle doit transférer la demande au backend le plus proche. Pour plus d’informations, consultez [Méthode de routage basée sur la latence la plus faible](front-door-routing-methods.md#latency) pour Front Door.

## <a name="backend"></a>Backend
Un backend est l’équivalent d’une instance de déploiement d’application dans une région. Front Door prend en charge les backends Azure et non Azure. Autrement dit, la région ne se limite pas ici limitée aux régions Azure et peut aussi correspondre à votre centre de données local ou à une instance d’application dans un autre cloud.

Dans le contexte des portes d’entrée, les backends représentent le nom d’hôte ou l’adresse IP publique de votre application, qui peut traiter les demandes des clients. Par conséquent, vous ne devez pas confondre les backends avec votre niveau de base de données, votre niveau de stockage, etc., mais plutôt les considérer comme le point de terminaison public de votre backend d’application.

Quand vous ajoutez un backend à un pool de backends de votre porte d’entrée, vous devez fournir les informations suivantes :

1. **Type de l’hôte backend** : type de ressource que vous souhaitez ajouter. La porte d’entrée prend en charge la détection automatique de vos backends d’application s’ils sont issus d’App Service, du service cloud ou de Stockage. Si vous voulez une autre ressource Azure, voire un backend non Azure, sélectionnez « Hôte personnalisé ». Remarque : pendant la configuration, les API ne vérifient pas si le backend est accessible à partir des environnements de porte d’entrée. C’est donc à vous qu’il revient de vérifier que la porte d’entrée peut atteindre votre backend. 
2. **Abonnement et Nom de l’hôte backend** : si vous n’avez pas sélectionné « Hôte personnalisé » pour le type de l’hôte backend, vous devez réduire l’étendue des opérations et sélectionner votre backend en choisissant l’abonnement approprié et le nom de l’hôte backend correspondant dans l’utilisateur interface.
3. **En-tête de l’hôte backend** : valeur d’en-tête de l’hôte envoyée au backend pour chaque demande. Pour plus d’informations, consultez [En-tête de l’hôte backend](#hostheader).
4. **Priorité** : vous pouvez attribuer des priorités à vos différents backends si vous voulez utiliser un backend de service principal pour l’ensemble du trafic et fournir une solution de secours en cas d’indisponibilité des backends principal ou de secours. En savoir plus sur la [priorité](front-door-routing-methods.md#priority).
5. **Poids** : vous pouvez attribuer des poids à vos différents backends si vous voulez répartir le trafic entre un ensemble de backends, que ce soit de façon équitable ou selon des coefficients de pondération. En savoir plus sur les [poids](front-door-routing-methods.md#weighted).


### <a name = "hostheader"></a>En-tête de l’hôte backend

Les demandes transférées par la porte d’entrée à un backend ont un champ En-tête de l’hôte dont se sert le backend pour récupérer la ressource cible. La valeur de ce champ provient généralement de l’URI du backend et indique l’hôte et le port. Par exemple, une demande formulée pour `www.contoso.com` aura l’en-tête d’hôte `www.contoso.com`. Si vous configurez votre backend à partir du portail Azure, la valeur renseignée par défaut pour ce champ est le nom d’hôte du backend. Par exemple, si votre backend est `contoso-westus.azurewebsites.net`, la valeur renseignée automatiquement pour l’en-tête de l’hôte backend dans le portail Azure est `contoso-westus.azurewebsites.net`. 
</br>En revanche, si vous utilisez des modèles Resource Manager ou un autre mécanisme et que vous ne définissez pas ce champ explicitement, la porte d’entrée envoie le nom d’hôte entrant comme valeur du champ En-tête de l’hôte. Par exemple, si la demande a été formulée pour `www.contoso.com` et que votre backend est `contoso-westus.azurewebsites.net` avec un champ En-tête de l’hôte backend vide, la porte d’entrée attribue au champ En-tête de l’hôte la valeur `www.contoso.com`.

La plupart des backends d’application (comme Web Apps, Stockage Blob et Cloud Services) exigent une correspondance entre l’en-tête de l’hôte et le domaine du backend. Cependant, l’hôte frontend qui achemine vers votre backend aura un nom d’hôte différent comme www.contoso.azurefd.net. Si le backend que vous configurez exige une correspondance entre l’en-tête de l’hôte et le nom d’hôte du backend, vous devez veiller à ce que le champ « En-tête de l’hôte backend » présente aussi le nom d’hôte du backend.

#### <a name="configuring-the-backend-host-header-for-the-backend"></a>Configuration du champ En-tête de l’hôte backend pour le backend
Le champ « En-tête de l’hôte backend » peut être configuré pour un backend dans la section Pool de backends.

1. Ouvrez votre ressource de porte d’entrée, puis cliquez sur le pool de backends qui contient le backend à configurer.

2. Ajoutez un backend si ce n’est pas déjà fait ou modifiez-en un existant. Le champ « En-tête de l’hôte backend » peut être défini avec une valeur personnalisée ou laissé vide, ce qui signifie que le nom d’hôte pour la demande entrante sera utilisé comme valeur du champ En-tête de l’hôte.



## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment [créer un porte d’entrée](quickstart-create-front-door.md).
- Découvrez [comment fonctionne une porte d’entrée](front-door-routing-architecture.md).