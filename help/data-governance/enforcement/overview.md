---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Présentation de l’application des stratégies
topic: enforcement
description: Une fois les étiquettes d’utilisation des données appliquées aux jeux de données Adobe Experience Platform et les stratégies d’utilisation des données définies pour les actions marketing par rapport à ces étiquettes, les fonctionnalités de gouvernance des données vous permettent d’appliquer ces stratégies et d’empêcher les opérations de données qui constituent des violations de stratégie. Il existe deux méthodes d’application des stratégies fournies par les fonctionnalités de gouvernance des données sur la plate-forme, l’application basée sur les API et l’application automatique.
translation-type: tm+mt
source-git-commit: 2fdab7d984a7368df77110f8ba0e0ba687e96d7e
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 16%

---


# Présentation de l’application des stratégies

Once data usage labels have been applied to [!DNL Platform] datasets, and data usage policies have been defined for marketing actions against those labels, [!DNL Data Governance] capabilities allow you to enforce those policies and prevent data operations that constitute policy violations.

Deux méthodes d&#39;application des politiques sont offertes par les [!DNL Data Governance] fonctionnalités [!DNL Platform]: **Application** basée sur les API et application **** automatique.

## Application basée sur les API

The [!DNL Policy Service] API provides endpoints that allow you to test marketing actions against datasets or arbitrary combinations of data usage labels in order to check if any policy violations occur. En fonction de la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience, afin d’être en conformité avec les stratégies d’utilisation des données.

Pour savoir comment évaluer l’application des stratégies à l’aide de l’API, voir le tutoriel sur [l’application des stratégies](api-enforcement.md).

## Application automatique

Certaines applications créées à partir de [!DNL Experience Platform] (par exemple [!DNL Real-time Customer Data Platform]) permettent l’application automatique des stratégies d’utilisation des données. Chaque application conserve sa propre méthode de détection des violations de la politique et fournit des étapes pour résoudre les problèmes.

Consultez la documentation de l&#39;application [!DNL Platform]basée que vous utilisez pour plus d&#39;informations sur l&#39;application automatique de la stratégie d&#39;utilisation des données. Pour plus d&#39;informations sur l&#39;application automatique de la stratégie dans le CDP en temps réel, consultez l&#39;aperçu [de la gouvernance des données du CDP en temps](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)réel.