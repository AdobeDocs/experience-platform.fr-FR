---
keywords: Experience Platform;accueil;rubriques populaires;gouvernance des données;api de libellé d’utilisation des données;api policy service;présentation des libellés d’utilisation des données
solution: Experience Platform
title: Présentation des libellés d’utilisation des données
description: Découvrez comment les libellés d’utilisation des données sont utilisés pour appliquer la conformité en matière de gouvernance des données dans Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
TQID: https://experienceleague.adobe.com/7pzsy2I5tNQP1s3QxXKIzBiijHA4BkicuBph0kX6Uy8
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: b572b7ff-a413-4173-b2b4-d7d3874f1b9b
  - id: b784da9a-7978-4766-bf1f-5ab2b23d894a
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 830
ht-degree: 88%

---

# Présentation des libellés d’utilisation des données {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Contrôler l’accès aux données sensibles et protégées"
>abstract="<h2>Description</h2><p>Contrôlez l’accès à des attributs et/ou segments de données spécifiques afin de concevoir des workflows flexibles pour les différentes personnes et équipes qui élaborent les cas d’utilisation d’Experience Platform.</p>"

Adobe Experience Platform vous permet d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des [politiques de gouvernance des données](../policies/overview.md) et des [politiques de contrôle d’accès](../../access-control/abac/ui/policies.md) associées.

Ce document offre une présentation des libellés d’utilisation des données dans [!DNL Experience Platform].

## Comprendre les libellés d’utilisation des données

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des politiques de gouvernance qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les bonnes pratiques recommandent de libeller les données dès qu’elles sont ingérées dans [!DNL Experience Platform], ou dès que les données sont disponibles pour une utilisation dans [!DNL Experience Platform].

Les libellés d’utilisation des données appliqués au niveau du jeu de données sont propagés à tous les champs du jeu de données. Vous pouvez également appliquer les libellés directement sur des champs individuels (en-têtes de colonne) d’un jeu de données, sans propagation.

[!DNL Experience Platform] fournit plusieurs libellés d’utilisation des données « principaux » et prêts à l’emploi, qui couvrent une grande variété de restrictions fréquentes applicables à la gouvernance des données. Pour plus d’informations sur ces libellés et sur les politiques de gouvernance qu’ils représentent, consultez le guide sur les [principaux libellés d’utilisation des données](reference.md).

Outre les libellés fournis par Adobe, vous pouvez également définir vos propres libellés personnalisés pour votre entreprise. Pour plus d’informations, consultez la section sur la [gestion des libellés](#manage-labels).

## Héritage de libellé pour les segments d’audience

Tous les segments d’audience créés par le [service de segmentation d’Adobe Experience Platform](../../segmentation/home.md) héritent des libellés d’utilisation de leurs jeux de données correspondants. Cela permet à Experience Platform d’appliquer automatiquement la politique lors de l’activation de segments vers des destinations.

Outre l’héritage de libellés au niveau des jeux de données, les segments héritent par défaut de tous les libellés au niveau des champs de leurs jeux de données associés. Par conséquent, vous pouvez identifier plus facilement les attributs à exclure de vos segments et les empêcher d’hériter des libellés de champs exclus.

Pour plus d’informations sur le fonctionnement de l’application automatique dans Experience Platform, consultez la présentation de l’[&#x200B; application automatique des politiques &#x200B;](../enforcement/auto-enforcement.md).

### Héritage des contrôles d’exportation de données d’Adobe Audience Manager

[!DNL Experience Platform] permet de partager des segments avec Adobe Audience Manager. Les contrôles d’exportation de données appliqués aux segments d’Audience Manager sont convertis en libellés équivalents et en actions marketing reconnues par la gouvernance des données [!DNL Experience Platform].

Pour savoir comment des contrôles d‘exportation de données spécifiques se mappent aux libellés d’utilisation des données dans [!DNL Experience Platform], consultez la [documentation sur Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aam-data-export-control-in-aep).

## Gestion des libellés d’utilisation des données dans [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instructions"
>abstract="<ul><li>Étiquetez et classez les champs et segments XDM dont vous souhaitez restreindre l’accès.</li><li>Étiquetez les rôles et définissez les restrictions applicables aux membres de ce rôle.</li><li>Créez des stratégies et associez les libellés sur les objets libellés, tels que les champs et les segments XDM, aux libellés sur les rôles. Si les libellés correspondent, un accès autorisé ou restreint peut être défini.</li></ul>"

Vous pouvez gérer les libellés d’utilisation des données à l’aide des API [!DNL Experience Platform] ou de l’interface utilisateur. Consultez les sous-sections ci-dessous pour plus de détails sur chaque option.

### Utilisation de l’interface utilisateur

L’espace de travail **[!UICONTROL Politiques]** de l’interface utilisateur de [!DNL Experience Platform] vous permet d’afficher et de gérer les libellés personnalisés et principaux de votre entreprise. Utilisez l’espace de travail **[!UICONTROL Schémas]** pour [appliquer des libellés à vos schémas de modèle de données d’expérience (XDM)](../../xdm/tutorials/labels.md) ou découvrez comment [créer et gérer des libellés personnalisés dans l’interface utilisateur **[!UICONTROL Politiques]**](./user-guide.md) dans le guide d’utilisation des libellés d’utilisation des données.

>[!IMPORTANT]
>
>Les libellés ne peuvent plus être appliqués aux champs au niveau du jeu de données. Ce workflow a été abandonné au profit de l’application des libellés au niveau du schéma. Les libellés précédemment appliqués au niveau de l’objet du jeu de données seront toujours pris en charge par l’interface utilisateur d’Experience Platform jusqu’au 31 mai 2024. Pour garantir la cohérence de vos libellés sur tous les schémas, les libellés précédemment attachés aux champs au niveau du jeu de données doivent être migrés au niveau du schéma par vous-même au cours de l’année à venir. Voir la section sur la [migration des libellés précédemment appliqués](../e2e.md#migrate-labels) pour obtenir des instructions sur la manière de procéder.

### Utilisation des API

Le point d’entrée `/labels` de l’[API Policy Service](https://www.adobe.io/experience-platform-apis/references/policy-service/) vous permet de gérer par programmation les libellés d’utilisation des données, y compris la création de libellés personnalisés. Pour plus d’informations, consultez le [guide des points d’entrée des libellés](../api/labels.md).

L’[API Dataset Service](https://www.adobe.io/experience-platform-apis/references/dataset-service/) est utilisée pour gérer les libellés des jeux de données et des champs. Pour plus d’informations, consultez le guide sur la [gestion des libellés de jeux de données](./dataset-api.md).

## Étapes suivantes

Ce document vous a présenté les libellés d’utilisation des données et leur rôle dans le cadre de la gouvernance des données. Reportez-vous à la documentation référencée tout au long de ce guide pour en savoir plus sur la gestion des libellés dans [!DNL Experience Platform].
