---
keywords: destinations;destination;types de destinations
title: Types et catégories de destination
description: Découvrez les différents types et catégories de destinations dans Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
TQID: https://experienceleague.adobe.com/ASiVeC74mG6OUPqVdq07b1901ZUKixb4zii8yIu2dAY
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
subfeature_v2:
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
  - id: ae2cba0e-54f2-464b-a3b3-ad371e8a886a
  - id: b784da9a-7978-4766-bf1f-5ab2b23d894a
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
  - id: d3f95e25-a50e-4fd0-bc23-9a22409a183b
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1c
  - id: e8c2a8db-c24b-44d9-ab8e-a8bc03acf6b1
  - id: f6ff4d13-7b5c-4533-8556-95e76673d4cb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: beb7a3c1-66ab-4786-b879-7621375b3c40
  - id: c18d9e03-ac7d-4811-9c92-3e92ddc70ade
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 841
ht-degree: 48%

---

# Types et catégories de destination

Lisez cette page pour comprendre les différents types et catégories de destinations [!DNL Adobe Experience Platform].

## Types de destinations {#destination-types}

Dans [!DNL Adobe Experience Platform], nous faisons la distinction entre différents types de destinations : connexions, exportations de jeux de données et extensions. Il existe plusieurs types de destinations de connexion, ce qui vous permet d’exporter des données vers des destinations basées sur des API, des destinations de réseaux sociaux, des plateformes CRM, etc.

Enfin, les connexions peuvent également être distinguées entre les destinations publiques disponibles dans toutes les organisations du catalogue des destinations, et les destinations privées que [!DNL Real-Time CDP] clients Ultimate peuvent créer pour répondre à leurs cas d’utilisation d’exportation spécifiques.

>[!BEGINSHADEBOX]

Diagramme ![Types de destinations).](./assets/destination-types/types-of-destinations-no-highlight.png "Diagramme Types de destinations."){zoomable="yes"}

>[!ENDSHADEBOX]

## Connexions {#connections}

**[!UICONTROL Exportation de profils]**, **[!UICONTROL Exportation d’audiences en flux continu]** et **[!DNL Edge Personalization]** destinations dans [!DNL Adobe Experience Platform] capturent des données d’événement, les combinent avec d’autres sources de données pour former le [Profil client en temps réel](../profile/home.md), appliquent une segmentation et exportent des audiences et des profils qualifiés vers des destinations.

## Destinations d’exportation de profils {#profile-export}

Les destinations d’exportation de profils reçoivent des données brutes, souvent avec l’adresse e-mail comme clé primaire. Experience Platform prend actuellement en charge deux types de destinations d’exportation de profils :

* [Destinations de lot (basées sur des fichiers)](#file-based)
* [Destinations d’entreprise avancées (destinations d’exportation de profils de streaming)](#advanced-enterprise-destinations)

### Destinations d’entreprise avancées (destinations d’exportation de profils de streaming) {#advanced-enterprise-destinations}

>[!IMPORTANT]
>
>Les destinations d’entreprise avancées, ou destinations d’exportation de profil de diffusion en continu, sont disponibles uniquement pour les clients [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html).

Utilisez les connecteurs de données de destination d’entreprise avancés pour transmettre les profils Adobe [!DNL Real-Time Customer Data Platform] en temps quasi réel à des systèmes internes ou à des systèmes tiers à des fins de synchronisation des données, d’analyse et d’enrichissement des profils.

Ces destinations reçoivent des données d’audience et de profil en tant que flux de données Experience Platform.

Les destinations d’entreprise avancées sont les suivantes :

* [Destination de l’API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)
* [Streaming Snowflake](catalog/warehouses/snowflake.md)
* [Lot Snowflake](catalog/warehouses/snowflake-batch.md)

>[!NOTE]
>
>Les destinations Snowflake sont actuellement disponibles uniquement pour les clients américains. Si vous avez besoin d’un accès en dehors des États-Unis, contactez votre équipe de compte Adobe.

### Destinations de lot (basées sur des fichiers) {#file-based}

Les destinations basées sur des fichiers reçoivent des fichiers `.csv` contenant des profils et/ou des attributs. [Amazon S3](catalog/cloud-storage/amazon-s3.md) est un exemple de destination où vous pouvez exporter des fichiers contenant des exportations de profils.

## Destinations d’exportation d’audiences de diffusion en continu {#streaming-destinations}

Les destinations d’exportation d’audience reçoivent des données d’audience Experience Platform. Ces destinations utilisent des ID d’audience ou d’utilisateur. Les destinations publicitaires et sociales telles que [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)ou [Facebook](catalog/social/facebook.md) sont des exemples de ces destinations.

## Destinations de personnalisation Edge {#edge-personalization-destinations}

Les destinations de personnalisation Edge dans Experience Platform comprennent [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) et la [destination de personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md). En utilisant ces destinations, vous pouvez permettre à vos clients d’utiliser la personnalisation sur la même page et sur la page suivante.

En savoir plus sur la façon de [configurer des destinations de personnalisation pour la personnalisation de la même page et de la page suivante](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Destinations d’exportation de profils et d’audiences - présentation vidéo {#video}

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/33171?captions=fre_fr&quality=12)

## Types d’audiences exportées {#exported-audiences-types}

Vous pouvez exporter trois types d’audiences d’Experience Platform vers différentes destinations :

* Audiences de personnes
* Audiences de compte
* Audiences de prospects

En savoir plus sur les [différents types d’audiences](/help/segmentation/types/account-audiences.md#terminology).

Un symbole sur la carte de destination indique les types d’audiences que vous pouvez exporter vers chaque destination.

![Exemple de carte de destination avec des symboles indiquant les types d’audience pouvant être exportés.](/help/destinations/assets/destination-types/types-of-audiences.png "Exemple de carte de destination avec des symboles indiquant les types d’audience pouvant être exportés."){zoomable="yes"}


## Destinations d’exportation de jeux de données {#dataset-export-destinations}

Certaines destinations d’espace de stockage dans le catalogue des destinations prennent en charge les exportations de jeux de données. Utilisez ces destinations pour exporter des jeux de données brutes vers des emplacements d’espace de stockage.

En savoir plus sur la façon d’[exporter des jeux de données](/help/destinations/ui/export-datasets.md).

## Extensions {#extensions}

Experience Platform tire parti de la puissance et de la flexibilité de la gestion des balises, ce qui vous permet de configurer des extensions de balises dans l’interface utilisateur.

>[!TIP]
>
>Pour plus d’informations détaillées sur les extensions de balises, y compris les cas d’utilisation et la façon de les trouver dans l’interface, consultez la [Présentation des extensions de balises](./catalog/launch-extensions/overview.md).

Les extensions de balises transfèrent les données brutes des événements vers plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](./catalog/personalization/gainsight.md) ou l’[extension de voix du client Confirmit](./catalog/voice/confirmit-digital-feedback.md).

![Les extensions de balises par rapport aux autres destinations](./assets/common/launch-and-other-destinations.png)

## Utilisation des connexions et des extensions {#when-to-use}

En tant que spécialiste marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’utiliser un profil client centralisé complet ou une audience client pour l’activation. Utilisez, par exemple, des connexions si vous joignez des données comportementales à partir d’un système d’analyse avec des données CRM chargées afin de qualifier un utilisateur pour une audience donnée avant de lui diffuser un message personnalisé.

Les extensions s’avèrent utiles lorsque les données d’événement déclenchent une action ou effectuent une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

## Catégories de destination {#categories}

Les connexions et extensions du [catalogue des destinations](https://platform.adobe.com/destination/catalog) sont regroupées par catégorie de destination (**Publicité**, **Espace de stockage**, **Plateformes d’enquête**, **Marketing par e-mail**, etc.), selon l’action marketing qu’elles permettent de réaliser. Pour plus d’informations sur chaque catégorie, ainsi que sur les destinations incluses dans chaque catégorie, consultez la [documentation du catalogue des destinations](./catalog/overview.md).

![Catégories de destination mises en surbrillance dans la page du catalogue.](./assets/destination-types/destination-categories-menu.png "Catégories de destination mises en surbrillance dans la page du catalogue."){zoomable="yes"}
