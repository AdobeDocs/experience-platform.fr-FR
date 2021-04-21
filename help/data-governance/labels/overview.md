---
keywords: Experience Platform ; accueil ; rubriques populaires ; gouvernance des données ; api de l’étiquette d’utilisation des données ; api du service de stratégie ; étiquettes d’utilisation des données présentation
solution: Experience Platform
title: Présentation des étiquettes d’utilisation des données
topic-legacy: labels
description: La gouvernance des données Adobe Experience Platform vous permet d’appliquer des étiquettes d’utilisation des données aux jeux de données et aux champs, en les classant par catégorie selon les stratégies d’utilisation des données associées. Ce document présente un aperçu des étiquettes d’utilisation des données dans l’Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 14%

---

# Présentation des libellés d’utilisation des données

Adobe Experience Platform [!DNL Data Governance] vous permet d’appliquer des étiquettes d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d’utilisation des données associées.

Ce document fournit un aperçu des étiquettes d&#39;utilisation des données dans [!DNL Experience Platform]. Avant de lire ce guide, veuillez consulter la [Présentation de la gouvernance des données](../home.md) pour une présentation plus robuste du cadre de gouvernance des données.

## Comprendre les libellés d’utilisation des données

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les meilleures pratiques encouragent l’étiquetage des données dès qu’elles sont ingérées dans [!DNL Experience Platform] ou dès que les données sont disponibles pour être utilisées dans [!DNL Platform].

Les libellés d’utilisation des données appliqués au niveau du jeu de données sont propagés à tous les champs du jeu de données. Vous pouvez également appliquer les libellés directement sur des champs individuels (en-têtes de colonne) d’un jeu de données, sans propagation.

[!DNL Platform] fournit plusieurs étiquettes d’utilisation de données &quot;de base&quot; prêtes à l’emploi, qui couvrent une grande variété de restrictions courantes applicables à la gouvernance des données. Pour plus d&#39;informations sur ces étiquettes et les stratégies d&#39;utilisation qu&#39;elles représentent, consultez le guide intitulé [les étiquettes d&#39;utilisation des données de base](reference.md).

Outre les étiquettes fournies par Adobe, vous pouvez également définir vos propres étiquettes personnalisées pour votre entreprise. Pour plus d&#39;informations, consultez la section [gestion des étiquettes](#manage-labels).

## Héritage d’étiquette pour les segments d’audience

Tous les segments d’audience créés par [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) héritent des étiquettes d’utilisation de leurs jeux de données correspondants. Cela permet à l’Experience Platform d’appliquer automatiquement la stratégie d’utilisation des données lors de l’activation de segments vers des destinations.

Outre l’héritage d’étiquettes au niveau des jeux de données, les segments héritent par défaut de tous les libellés au niveau des champs de leurs jeux de données associés. Par conséquent, vous pouvez identifier plus facilement les attributs à exclure de vos segments et les empêcher d’hériter des étiquettes des champs exclus.

Pour plus d&#39;informations sur le fonctionnement de l&#39;application automatique dans Platform, consultez l&#39;aperçu de [l&#39;application automatique de la stratégie](../enforcement/auto-enforcement.md).

### Héritage des contrôles d&#39;exportation des données Adobe Audience Manager

[!DNL Experience Platform] permet de partager des segments avec Adobe Audience Manager. Les contrôles d&#39;exportation de données appliqués aux segments d&#39;Audience Manager sont convertis en étiquettes équivalentes et en actions marketing reconnues par [!DNL Experience Platform] [!DNL Data Governance].

Pour savoir comment des contrôles d&#39;exportation de données spécifiques correspondent aux étiquettes d&#39;utilisation des données dans [!DNL Platform], consultez la [documentation sur l&#39;Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gestion des étiquettes d&#39;utilisation des données dans [!DNL Experience Platform] {#manage-labels}

Vous pouvez gérer les libellés d’utilisation des données à l’aide des API [!DNL Experience Platform] ou de l’interface utilisateur. Consultez les sous-sections ci-dessous pour plus de détails sur chacun d&#39;eux.

### Utilisation de l’interface utilisateur

L&#39;espace de travail **[!UICONTROL Stratégies]** de l&#39;interface utilisateur [!DNL Experience Platform] vous permet de vue et de gérer les étiquettes personnalisées et de base de votre entreprise. L&#39;espace de travail **[!DNL Datasets]** vous permet d&#39;appliquer des étiquettes aux jeux de données et aux champs. Pour plus d&#39;informations, consultez le [guide de l&#39;utilisateur des étiquettes](user-guide.md).

### Utilisation des API

Le point de terminaison `/labels` de l&#39;API [Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) permet de gérer par programmation les étiquettes d&#39;utilisation des données, y compris la création d&#39;étiquettes personnalisées. Pour plus d&#39;informations, consultez le [guide du point de terminaison des étiquettes](../api/labels.md).

L&#39;[API du service de dataset](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) est utilisée pour gérer les étiquettes des jeux de données et des champs. Pour plus d&#39;informations, consultez le guide [gestion des étiquettes de jeux de données](./dataset-api.md).

## Étapes suivantes

Ce document présente les étiquettes d’utilisation des données et leur rôle dans le cadre de la gouvernance des données. Reportez-vous à la documentation à laquelle est lié ce guide pour en savoir plus sur la gestion des étiquettes dans [!DNL Experience Platform].
