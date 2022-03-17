---
keywords: destinations;destination;types de destinations
title: Types et catégories de destination
seo-title: Destination types and categories
description: Découvrez les différents types et catégories de destinations dans Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 08c6c2716b88180b1eb290663117e6da2d8641f0
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 45%

---

# Types et catégories de destination

Lisez cette page pour comprendre les différents types et catégories de destinations Adobe Experience Platform.

## Types de destinations

Dans Adobe Experience Platform, nous faisons la distinction entre deux types de destinations : les connexions et les extensions. Il existe deux types de destinations de connexion : les destinations d’exportation de profils et les destinations d’exportation de segments.

![Types de destinations](./assets/destination-types/types-of-destinations.png)

## Connexions {#connections}

**[!UICONTROL Exportation de profils]** et **[!UICONTROL Exportation de segments en flux continu]** les destinations dans Adobe Experience Platform capturent les données d’événement, les combinent à d’autres sources de données pour former la variable [Real-time Customer Profile](../profile/home.md), appliquez une segmentation et exportez des segments et des profils qualifiés vers les destinations.

## Destinations d’exportation de profils

Les destinations d’exportation de profils reçoivent des données brutes, souvent avec l’adresse électronique comme clé Principale. Experience Platform prend actuellement en charge deux types de destinations d’exportation de profils :

* [Destinations d’exportation de profils en flux continu](#streaming-profile-export)
* [Destinations de lot (basées sur des fichiers)](#file-based)

### Destinations d’exportation de profils en flux continu {#streaming-profile-export}

Les destinations d’exportation de profils en flux continu reçoivent des données de segment et de profil en tant que flux de données Experience Platform. [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md) et [Centre d’événements Azure](catalog/cloud-storage/azure-event-hubs.md) sont des exemples de ces destinations.

### Destinations de lot (basées sur des fichiers) {#file-based}

Les destinations basées sur des fichiers reçoivent `.csv` fichiers contenant des profils et/ou des attributs. [Amazon S3](catalog/cloud-storage/amazon-s3.md) est un exemple de destination où vous pouvez exporter des fichiers contenant des exportations de profils.

## Destinations d’exportation de segments en flux continu {#streaming-destinations}

Les destinations d’exportation de segments reçoivent des données de segment Experience Platform. Ces destinations utilisent des identifiants de segment ou d’utilisateur. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)et sont des exemples de ces destinations.

## Destinations d’exportation de profils et de segments - Présentation vidéo {#video}

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensions {#extensions}

Platform tire parti de la puissance et de la flexibilité de la gestion des balises, ce qui vous permet de configurer des extensions de balise dans l’interface utilisateur de la collecte de données.

>[!TIP]
>
>Pour plus d’informations sur les extensions de balises, y compris les cas d’utilisation et la manière de les trouver dans l’interface, voir [Présentation des extensions de balise](./catalog/launch-extensions/overview.md).

Les extensions de balise transfèrent les données d’événement brutes à plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](./catalog/personalization/gainsight.md) ou l’[extension de voix du client Confirmit](./catalog/voice/confirmit-digital-feedback.md).

![Comparaison des extensions de balise avec d’autres destinations](./assets/common/launch-and-other-destinations.png)

## Utilisation des connexions et des extensions {#when-to-use}

En tant que professionnel du marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’utiliser un profil client centralisé complet ou un segment client pour l’activation. Par exemple, utilisez des connexions si vous assemblez les données comportementales d’un système d’analyse et des données de gestion de la relation client chargées, afin de qualifier un utilisateur pour un segment donné avant de lui envoyer un message personnalisé.

Les extensions s’avèrent utiles lorsque des données d’événement sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

## Catégories de destination {#categories}

Les connexions et les extensions dans le [destinations](https://platform.adobe.com/destination/catalog) sont regroupées par catégorie de destination (**Publicité**, **Stockage dans le cloud**, **Plateformes d&#39;enquêtes**, **Marketing par e-mail**, etc.), en fonction de l’action marketing qu’ils vous aident à réaliser. Pour plus d’informations sur chaque catégorie, ainsi que sur les destinations incluses dans chaque catégorie, consultez la [documentation du catalogue des destinations](./catalog/overview.md).

![Catégories de destination](./assets/destination-types/destination-categories-menu.png)
