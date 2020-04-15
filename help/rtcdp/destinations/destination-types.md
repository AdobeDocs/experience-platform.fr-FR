---
title: Types de destination et  de
seo-title: Types de destination et  de
description: 'Dans la plate-forme de données clientes Adobe en temps réel, les destinations d’exportation de /segments capturent des données de, les combinent à d’autres sources de données, appliquent la segmentation et exportent des segments et des qualifiés vers des destinations. Les extensions lancent des données de  brutes vers plusieurs types de destinations. '
seo-description: Dans la plate-forme de données clientes Adobe en temps réel, les destinations d’exportation de /segments capturent des données de, les combinent à d’autres sources de données, appliquent la segmentation et exportent des segments et des qualifiés vers des destinations. Les extensions lancent des données de  brutes vers plusieurs types de destinations.
translation-type: tm+mt
source-git-commit: 617cf1934402b9001647d7704fb24d6256069ff3

---


# Types de destination et  de

Lisez cette page pour comprendre les différents types et les  de la plateforme de données clientes en temps réel d’Adobe.

## Types de destination

Dans la plateforme de données clientes Adobe en temps réel, nous faisons la distinction entre deux types de destination : les connexions et les extensions. Il existe deux types de destinations de connexion : les destinations d’exportation de  et les destinations d’exportation de segment.

![Types de destinations](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Connexions

**Exporter** et **segmenter les destinations d’exportation** dans la plate-forme de données clientes Adobe en temps réel captent les données , les combinent avec d’autres sources de données pour former le en temps [](/help/profile/home.md)réel, appliquer la segmentation et exporter des segments et des qualifiés vers les destinations.

<br> 

#### Destinations d’exportation de profils

Les destinations d’exportation de profils génèrent un fichier contenant des profils et/ou des attributs. Ces destinations utilisent des données brutes, souvent avec l’adresse électronique comme clé primaire. Le cloud [Amazon S3  destination](/help/rtcdp/destinations/amazon-s3-destination.md) du est un exemple de destination où vous pouvez déposer des fichiers contenant des exportations de .

#### Destinations d’exportation de segments

Les destinations d’exportation de segments envoient le  et les segments pour lesquels ils sont qualifiés vers les plateformes de destination. Ces destinations utilisent des identifiants de segment ou d’utilisateur. Les destinations publicitaires telles que [Google Display &amp; Video 360](/help/rtcdp/destinations/google-dv360-destination.md) ou les publicités [](/help/rtcdp/destinations/google-ads-destination.md) Google sont des exemples de ces types de destinations.

#### Destinations d&#39;exportation de  d&#39;exportation et de segments - Présentation vidéo

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Extensions

Le CDP Adobe en temps réel tire parti de la puissance et de la flexibilité du lancement de la plate-forme d’expérience pour inclure les extensions de lancement dans l’interface CDP Adobe en temps réel.

>[!TIP]
>
>Pour plus d’informations sur les extensions de lancement de plateforme d’expérience, y compris les cas d’utilisation et la manière de les trouver dans l’interface, voir la présentation [des extensions de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)lancement.

Les extensions lancent des données de  brutes vers plusieurs types de destinations. Considérez les extensions comme un **type de destination Transfert** . Il s’agit d’un type d’intégration plus simple avec les plateformes de destination, qui ne transfère que les données  brutes. Par exemple, l’extension [de personnalisation de](/help/rtcdp/destinations/gainsight-extension.md) Gainsight ou la voix de [confirmation de l’extension](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Client.

![Expérience Platform Launch Extensions par rapport à d’autres destinations](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Quand utiliser des connexions et des extensions

En tant que spécialiste du marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire de tirer parti d’un de clients centralisé complet ou d’un segment de clients pour    de. Par exemple, utilisez des connexions si vous joignez des données comportementales d’un système d’analyse à des données de gestion de la relation client téléchargées afin de qualifier un utilisateur pour un segment donné avant de lui envoyer un message personnalisé.

Les extensions s’avèrent utiles lorsque des données  sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un  externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

<br> 

## Catégories de destination

Les connexions et les extensions du catalogue [de](https://platform.adobe.com/destination/catalog) destinations sont regroupées par  de destination (**Publicité**, **Cloud**, plateformes **dede, marketing par courriel, etc.), selon le cas d’utilisation marketing qu’elles vous aident à atteindre.****** Pour plus d’informations sur chaque  de, ainsi que sur les destinations incluses dans chaque  de, consultez la documentation [du catalogue](/help/rtcdp/destinations/destinations-catalog.md)Destinations.

![Catégories de destination](/help/rtcdp/destinations/assets/destination-categories-menu.png)

