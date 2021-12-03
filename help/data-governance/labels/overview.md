---
keywords: Experience Platform;accueil;rubriques populaires;gouvernance des données;api de libellé d’utilisation des données;api policy service;présentation des libellés d’utilisation des données
solution: Experience Platform
title: Présentation des libellés d’utilisation des données
topic-legacy: labels
description: La gouvernance des données d’Adobe Experience Platform vous permet d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d’utilisation des données associées. Ce document offre une présentation des libellés d’utilisation des données dans Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: ht
source-wordcount: '615'
ht-degree: 100%

---

# Présentation des libellés d’utilisation des données

La gouvernance des données d’Adobe Experience Platform vous permet d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d’utilisation des données associées.

Ce document offre une présentation des libellés d’utilisation des données dans [!DNL Experience Platform]. Avant de lire ce guide, consultez la [présentation de la gouvernance des données](../home.md) pour une introduction plus détaillée du cadre de la gouvernance des données.

## Comprendre les libellés d’utilisation des données

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les bonnes pratiques recommandent de libeller les données dès qu’elles sont ingérées dans [!DNL Experience Platform], ou dès que les données sont disponibles pour une utilisation dans [!DNL Platform].

Les libellés d’utilisation des données appliqués au niveau du jeu de données sont propagés à tous les champs du jeu de données. Vous pouvez également appliquer les libellés directement sur des champs individuels (en-têtes de colonne) d’un jeu de données, sans propagation.

[!DNL Platform] fournit plusieurs libellés d’utilisation des données « principaux » et prêts à l’emploi, qui couvrent une grande variété de restrictions fréquentes applicables à la gouvernance des données. Pour plus d’informations sur ces libellés et sur les stratégies d’utilisation qu’ils représentent, consultez le guide sur les [principaux libellés d’utilisation des données](reference.md).

Outre les libellés fournis par Adobe, vous pouvez également définir vos propres libellés personnalisés pour votre entreprise. Pour plus d’informations, consultez la section sur la [gestion des libellés](#manage-labels).

## Héritage de libellé pour les segments d’audience

Tous les segments d’audience créés par le [service de segmentation d’Adobe Experience Platform](../../segmentation/home.md) héritent des libellés d’utilisation de leurs jeux de données correspondants. Cela permet à Experience Platform d’appliquer automatiquement la stratégie d’utilisation des données lors de l’activation de segments vers des destinations.

Outre l’héritage de libellés au niveau des jeux de données, les segments héritent par défaut de tous les libellés au niveau des champs de leurs jeux de données associés. Par conséquent, vous pouvez identifier plus facilement les attributs à exclure de vos segments et les empêcher d’hériter des libellés de champs exclus.

Pour plus d’informations sur le fonctionnement de l’application automatique dans Platform, consultez la présentation de l’[application automatique des stratégies](../enforcement/auto-enforcement.md).

### Héritage des contrôles d’exportation de données d’Adobe Audience Manager

[!DNL Experience Platform] permet de partager des segments avec Adobe Audience Manager. Les contrôles d’exportation de données appliqués aux segments d’Audience Manager sont convertis en libellés équivalents et en actions marketing reconnues par la gouvernance des données [!DNL Experience Platform].

Pour savoir comment des contrôles d‘exportation de données spécifiques se mappent aux libellés d’utilisation des données dans [!DNL Platform], consultez la [documentation sur Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aam-data-export-control-in-aep).

## Gestion des libellés d’utilisation des données dans [!DNL Experience Platform] {#manage-labels}

Vous pouvez gérer les libellés d’utilisation des données à l’aide des API [!DNL Experience Platform] ou de l’interface utilisateur. Consultez les sous-sections ci-dessous pour plus de détails sur chaque option.

### Utilisation de l’interface utilisateur

L’espace de travail **[!UICONTROL Stratégies]** de l’interface utilisateur [!DNL Experience Platform] vous permet d’afficher et de gérer les libellés personnalisés et principaux de votre entreprise. L’espace de travail **[!DNL Datasets]** vous permet d’appliquer des libellés aux jeux de données et aux champs. Pour plus d’informations, reportez-vous au [guide d’utilisation des libellés](user-guide.md).

### Utilisation des API

Le point d’entrée `/labels` de l’[API Policy Service](https://www.adobe.io/experience-platform-apis/references/policy-service/) vous permet de gérer par programmation les libellés d’utilisation des données, y compris la création de libellés personnalisés. Pour plus d’informations, consultez le [guide des points d’entrée des libellés](../api/labels.md).

L’[API Dataset Service](https://www.adobe.io/experience-platform-apis/references/dataset-service/) est utilisée pour gérer les libellés des jeux de données et des champs. Pour plus d’informations, consultez le guide sur la [gestion des libellés de jeux de données](./dataset-api.md).

## Étapes suivantes

Ce document vous a présenté les libellés d’utilisation des données et leur rôle dans le cadre de la gouvernance des données. Reportez-vous à la documentation référencée tout au long de ce guide pour en savoir plus sur la gestion des libellés dans [!DNL Experience Platform].
