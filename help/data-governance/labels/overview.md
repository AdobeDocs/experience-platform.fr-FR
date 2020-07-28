---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des libellés d’utilisation des données
topic: labels
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 28%

---


# Présentation des libellés d’utilisation des données

Data Usage Labeling and Enforcement (DULE) is the core mechanism of Adobe Experience Platform [!DNL Data Governance]. Les fonctionnalités de DULE vous permettent d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d’utilisation des données associées.

Ce document donne un aperçu des libellés d’utilisation des données (également appelés libellés DULE) dans [!DNL Experience Platform]. Avant de lire ce guide, consultez la [présentation de la gouvernance des données](../home.md) pour une introduction plus détaillée du cadre DULE.

## Comprendre les libellés d’utilisation des données

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform].

Les libellés d’utilisation des données appliqués au niveau du jeu de données sont propagés à tous les champs du jeu de données. Vous pouvez également appliquer les libellés directement sur des champs individuels (en-têtes de colonne) d’un jeu de données, sans propagation.

[!DNL Platform] fournit plusieurs étiquettes d’utilisation de données &quot;de base&quot; prêtes à l’emploi, qui couvrent une grande variété de restrictions courantes applicables à la gouvernance des données. Pour plus d’informations sur ces étiquettes et les stratégies d’utilisation qu’elles représentent, voir le guide sur les étiquettes [d’utilisation des données de](reference.md)base.

In addition to the labels provided by Adobe, you can also define your own custom labels. Pour savoir comment procéder dans l’interface utilisateur, voir le guide [d’utilisation des étiquettes d’utilisation des](./user-guide.md)données. Pour savoir comment effectuer cette opération à l’aide d’appels d’API, consultez le guide [sur les étiquettes d’utilisation des](./api.md)données.

## Héritage d’étiquette pour les segments d’audience

Tous les segments d’audience créés par [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) héritent des étiquettes d’utilisation des jeux de données correspondants. Cela permet aux applications créées sur [!DNL Experience Platform] (par exemple [!DNL Real-time Customer Data Platform]) de fournir une application automatique de la stratégie d’utilisation des données lors de l’activation de segments vers des destinations.

Outre l’héritage d’étiquettes au niveau des jeux de données, les segments héritent par défaut de tous les libellés au niveau des champs de leurs jeux de données associés. Selon la manière dont votre application [!DNL Platform]basée sur le trafic des segments est utilisée, vous pouvez éventuellement spécifier les champs utilisés, ce qui empêche le segment d’hériter des libellés des champs exclus.

Pour plus d&#39;informations sur le fonctionnement de l&#39;application automatique dans le CDP en temps réel, consultez l&#39;aperçu [de la gouvernance des données CDP en temps réel de l&#39;](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe.

### Héritage des contrôles d&#39;exportation des données d&#39;Adobe Audience Manager

[!DNL Experience Platform] permet de partager des segments avec l’Adobe Audience Manager. Tous les contrôles d’exportation de données appliqués aux segments d’Audience Manager sont traduits en étiquettes équivalentes et en actions marketing reconnues par [!DNL Experience Platform][!DNL Data Governance].

Pour savoir comment des contrôles d’exportation de données spécifiques correspondent aux étiquettes d’utilisation des données dans [!DNL Platform], consultez la documentation [de l’](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.


## Étapes suivantes

Now that you have been introduced data usage labels, you can continue to the read the [user guide](user-guide.md) to learn how to manage labels in the [!DNL Experience Platform] UI. Pour savoir comment gérer les libellés à l’aide des API, consultez le guide [API des libellés d’](./api.md)utilisation.