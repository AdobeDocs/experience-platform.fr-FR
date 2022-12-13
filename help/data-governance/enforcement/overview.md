---
keywords: Experience Platform;accueil;rubriques populaires;Application des stratégies;Application automatique;Application basée sur les API;gouvernance des données
solution: Experience Platform
title: Présentation de l’application des stratégies
topic-legacy: guide
description: Découvrez comment les stratégies d’utilisation des données sont appliquées sur Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 6f79b1a03a75558d1a25f0375e8393ad56756d80
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 48%

---

# Présentation de l’application des stratégies

Une fois [libellés d’utilisation des données](../labels/overview.md) ont été appliquées et [stratégies d’utilisation des données](../policies/overview.md) ont été définies, vous pouvez appliquer ces stratégies afin d’empêcher les opérations de données qui constituent des violations de stratégie.

>[!NOTE]
>
>Ce document se concentre sur l’application des stratégies d’utilisation des données. Pour plus d’informations sur les stratégies de contrôle d’accès, reportez-vous au guide sur les [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md).

Il existe deux méthodes d’application des stratégies dans Adobe Experience Platform : application automatique et application basée sur les API.

## Application automatique

Experience Platform tire parti des fonctionnalités de gestion des stratégies, de classification des données et de parenté des données pour évaluer automatiquement et faire apparaître les violations de stratégies. Pour plus d’informations, consultez la présentation de l’[application automatique des stratégies](./auto-enforcement.md).

## Application basée sur les API

L’API [!DNL Policy Service] fournit des points d’entrée qui vous permettent de tester les actions marketing par rapport aux jeux de données ou à des combinaisons arbitraires de libellés d’utilisation des données, afin de vérifier si des violations de stratégies se produisent. En fonction de la réponse de l’API, vous pouvez ensuite configurer des protocoles dans votre application d’expérience afin d’appliquer correctement la conformité de la stratégie de gouvernance des données.

Pour savoir comment évaluer les stratégies à l’aide de l’API, consultez le tutoriel sur [l’application basée sur l’API](./api-enforcement.md).
