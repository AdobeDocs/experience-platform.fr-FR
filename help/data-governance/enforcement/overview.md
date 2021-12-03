---
keywords: Experience Platform;accueil;rubriques populaires;Application des stratégies;Application automatique;Application basée sur les API;gouvernance des données
solution: Experience Platform
title: Présentation de l’application des stratégies
topic-legacy: guide
description: Une fois que les libellés d’utilisation des données ont été appliqués aux jeux de données d’Adobe Experience Platform et que les stratégies d’utilisation des données ont été définies pour les actions marketing suivant ces libellés, les fonctionnalités de gouvernance des données vous permettent d’appliquer ces stratégies et d’empêcher les opérations de données en violation avec celles-ci. Il existe deux méthodes d’application des stratégies fournies par les fonctionnalités de gouvernance des données sur Platform. Il s’agit de l’application basée sur les API et de l’application automatique.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: ht
source-wordcount: '239'
ht-degree: 100%

---

# Présentation de l’application des stratégies

Une fois que les libellés d’utilisation des données ont été appliqués aux jeux de données et que les stratégies d’utilisation des données ont été définies pour les actions marketing suivant ces libellés, les fonctionnalités de gouvernance des données d’Adobe Experience Platform vous permettent d’appliquer ces stratégies et d’empêcher les opérations de données en violation avec celles-ci.

Il existe deux méthodes d’application des stratégies fournies par les fonctionnalités de gouvernance des données sur [!DNL Platform] : il s’agit de l’application basée sur les API et de l’application automatique.

## Application basée sur les API

L’API [!DNL Policy Service] fournit des points d’entrée qui vous permettent de tester les actions marketing par rapport aux jeux de données ou à des combinaisons arbitraires de libellés d’utilisation des données, afin de vérifier si des violations de stratégies se produisent. En fonction de la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience, afin d’être en conformité avec les stratégies d’utilisation des données.

Pour savoir comment évaluer les stratégies à l’aide de l’API, consultez le tutoriel sur [l’application basée sur l’API](./api-enforcement.md).

## Application automatique

Experience Platform tire parti des fonctionnalités de gestion des stratégies, de classification des données et de parenté des données pour évaluer automatiquement et faire apparaître les violations de stratégies. Pour plus d’informations, consultez la présentation de l’[application automatique des stratégies](./auto-enforcement.md).
