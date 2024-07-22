---
keywords: destinations;destination;types de destinations
title: Types et catégories de destination
description: Découvrez les différents types et catégories de destinations dans Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 8314aca706b47c4cbcb993418c287629f5563189
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 55%

---

# Types et catégories de destination

Lisez cette page pour comprendre les différentes catégories et types de destinations d’Adobe Experience Platform.

## Types de destinations {#destination-types}

Dans Adobe Experience Platform, nous faisons la distinction entre différents types de destination : connexions, exportations de jeux de données et extensions. Il existe plusieurs types de destinations de connexion, qui vous permettent d’exporter des données vers des destinations basées sur l’API, des destinations sociales, des plateformes CRM, etc.

Enfin, les connexions peuvent également être distinguées entre les destinations publiques disponibles dans toutes les organisations du catalogue des destinations et les destinations privées que les clients Real-Time CDP Ultimate peuvent créer pour répondre à leurs cas d’utilisation spécifiques à l’exportation.

![Diagramme des types de destinations.](./assets/destination-types/types-of-destinations-no-highlight.png "Diagramme des types de destinations."){zoomable="yes"}

## Connexions {#connections}

Les destinations **[!UICONTROL Export de profil]**, **[!UICONTROL Export d’audience en flux continu]** et **[!DNL Edge Personalization]** dans Adobe Experience Platform capturent les données d’événement, les combinent à d’autres sources de données pour former le [profil client en temps réel](../profile/home.md), appliquent la segmentation et exportent les audiences et les profils qualifiés vers les destinations.

## Destinations d’exportation de profils {#profile-export}

Les destinations d’exportation de profils reçoivent des données brutes, souvent avec l’adresse e-mail comme clé primaire. Experience Platform prend actuellement en charge deux types de destinations d’exportation de profils :

* [Destinations d’exportation de profils en flux continu (destinations d’entreprise)](#streaming-profile-export)
* [Destinations de lot (basées sur des fichiers)](#file-based)

### Destinations d’entreprise avancées (destinations d’exportation de profils en continu) {#streaming-profile-export}

>[!IMPORTANT]
>
>Les destinations d’entreprise avancées, ou les destinations d’exportation de profils en continu, sont disponibles uniquement pour les clients [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html).

Utilisez les connecteurs de données de destination avancés de l’entreprise pour fournir des profils Adobe Real-Time Customer Data Platform en temps quasi réel aux systèmes internes ou à d’autres systèmes tiers pour la synchronisation des données, l’analyse et d’autres cas d’utilisation d’enrichissement de profil.

Ces destinations reçoivent les données d’audience et de profil en tant que flux de données Experience Platform.

Les destinations d’entreprise avancées incluent :

* [Destination de l’API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Destinations de lot (basées sur des fichiers) {#file-based}

Les destinations basées sur des fichiers reçoivent des fichiers `.csv` contenant des profils et/ou des attributs. [Amazon S3](catalog/cloud-storage/amazon-s3.md) est un exemple de destination où vous pouvez exporter des fichiers contenant des exportations de profils.

## Destinations d’exportation d’audiences par flux {#streaming-destinations}

Les destinations d’exportation d’audiences reçoivent des données d’audience Experience Platform. Ces destinations utilisent des identifiants d’audience ou d’utilisateur. Les destinations publicitaires et sociales telles que [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)ou [Facebook](catalog/social/facebook.md) sont des exemples de ces destinations.

## Destinations de personnalisation Edge {#edge-personalization-destinations}

Les destinations de personnalisation Edge dans Experience Platform comprennent [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) et la [destination de personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md). En utilisant ces destinations, vous pouvez permettre à vos clients d’utiliser la personnalisation sur la même page et sur la page suivante.

En savoir plus sur la façon de [configurer des destinations de personnalisation pour la personnalisation de la même page et de la page suivante](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Destinations d’exportation de profils et d’audiences - Présentation vidéo {#video}

La vidéo ci-dessous vous montre les particularités des deux types de destinations :

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Types d&#39;audiences exportées {#exported-audiences-types}

Vous pouvez exporter trois types d’audiences d’Experience Platform vers différentes destinations :

* Audiences de personnes
* Audiences de compte
* Audiences de prospects

En savoir plus sur les [différents types d’audience](/help/segmentation/ui/account-audiences.md#terminology).

Un symbole sur la carte de destination indique les types d’audiences que vous pouvez exporter vers chaque destination.

![Exemple de carte de destination avec des symboles indiquant quels types d’audience peuvent être exportés.](/help/destinations/assets/destination-types/types-of-audiences.png " Exemple de carte de destination avec des symboles indiquant quels types d’audience peuvent être exportés."){zoomable="yes"}


## Destinations d’exportation de jeux de données {#dataset-export-destinations}

Certaines destinations d’espace de stockage dans le catalogue des destinations prennent en charge les exportations de jeux de données. Utilisez ces destinations pour exporter des jeux de données brutes vers des emplacements d’espace de stockage.

En savoir plus sur la façon d’[exporter des jeux de données](/help/destinations/ui/export-datasets.md).

## Extensions {#extensions}

Platform tire parti de la puissance et de la flexibilité de la gestion des balises, ce qui vous permet de configurer des extensions de balises dans l’interface utilisateur.

>[!TIP]
>
>Pour plus d’informations détaillées sur les extensions de balises, y compris les cas d’utilisation et la façon de les trouver dans l’interface, consultez la [Présentation des extensions de balises](./catalog/launch-extensions/overview.md).

Les extensions de balises transfèrent les données brutes des événements vers plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](./catalog/personalization/gainsight.md) ou l’[extension de voix du client Confirmit](./catalog/voice/confirmit-digital-feedback.md).

![Les extensions de balises par rapport aux autres destinations](./assets/common/launch-and-other-destinations.png)

## Utilisation des connexions et des extensions {#when-to-use}

En tant que spécialiste marketing, vous pouvez utiliser une combinaison de connexions et d’extensions pour répondre à vos cas d’utilisation.

Les connexions sont utiles lorsqu’il est nécessaire d’exploiter un profil client centralisé complet ou une audience client pour l’activation. Par exemple, utilisez des connexions si vous combinez des données comportementales d’un système d’analyse avec des données de gestion de la relation client chargées afin de qualifier un utilisateur pour une audience donnée avant de lui envoyer un message personnalisé.

Les extensions s’avèrent utiles lorsque des données d’événement sont utilisées pour déclencher une action ou pour effectuer une segmentation dans un environnement externe. Par exemple, si les données comportementales doivent être transférées vers un système externe sans être jointes à d’autres sources de données dans un fichier pour un utilisateur donné.

## Catégories de destination {#categories}

Les connexions et extensions du [catalogue des destinations](https://platform.adobe.com/destination/catalog) sont regroupées par catégorie de destination (**Publicité**, **Espace de stockage**, **Plateformes d’enquête**, **Marketing par e-mail**, etc.), selon l’action marketing qu’elles permettent de réaliser. Pour plus d’informations sur chaque catégorie, ainsi que sur les destinations incluses dans chaque catégorie, consultez la [documentation du catalogue des destinations](./catalog/overview.md).

![Catégories de destination mises en surbrillance dans la page de catalogue.](./assets/destination-types/destination-categories-menu.png "Catégories de destination mises en surbrillance dans la page de catalogue."){zoomable="yes"}
