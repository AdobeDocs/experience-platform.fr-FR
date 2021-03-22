---
keywords: destinations;destination;types de destination
title: Types et catégories de destination
seo-title: Types et catégories de destination
description: Découvrez les différents types et catégories de destinations dans Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 64%

---


# Types et catégories de destination

Lisez cette page pour comprendre les différents types et catégories de destinations Adobe Experience Platform.

## Types de destinations

Dans Adobe Experience Platform, nous faisons la distinction entre deux types de destination : les connexions et les extensions. Il existe deux types de destinations de connexion : les destinations d’exportation de profils et les destinations d’exportation de segments.

![Types de destinations](./assets/destination-types/types-of-destinations.png)

## Connexions {#connections}

**[!UICONTROL Profil]** Exportations et  **[!UICONTROL segments]** Exportations dans Adobe Experience Platform capture les données du événement, les combine avec d’autres sources de données pour former le Profil [ client en temps ](../profile/home.md)réel, appliquer la segmentation et exporter des segments et des profils qualifiés vers des destinations.

## Destinations d’exportation de profils

Les destinations d’exportation de profils génèrent un fichier contenant des profils et/ou des attributs. Ces destinations utilisent des données brutes, souvent avec l’adresse électronique comme clé primaire. La [destination de stockage dans le cloud Amazon S3](./catalog/cloud-storage/amazon-s3.md) est un exemple de destination où vous pouvez déposer des fichiers contenant des exportations de profils.

## Destinations d’exportation de segments

Les destinations d’exportation de segments envoient les profils et les segments pour lesquels ils sont qualifiés vers des plateformes de destination. Ces destinations utilisent des identifiants de segment ou d’utilisateur. Les destinations publicitaires telles que [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) ou [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) sont des exemples de ces types de destinations.

## Destinations d’exportation de segments et de profils : présentation vidéo

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Extensions {#extensions}

Platform tire parti de la puissance et de la flexibilité d&#39;Adobe Experience Platform Launch pour inclure des extensions de Platform launch dans l&#39;interface Platform.

>[!TIP]
>
>Pour plus d&#39;informations sur les extensions Adobe Experience Platform Launch, y compris les cas d&#39;utilisation et la façon de les trouver dans l&#39;interface, consultez la [présentation des extensions Adobe Experience Platform Launch](./catalog/launch-extensions/overview.md).

Les extensions de platform launch transfèrent les données de événement brutes vers plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](./catalog/personalization/gainsight.md) ou l’[extension de voix du client Confirmit](./catalog/voice/confirmit-digital-feedback.md).

![Comparaison entre les extensions d’Experience Platform Launch et d’autres destinations](./assets/common/launch-and-other-destinations.png)

## Utilisation des connexions et des extensions

En tant que professionnel du marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’utiliser un profil client centralisé complet ou un segment client pour l’activation. Par exemple, utilisez des connexions si vous assemblez les données comportementales d’un système d’analyse et des données de gestion de la relation client chargées, afin de qualifier un utilisateur pour un segment donné avant de lui envoyer un message personnalisé.

Les extensions s’avèrent utiles lorsque des données d’événement sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

## Catégories de destination

Les connexions et extensions du catalogue de destinations [destinations](https://platform.adobe.com/destination/catalog) sont regroupées par catégorie de destination (**Publicité**, **enregistrement de cloud**, **plateformes de Questionnaire**, **Marketing par courriel**, etc.), en fonction de l&#39;action marketing qu&#39;ils vous aident à réaliser. Pour plus d’informations sur chaque catégorie, ainsi que sur les destinations incluses dans chaque catégorie, consultez la [documentation du catalogue des destinations](./catalog/overview.md).

![Catégories de destination](./assets/destination-types/destination-categories-menu.png)

