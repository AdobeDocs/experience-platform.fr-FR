---
title: Types et Catégories de destination
seo-title: Types et Catégories de destination
description: 'Dans la plate-forme de données client en temps réel d’Adobe, les destinations d’exportation de Profil/segment capturent les données de événement, les combinent à d’autres sources de données, appliquent la segmentation et exportent des segments et des profils qualifiés vers les destinations. Les extensions lancent des extensions pour transférer des données de événement brutes vers plusieurs types de destinations. '
seo-description: Dans la plate-forme de données client en temps réel d’Adobe, les destinations d’exportation de Profil/segment capturent les données de événement, les combinent à d’autres sources de données, appliquent la segmentation et exportent des segments et des profils qualifiés vers les destinations. Les extensions lancent des extensions pour transférer des données de événement brutes vers plusieurs types de destinations.
translation-type: tm+mt
source-git-commit: 617cf1934402b9001647d7704fb24d6256069ff3
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 7%

---


# Types et Catégories de destination

Lisez cette page pour comprendre les différents types et catégories de destination des plateformes de données clientes en temps réel d’Adobe.

## Types de destination

Dans la plate-forme de données client en temps réel d’Adobe, nous faisons la distinction entre deux types de destination : les connexions et les extensions. Il existe deux types de destinations de connexion : destinations d’exportation de Profil et destinations d’exportation de segment.

![Types de destinations](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Connexions

**Exportation** de Profil et **segmentation Exportation** de destinations dans la plateforme de données clientes Adobe en temps réel, capture des données de événement, les combine à d’autres sources de données pour former le profil [client en temps](/help/profile/home.md)réel, appliquer la segmentation et exporter des segments et des profils qualifiés vers les destinations.

<br> 

#### Destinations d’exportation de profils

Les destinations d’exportation de profils génèrent un fichier contenant des profils et/ou des attributs. Ces destinations utilisent des données brutes, souvent avec l’adresse électronique comme clé primaire. La destination [de l’enregistrement cloud](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 est un exemple de destination où vous pouvez déposer des fichiers contenant des exportations de profils.

#### Destinations d’exportation de segments

Les destinations d’exportation de segments envoient les profils et les segments pour lesquels ils se sont qualifiés vers les plateformes de destination. Ces destinations utilisent des identifiants de segment ou d’utilisateur. Les destinations publicitaires, telles que [Google Display &amp; Video 360](/help/rtcdp/destinations/google-dv360-destination.md) ou les publicités [](/help/rtcdp/destinations/google-ads-destination.md) Google, sont des exemples de ces types de destinations.

#### Destinations d&#39;exportation de Profils et de segments - présentation vidéo

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Extensions

Le CDP Adobe en temps réel tire parti de la puissance et de la flexibilité du lancement de la plate-forme d’expérience pour inclure les extensions de lancement dans l’interface CDP Adobe en temps réel.

>[!TIP]
>
>Pour plus d’informations sur les extensions de lancement de plateformes d’expérience, y compris les cas d’utilisation et la manière de les trouver dans l’interface, voir la présentation [des extensions de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)lancement.

Les extensions lancent des extensions pour transférer des données de événement brutes vers plusieurs types de destinations. Considérez les extensions comme un type de destination **Événement de transfert** . Il s’agit d’un type d’intégration plus simple avec les plateformes de destination, qui transfère uniquement les données de événement brutes. Par exemple, l’extension [de personnalisation de](/help/rtcdp/destinations/gainsight-extension.md) Gainsight ou la voix de [confirmation de l’extension](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Client.

![Extensions de lancement de plateformes d’expérience par rapport à d’autres destinations](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Utilisation des connexions et des extensions

En tant que spécialiste du marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’exploiter un profil client centralisé complet ou un segment de clients pour l’activation. Par exemple, utilisez des connexions si vous joignez des données comportementales d’un système d’analyse aux données de gestion de la relation client téléchargées afin de qualifier un utilisateur pour un segment donné avant de lui envoyer un message personnalisé.

Les extensions sont utiles lorsque des données de événement sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

<br> 

## Catégories de destination

Les connexions et extensions du catalogue [de](https://platform.adobe.com/destination/catalog) destinations sont regroupées par catégorie de destination (**publicité**, enregistrement **** Cloud, plateformes **Questionnaire, marketing par courriel, etc.), selon le cas d’utilisation marketing qu’elles vous aident à atteindre.****** Pour plus d&#39;informations sur chacune des catégories, ainsi que sur les destinations incluses dans chaque catégorie, consultez la documentation [du catalogue](/help/rtcdp/destinations/destinations-catalog.md)Destinations.

![Catégories de destination](/help/rtcdp/destinations/assets/destination-categories-menu.png)

