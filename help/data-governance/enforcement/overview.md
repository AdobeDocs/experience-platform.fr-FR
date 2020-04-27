---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l'application des stratégies
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc

---


# Présentation de l&#39;application des stratégies

Une fois que les étiquettes d’utilisation des données ont été appliquées aux jeux de données de la plateforme et que les stratégies d’utilisation des données ont été définies pour les actions marketing par rapport à ces étiquettes, les fonctionnalités de gouvernance des données vous permettent d’appliquer ces stratégies et d’empêcher les opérations de données qui constituent des violations de la stratégie.

Il existe deux méthodes d’application des politiques fournies par les fonctionnalités de gouvernance des données sur la plateforme : Application **basée sur les** API et application **** automatique.

## Application basée sur les API

L’API Service de stratégie fournit des points de fin qui vous permettent de tester les actions marketing par rapport aux jeux de données ou à des combinaisons arbitraires de libellés d’utilisation des données afin de vérifier si des violations de stratégie se produisent. En fonction de la réponse de l’API, vous pouvez ensuite configurer des protocoles dans votre application d’expérience afin d’appliquer correctement la conformité aux stratégies d’utilisation des données.

Consultez le didacticiel sur l’application [des](api-enforcement.md) stratégies pour savoir comment évaluer les stratégies à l’aide de l’API.

## Application automatique

Certaines applications créées à partir de la plateforme d’expérience (telle que la plateforme de données clientes en temps réel) assurent l’application automatique des stratégies d’utilisation des données. Chaque application conserve sa propre méthode de détection des violations de stratégie et fournit des étapes pour résoudre les problèmes.

Consultez la documentation de l’application basée sur la plateforme que vous utilisez pour plus d’informations sur l’application automatique de la stratégie d’utilisation des données. Pour plus d&#39;informations sur l&#39;application automatique de la stratégie dans le CDP en temps réel, consultez l&#39;aperçu [de la gouvernance des données CDP en temps](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)réel.