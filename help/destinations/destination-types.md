---
keywords: destinations;destination;types de destinations
title: Types et catégories de destination
description: Découvrez les différents types et catégories de destinations dans Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: c140e68467065d17f143850bfb8eefb3ac46443a
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 34%

---

# Types et catégories de destination

Lisez cette page pour comprendre les différents types et catégories de destinations Adobe Experience Platform.

## Types de destinations {#destination-types}

Dans Adobe Experience Platform, nous faisons la distinction entre deux types de destinations : les connexions et les extensions. Il existe deux types de destinations de connexion : les destinations d’exportation de profils et les destinations d’exportation de segments.

![Types de destinations](./assets/destination-types/types-of-destinations.png)

## Connexions {#connections}

**[!UICONTROL Exportation de profils]**, **[!UICONTROL Exportation de segments en flux continu]**, et **[!DNL Edge Personalization]** les destinations dans Adobe Experience Platform capturent les données d’événement, les combinent à d’autres sources de données pour former la variable [Real-time Customer Profile](../profile/home.md), appliquez une segmentation et exportez des segments et des profils qualifiés vers les destinations.

## Destinations d’exportation de profils {#profile-export}

Les destinations d’exportation de profils reçoivent des données brutes, souvent avec l’adresse électronique comme clé Principale. Experience Platform prend actuellement en charge deux types de destinations d’exportation de profils :

* [Destinations d’exportation de profils en flux continu (destinations d’entreprise)](#streaming-profile-export)
* [Destinations de lot (basées sur des fichiers)](#file-based)

### Destinations d’exportation de profils en flux continu (destinations d’entreprise) {#streaming-profile-export}

>[!IMPORTANT]
>
>Les destinations d’entreprise ou les destinations d’exportation de profils en continu sont disponibles pour [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) clients uniquement.

Utilisez les connecteurs de données de destination d’entreprise pour fournir des profils Adobe Real-time Customer Data Platform en temps quasi réel aux systèmes internes ou à d’autres systèmes tiers pour la synchronisation des données, l’analyse et d’autres cas d’utilisation d’enrichissement de profil.

Ces destinations reçoivent des données de segment et de profil en tant que flux de données Experience Platform.

Les destinations d’entreprise incluent :

* [Destination de l’API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Destinations de lot (basées sur des fichiers) {#file-based}

Les destinations basées sur des fichiers reçoivent `.csv` fichiers contenant des profils et/ou des attributs. [Amazon S3](catalog/cloud-storage/amazon-s3.md) est un exemple de destination où vous pouvez exporter des fichiers contenant des exportations de profils.

## Destinations d’exportation de segments en flux continu {#streaming-destinations}

Les destinations d’exportation de segments reçoivent des données de segment Experience Platform. Ces destinations utilisent des identifiants de segment ou d’utilisateur. Destinations publicitaires et sociales telles que [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)ou [Facebook](catalog/social/facebook.md) sont des exemples de ces destinations.

## Destinations de personnalisation Edge {#edge-personalization-destinations}

Destinations de personnalisation Edge dans Experience Platform : [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) et le [Destination de personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md). En utilisant ces destinations, vous pouvez activer des cas d’utilisation de personnalisation de la même page et de la page suivante pour vos clients.

En savoir plus sur la manière de procéder [configuration des destinations de personnalisation pour la personnalisation de la même page et de la page suivante](/help/destinations/ui/configure-personalization-destinations.md).

## Destinations d’exportation de profils et de segments - Présentation vidéo {#video}

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## (Version bêta) Destinations d’exportation de jeux de données {#dataset-export-destinations}

Certaines destinations de stockage dans le cloud dans le catalogue des destinations prennent en charge les exportations de jeux de données. Utilisez ces destinations pour exporter des jeux de données bruts vers des emplacements de stockage dans le cloud.

En savoir plus sur la manière de procéder [exportation de jeux de données](/help/destinations/ui/export-datasets.md).

## Extensions {#extensions}

Platform tire parti de la puissance et de la flexibilité de la gestion des balises, ce qui vous permet de configurer des extensions de balises dans l’interface utilisateur.

>[!TIP]
>
>Pour plus d’informations sur les extensions de balises, y compris les cas d’utilisation et la manière de les trouver dans l’interface, voir [Présentation des extensions de balise](./catalog/launch-extensions/overview.md).

Les extensions de balise transfèrent les données d’événement brutes à plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](./catalog/personalization/gainsight.md) ou l’[extension de voix du client Confirmit](./catalog/voice/confirmit-digital-feedback.md).

![Comparaison des extensions de balise avec d’autres destinations](./assets/common/launch-and-other-destinations.png)

## Utilisation des connexions et des extensions {#when-to-use}

En tant que professionnel du marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’exploiter un profil client centralisé complet ou un segment de client pour l’activation. Par exemple, utilisez des connexions si vous assemblez les données comportementales d’un système d’analyse et des données de gestion de la relation client chargées, afin de qualifier un utilisateur pour un segment donné avant de lui envoyer un message personnalisé.

Les extensions s’avèrent utiles lorsque des données d’événement sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

## Catégories de destination {#categories}

Les connexions et les extensions dans le [destinations](https://platform.adobe.com/destination/catalog) sont regroupées par catégorie de destination (**Publicité**, **Stockage dans le cloud**, **Plateformes d&#39;enquêtes**, **Marketing par e-mail**, etc.), en fonction de l’action marketing qu’ils vous aident à réaliser. Pour plus d’informations sur chaque catégorie, ainsi que sur les destinations incluses dans chaque catégorie, consultez la [documentation du catalogue des destinations](./catalog/overview.md).

![Catégories de destination](./assets/destination-types/destination-categories-menu.png)
