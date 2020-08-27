---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: Présentation des libellés d’utilisation des données
topic: labels
description: Data Usage Labeling and Enforcement (DULE) constitue le mécanisme de base de la gouvernance des données d’Adobe Experience Platform. Les fonctionnalités de DULE vous permettent d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d’utilisation des données associées. Ce document donne un aperçu des libellés d’utilisation des données (également appelés libellés DULE) dans Experience Platform.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 23%

---


# Présentation des libellés d’utilisation des données

Adobe Experience Platform [!DNL Data Governance] allows you to apply data usage labels to datasets and fields, categorizing each according to related data usage policies.

Ce document fournit un aperçu des étiquettes d’utilisation des données dans [!DNL Experience Platform]. Before reading this guide, please see the [Data Governance overview](../home.md) for a more robust introduction to the Data Governance framework.

## Comprendre les libellés d’utilisation des données

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform].

Les libellés d’utilisation des données appliqués au niveau du jeu de données sont propagés à tous les champs du jeu de données. Vous pouvez également appliquer les libellés directement sur des champs individuels (en-têtes de colonne) d’un jeu de données, sans propagation.

[!DNL Platform] fournit plusieurs étiquettes d’utilisation de données &quot;de base&quot; prêtes à l’emploi, qui couvrent une grande variété de restrictions courantes applicables à la gouvernance des données. Pour plus d’informations sur ces étiquettes et les stratégies d’utilisation qu’elles représentent, voir le guide sur les étiquettes [d’utilisation des données de](reference.md)base.

Outre les étiquettes fournies par Adobe, vous pouvez également définir vos propres étiquettes personnalisées pour votre entreprise. See the section on [managing labels](#manage-labels) for more information.

## Héritage d’étiquette pour les segments d’audience

Tous les segments d’audience créés par [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) héritent des étiquettes d’utilisation de leurs jeux de données correspondants. Cela permet aux applications créées sur [!DNL Experience Platform] (par exemple [!DNL Real-time Customer Data Platform]) de fournir une application automatique de la stratégie d’utilisation des données lors de l’activation de segments vers des destinations.

Outre l’héritage d’étiquettes au niveau des jeux de données, les segments héritent par défaut de tous les libellés au niveau des champs de leurs jeux de données associés. Selon la manière dont votre application [!DNL Platform]basée sur le trafic des segments est utilisée, vous pouvez éventuellement spécifier les champs utilisés, ce qui empêche le segment d’hériter des libellés des champs exclus.

Pour plus d’informations sur le fonctionnement de l’application automatique dans le CDP en temps réel, voir l’aperçu sur la gouvernance des [données dans le CDP](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)en temps réel.

### Héritage des contrôles d&#39;exportation des données Adobe Audience Manager

[!DNL Experience Platform] permet de partager des segments avec Adobe Audience Manager. Tous les contrôles d’exportation de données appliqués aux segments d’Audience Manager sont traduits en étiquettes équivalentes et en actions marketing reconnues par [!DNL Experience Platform][!DNL Data Governance].

Pour savoir comment des contrôles d’exportation de données spécifiques correspondent aux étiquettes d’utilisation des données dans [!DNL Platform], consultez la documentation [de l’](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.

## Gestion des étiquettes d’utilisation des données dans [!DNL Experience Platform] {#manage-labels}

Vous pouvez gérer les étiquettes d’utilisation des données à l’aide [!DNL Experience Platform] d’API ou de l’interface utilisateur. Consultez les sous-sections ci-dessous pour plus de détails sur chacun d&#39;eux.

### Utilisation de l’interface utilisateur

L’espace de travail **[!UICONTROL Stratégies]** de l’ [!DNL Experience Platform] interface utilisateur vous permet de vue et de gérer des étiquettes personnalisées et de base pour votre entreprise. L’ **[!DNL Datasets]** espace de travail vous permet d’appliquer des étiquettes aux jeux de données et aux champs. For more information, refer to the [labels user guide](user-guide.md).

### Utilisation des API

Le `/labels` point de terminaison de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) Policy Service vous permet de gérer par programmation les étiquettes d’utilisation des données, y compris la création d’étiquettes personnalisées. Pour plus d’informations, consultez le guide [des points de terminaison des](../api/labels.md) étiquettes.

L’API [Service de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) dataset est utilisée pour gérer les étiquettes des jeux de données et des champs. Pour plus d’informations, consultez le guide sur la [gestion des étiquettes](./dataset-api.md) de jeux de données.

## Étapes suivantes

Ce document présente les étiquettes d’utilisation des données et leur rôle dans le cadre de la gouvernance des données. Reportez-vous à la documentation à laquelle est lié ce guide pour en savoir plus sur la gestion des étiquettes dans [!DNL Experience Platform].