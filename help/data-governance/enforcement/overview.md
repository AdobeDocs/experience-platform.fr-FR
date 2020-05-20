---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l'application des stratégies
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Présentation de l&#39;application des stratégies

Une fois que les étiquettes d’utilisation des données ont été appliquées aux jeux de données de la plate-forme et que les stratégies d’utilisation des données ont été définies pour les actions marketing par rapport à ces étiquettes, les capacités de gouvernance des données vous permettent d’appliquer ces stratégies et d’empêcher les opérations de données qui constituent des violations de stratégie.

Deux méthodes d’application des politiques sont fournies par les fonctionnalités de gouvernance des données sur la plate-forme : **Application** basée sur les API et application **** automatique.

## Application basée sur les API

L’API Policy Service fournit des points de terminaison qui vous permettent de tester des actions marketing par rapport à des jeux de données ou à des combinaisons arbitraires de libellés d’utilisation des données afin de vérifier si des violations de stratégie se produisent. En fonction de la réponse de l’API, vous pouvez ensuite configurer des protocoles au sein de votre application d’expérience afin d’appliquer de manière appropriée les règles d’utilisation des données.

Consultez le didacticiel sur l’application [des](api-enforcement.md) stratégies pour connaître les étapes d’évaluation des stratégies à l’aide de l’API.

## Application automatique

Certaines applications créées sur la plate-forme d’expérience (telle que la plate-forme de données clientes en temps réel) assurent l’application automatique des stratégies d’utilisation des données. Chaque application conserve sa propre méthode de détection des violations de la politique et fournit des étapes pour résoudre les problèmes.

Consultez la documentation de l&#39;application basée sur la plate-forme que vous utilisez pour plus d&#39;informations sur l&#39;application automatique de la stratégie d&#39;utilisation des données. Pour plus d&#39;informations sur l&#39;application automatique de la stratégie dans le CDP en temps réel, consultez l&#39;aperçu [de la gouvernance des données du CDP en temps](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)réel.