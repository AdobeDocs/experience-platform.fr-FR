---
keywords: Experience Platform ; accueil ; rubriques populaires ; Application des stratégies ; Application automatique ; Application basée sur les API ; gouvernance des données
solution: Experience Platform
title: Présentation de l'application des stratégies
topic-legacy: guide
description: Une fois les étiquettes d’utilisation des données appliquées aux jeux de données Adobe Experience Platform et les stratégies d’utilisation des données définies pour les actions marketing par rapport à ces étiquettes, les fonctionnalités de gouvernance des données vous permettent d’appliquer ces stratégies et d’empêcher les opérations de données qui constituent des violations de stratégie. Il existe deux méthodes d’application des stratégies fournies par les fonctionnalités de gouvernance des données sur la plate-forme, l’application basée sur les API et l’application automatique.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 10%

---

# Présentation de l’application des stratégies

Une fois que les étiquettes d’utilisation des données ont été appliquées aux jeux de données et que les stratégies d’utilisation des données ont été définies pour les actions marketing par rapport à ces étiquettes, les fonctionnalités de gouvernance des données de Adobe Experience Platform vous permettent d’appliquer ces stratégies et d’empêcher les opérations de données qui constituent des violations de stratégie.

Les fonctions [!DNL Data Governance] de [!DNL Platform] offrent deux méthodes d&#39;application des politiques : Application de la loi basée sur les API et application automatique.

## Application basée sur les API

L&#39;API [!DNL Policy Service] fournit des points de terminaison qui vous permettent de tester des actions marketing par rapport à des jeux de données ou à des combinaisons arbitraires d&#39;étiquettes d&#39;utilisation de données afin de vérifier si des violations de stratégie se produisent. En fonction de la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience, afin d’être en conformité avec les stratégies d’utilisation des données.

Pour savoir comment évaluer les stratégies à l’aide de l’API, consultez le didacticiel [Application basée sur l’API](./api-enforcement.md).

## Application automatique

L&#39;Experience Platform utilise les capacités de gestion des stratégies, de classification des données et de gestion des données pour évaluer automatiquement les violations de stratégie et les faire apparaître. Pour plus d&#39;informations, consultez la présentation de [application automatique de la stratégie](./auto-enforcement.md).
