---
keywords: destinations ; destination ; types de destination
title: Types et catégories de destination
seo-title: Destination types and categories
description: Découvrez les différents types et catégories de destinations dans Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: a7c36f1a157b6020fede53e5c1074d966f26cf3d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 45%

---

# Types et catégories de destination

Read this page to understand the different types and categories of Adobe Experience Platform destinations.

## Types de destinations

Dans Adobe Experience Platform, nous distinguons deux types de destination : les connexions et les extensions. Il existe deux types de destinations de connexion : les destinations d’exportation de profils et les destinations d’exportation de segments.

![Types de destinations](./assets/destination-types/types-of-destinations.png)

## Connexions {#connections}

**[!UICONTROL Exportation de profil]** et **[!UICONTROL Exportation du segment de diffusion]** destinations dans les données d’événement de capture Adobe Experience Platform, combinez-les avec d’autres sources de données pour former la [Profil du client en temps réel](../profile/home.md), appliquez la segmentation et exportez des segments et des profils qualifiés vers des destinations.

## Destinations d’exportation de profils

Les destinations d’exportation de profil reçoivent des données brutes, souvent avec une adresse électronique comme clé primaire. Experience Platform currently supports two types of profile export destinations:

* [Destinations d’exportation de profil de diffusion](#streaming-profile-export)
* [Destinations basées sur des fichiers](#file-based)

### Destinations d’exportation de profil de diffusion {#streaming-profile-export}

Streaming profile export destinations receive segment and profile data as Experience Platform data streams. [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md) et [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md) sont des exemples de ces destinations.

### Destinations basées sur des fichiers {#file-based}

Les destinations basées sur des fichiers reçoivent `.csv` contenant des profils et/ou des attributs. [Amazon S3](catalog/cloud-storage/amazon-s3.md) is an example of destination where you can deposit files containing profile exports.

## Destinations d’exportation des segments de flux {#streaming-destinations}

Segment export destinations receive Experience Platform segment data. These destinations use segment IDs or user IDs. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)et sont des exemples de ces destinations.

## Exportation de profils et destinations d’exportation de segments - Présentation vidéo {#video}

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensions {#extensions}

Platform leverages the power and flexibility of tag management, allowing you to configure tag extensions in the Data Collection UI.

>[!TIP]
>
>Pour plus d’informations sur les extensions de balises, y compris les cas d’utilisation et la façon de les trouver dans l’interface, consultez la section [présentation des extensions de balises](./catalog/launch-extensions/overview.md).

Les extensions de balises transmettent les données d’événements bruts à plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](./catalog/personalization/gainsight.md) ou l’[extension de voix du client Confirmit](./catalog/voice/confirmit-digital-feedback.md).

![Extensions de balises par rapport à d’autres destinations](./assets/common/launch-and-other-destinations.png)

## Utilisation des connexions et des extensions {#when-to-use}

En tant que professionnel du marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’utiliser un profil client centralisé complet ou un segment client pour l’activation. Par exemple, utilisez des connexions si vous assemblez les données comportementales d’un système d’analyse et des données de gestion de la relation client chargées, afin de qualifier un utilisateur pour un segment donné avant de lui envoyer un message personnalisé.

Les extensions s’avèrent utiles lorsque des données d’événement sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

## Catégories de destination {#categories}

Les connexions et les extensions dans le fichier [catalogue de destinations](https://platform.adobe.com/destination/catalog) sont regroupées par catégorie de destination (**Publicité**, **Stockage cloud**, **Plates-formes d&#39;enquête**, **Marketing par e-mail**, etc.), selon l&#39;action marketing qu&#39;ils vous aident à réaliser. Pour plus d’informations sur chaque catégorie, ainsi que sur les destinations incluses dans chaque catégorie, consultez la [documentation du catalogue des destinations](./catalog/overview.md).

![Catégories de destination](./assets/destination-types/destination-categories-menu.png)
