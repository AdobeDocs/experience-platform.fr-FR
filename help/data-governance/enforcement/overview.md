---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l'application des stratégies
topic: enforcement
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Présentation de l&#39;application des stratégies

Une fois les étiquettes d’utilisation des données appliquées aux [!DNL Platform] jeux de données et les stratégies d’utilisation des données définies pour les actions marketing par rapport à ces étiquettes, [!DNL Data Governance] les fonctionnalités vous permettent d’appliquer ces stratégies et d’empêcher les opérations de données qui constituent des violations de stratégie.

Deux méthodes d&#39;application des politiques sont offertes par les [!DNL Data Governance] fonctionnalités [!DNL Platform]: **Application** basée sur les API et application **** automatique.

## Application basée sur les API

L’ [!DNL Policy Service] API fournit des points de terminaison qui vous permettent de tester des actions marketing par rapport à des jeux de données ou à des combinaisons arbitraires d’étiquettes d’utilisation de données afin de vérifier si des violations de stratégie se produisent. En fonction de la réponse de l’API, vous pouvez ensuite configurer des protocoles au sein de votre application d’expérience afin d’appliquer de manière appropriée les règles d’utilisation des données.

Consultez le didacticiel sur l’application [des](api-enforcement.md) stratégies pour connaître les étapes d’évaluation des stratégies à l’aide de l’API.

## Application automatique

Certaines applications créées à partir de [!DNL Experience Platform] (par exemple [!DNL Real-time Customer Data Platform]) permettent l’application automatique des stratégies d’utilisation des données. Chaque application conserve sa propre méthode de détection des violations de la politique et fournit des étapes pour résoudre les problèmes.

Consultez la documentation de l&#39;application [!DNL Platform]basée que vous utilisez pour plus d&#39;informations sur l&#39;application automatique de la stratégie d&#39;utilisation des données. Pour plus d&#39;informations sur l&#39;application automatique de la stratégie dans le CDP en temps réel, consultez l&#39;aperçu [de la gouvernance des données du CDP en temps](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)réel.