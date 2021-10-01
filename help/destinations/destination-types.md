---
keywords: destinations;destination;types de destinations
title: Types et catégories de destination
seo-title: Destination types and categories
description: Découvrez les différents types et catégories de destinations dans Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 5a6f14ba65584a6bd61d62c4fb0b46e8f9e8e96d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 45%

---

# Types et catégories de destination

Lisez cette page pour comprendre les différents types et catégories de destinations Adobe Experience Platform.

## Types de destinations

Dans Adobe Experience Platform, nous faisons la distinction entre deux types de destinations : les connexions et les extensions. Il existe deux types de destinations de connexion : les destinations d’exportation de profils et les destinations d’exportation de segments.

![Types de destinations](./assets/destination-types/types-of-destinations.png)

## Connexions {#connections}

**[!UICONTROL Les destinations d’]** exportation de profils et d’ **[!UICONTROL exportation de segments en flux continu dans Adobe Experience Platform capturent les données d’événement, les combinent à d’autres sources de données pour former le profil client en temps]** réel [ ](../profile/home.md), appliquent la segmentation et exportent les segments et les profils qualifiés vers les destinations.

## Destinations d’exportation de profils

Les destinations d’exportation de profils reçoivent des données brutes, souvent avec l’adresse électronique comme clé Principale. Experience Platform prend actuellement en charge deux types de destinations d’exportation de profils :

* [Destinations d’exportation de profils en flux continu](#streaming-profile-export)
* [Destinations basées sur des fichiers](#file-based)

### Destinations d’exportation de profils en flux continu {#streaming-profile-export}

Les destinations d’exportation de profils en flux continu reçoivent des données de segment et de profil en tant que flux de données Experience Platform. [Amazon ](catalog/cloud-storage/amazon-kinesis.md) Kinesisand et  [Azure Event ](catalog/cloud-storage/azure-event-hubs.md) Hub sont des exemples de destinations de ce type.

### Destinations basées sur des fichiers {#file-based}

Les destinations basées sur des fichiers reçoivent des fichiers `.csv` contenant des profils et/ou des attributs. [Amazon S3](catalog/cloud-storage/amazon-s3.md) est un exemple de destination où vous pouvez déposer des fichiers contenant des exportations de profils.

## Destinations d’exportation de segments en flux continu

Les destinations d’exportation de segments reçoivent des données de segment Experience Platform. Ces destinations utilisent des identifiants de segment ou d’utilisateur. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md) et  [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) sont des exemples de ces destinations.

## Destinations d’exportation de profils et de segments - Présentation vidéo

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensions {#extensions}

Platform tire parti de la puissance et de la flexibilité de la gestion des balises, ce qui vous permet de configurer des extensions de balise dans l’interface utilisateur de la collecte de données.

>[!TIP]
>
>Pour plus d’informations sur les extensions de balise, y compris les cas d’utilisation et la manière de les trouver dans l’interface, consultez la [présentation des extensions de balise](./catalog/launch-extensions/overview.md).

Les extensions de balise transfèrent les données d’événement brutes à plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](./catalog/personalization/gainsight.md) ou l’[extension de voix du client Confirmit](./catalog/voice/confirmit-digital-feedback.md).

![Comparaison des extensions de balise avec d’autres destinations](./assets/common/launch-and-other-destinations.png)

## Utilisation des connexions et des extensions

En tant que professionnel du marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’utiliser un profil client centralisé complet ou un segment client pour l’activation. Par exemple, utilisez des connexions si vous assemblez les données comportementales d’un système d’analyse et des données de gestion de la relation client chargées, afin de qualifier un utilisateur pour un segment donné avant de lui envoyer un message personnalisé.

Les extensions s’avèrent utiles lorsque des données d’événement sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

## Catégories de destination

Les connexions et les extensions du [catalogue des destinations](https://platform.adobe.com/destination/catalog) sont regroupées par catégorie de destination (**Publicité**, **Stockage cloud**, **Plateformes d&#39;enquêtes**, **Marketing par e-mail**, etc.), selon l&#39;action marketing qu&#39;elles vous aident à réaliser. Pour plus d’informations sur chaque catégorie, ainsi que sur les destinations incluses dans chaque catégorie, consultez la [documentation du catalogue des destinations](./catalog/overview.md).

![Catégories de destination](./assets/destination-types/destination-categories-menu.png)
