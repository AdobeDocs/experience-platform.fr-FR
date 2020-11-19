---
keywords: destinations;destination;destination types
title: Types et catégories de destinations
seo-title: Types et catégories de destinations
description: 'Dans la plate-forme de données client en temps réel, les destinations d’exportation de Profil/segment capturent les données de événement, les combinent à d’autres sources de données, appliquent la segmentation et exportent des segments et des profils qualifiés vers les destinations. Les extensions Experience Platform Launch transfèrent des données de événement brutes vers plusieurs types de destinations. '
seo-description: Dans la plate-forme de données client en temps réel, les destinations d’exportation de Profil/segment capturent les données de événement, les combinent à d’autres sources de données, appliquent la segmentation et exportent des segments et des profils qualifiés vers les destinations. Les extensions Experience Platform Launch transfèrent des données de événement brutes vers plusieurs types de destinations.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 61%

---


# Types et catégories de destinations

Lisez cette page pour comprendre les différents types et catégories de destination des plateformes de données clientes en temps réel.

## Types de destinations

Dans la plate-forme de données client en temps réel, nous distinguons deux types de destination : les connexions et les extensions. Il existe deux types de destinations de connexion : les destinations d’exportation de profils et les destinations d’exportation de segments.

![Types de destinations](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Connexions {#connections}

**[!UICONTROL Exportation]** de profil et **[!UICONTROL segmentation Exportation]** de destinations dans la plate-forme de données clientes en temps réel, capture des données de événement, les combine avec d’autres sources de données pour former le profil [client en temps](/help/profile/home.md)réel, appliquer la segmentation et exporter des segments et des profils qualifiés vers les destinations.

<br> 

#### Destinations d’exportation de profils

Les destinations d’exportation de profils génèrent un fichier contenant des profils et/ou des attributs. Ces destinations utilisent des données brutes, souvent avec l’adresse électronique comme clé primaire. La [destination de stockage dans le cloud Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) est un exemple de destination où vous pouvez déposer des fichiers contenant des exportations de profils.

#### Destinations d’exportation de segments

Les destinations d’exportation de segments envoient les profils et les segments pour lesquels ils sont qualifiés vers des plateformes de destination. Ces destinations utilisent des identifiants de segment ou d’utilisateur. Advertising destinations such as [[!DNL Google Display & Video 360]](/help/rtcdp/destinations/google-dv360-destination.md) or [[!DNL Google Ads]](/help/rtcdp/destinations/google-ads-destination.md) are examples of these types of destinations.

#### Destinations d’exportation de segments et de profils : présentation vidéo

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Extensions {#extensions}

Adobe CDP en temps réel tire parti de la puissance et de la flexibilité de Adobe Experience Platform Launch pour inclure les extensions de lancement de plate-forme dans l&#39;interface CDP en temps réel de l&#39;Adobe.

>[!TIP]
>
>Pour plus d’informations sur les extensions Adobe Experience Platform Launch, y compris les cas d’utilisation et la façon de les trouver dans l’interface, consultez la présentation [des extensions](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Adobe Experience Platform Launch.

Les extensions de lancement de plateforme transfèrent des données de événement brutes vers plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](/help/rtcdp/destinations/gainsight-extension.md) ou l’[extension de voix du client Confirmit](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

![Comparaison entre les extensions d’Experience Platform Launch et d’autres destinations](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Utilisation des connexions et des extensions

En tant que professionnel du marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’utiliser un profil client centralisé complet ou un segment client pour l’activation. Par exemple, utilisez des connexions si vous assemblez les données comportementales d’un système d’analyse et des données de gestion de la relation client chargées, afin de qualifier un utilisateur pour un segment donné avant de lui envoyer un message personnalisé.

Les extensions s’avèrent utiles lorsque des données d’événement sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

<br> 

## Catégories de destination

Les connexions et les extensions du [catalogue des destinations](https://platform.adobe.com/destination/catalog) sont regroupées par catégorie de destination (**publicité**, **espace de stockage**, **plateforme d’enquêtes**, **marketing par e-mail**, etc.), selon le cas d’utilisation marketing qu’elles vous aident à résoudre. Pour plus d’informations sur chaque catégorie, ainsi que sur les destinations incluses dans chaque catégorie, consultez la [documentation du catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md).

![Catégories de destination](/help/rtcdp/destinations/assets/destination-categories-menu.png)

