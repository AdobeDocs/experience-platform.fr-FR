---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des étiquettes d’utilisation des données
topic: labels
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Présentation des étiquettes d’utilisation des données

L&#39;étiquetage et l&#39;application de l&#39;utilisation des données (DULE) est le mécanisme de base de la gouvernance des données d&#39;Adobe Experience Platform. Les fonctions DULE permettent d&#39;appliquer des étiquettes d&#39;utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d&#39;utilisation des données associées.

Ce document présente un aperçu des étiquettes d’utilisation des données (également appelées étiquettes DULE) dans [!DNL Experience Platform]. Avant de lire ce guide, veuillez consulter l&#39;aperçu [de la gouvernance des](../home.md) données pour une introduction plus robuste au cadre DULE.

## Présentation des étiquettes d’utilisation des données

Les étiquettes d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Les étiquettes peuvent être appliquées à tout moment, ce qui vous permet de gérer les données avec souplesse. Les meilleures pratiques encouragent l’étiquetage des données dès leur assimilation [!DNL Experience Platform]ou dès que les données deviennent disponibles pour utilisation dans [!DNL Platform].

Les étiquettes d’utilisation des données appliquées au niveau du jeu de données sont propagées à tous les champs du jeu de données. Les étiquettes peuvent également être appliquées directement à des champs individuels (en-têtes de colonne) dans un jeu de données, sans propagation.

Pour plus d’informations sur les étiquettes d’utilisation des données disponibles dans [!DNL Experience Platform] et sur les stratégies d’utilisation qu’elles représentent, voir le guide sur les étiquettes [d’utilisation des données](reference.md)prises en charge.

## Héritage d’étiquette pour les segments d’audience

Tous les segments d’audience créés par [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) héritent des étiquettes d’utilisation des jeux de données correspondants. Cela permet aux applications créées sur [!DNL Experience Platform] (par exemple [!DNL Real-time Customer Data Platform]) de fournir une application automatique de la stratégie d’utilisation des données lors de l’activation de segments vers des destinations.

Outre l’héritage d’étiquettes au niveau des jeux de données, les segments héritent par défaut de tous les libellés au niveau des champs de leurs jeux de données associés. Selon la manière dont votre application [!DNL Platform]basée sur le trafic des segments est utilisée, vous pouvez éventuellement spécifier les champs utilisés, ce qui empêche le segment d’hériter des libellés des champs exclus.

Pour plus d&#39;informations sur le fonctionnement de l&#39;application automatique dans le CDP en temps réel, consultez l&#39;aperçu [de la gouvernance des données CDP en temps réel](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Étapes suivantes

Maintenant que vous avez introduit des étiquettes d’utilisation des données, vous pouvez continuer à lire le guide [d’](user-guide.md) utilisateur pour savoir comment gérer les étiquettes dans l’ [!DNL Experience Platform] interface utilisateur. Pour connaître les étapes de gestion des étiquettes à l’aide des API, voir la section appropriée du guide [du développeur](../../catalog/api/labels.md)Catalog Service.