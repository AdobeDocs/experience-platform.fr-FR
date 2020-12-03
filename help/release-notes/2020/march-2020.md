---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 11 mars 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 60%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 11 mars 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] permet aux entreprises de rassembler des données issues de plusieurs systèmes d’entreprise afin de mieux permettre aux spécialistes du marketing d’identifier, de comprendre et d’impliquer les clients. [!DNL Experience Platform] comprend une infrastructure de gouvernance des données de bout en bout pour assurer une utilisation adéquate des données au sein [!DNL Platform] et lors du partage entre les systèmes.

Adobe Experience Platform [!DNL Data Governance] is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**Nouvelles fonctionnalités**

>[!NOTE]
>
>Certaines des nouvelles fonctionnalités suivantes sont actuellement en version bêta et ne sont pas disponibles pour tous les utilisateurs. Les fonctionnalités en version bêta peuvent être modifiées.

| Fonctionnalité | Description |
| ------- | ----------- |
| Application automatisée des stratégies d’utilisation des données pour [!DNL Real-time Customer Data Platform] | Les stratégies d’utilisation des données sont désormais appliquées dans le workflow d’activation des données vers les destinations. [!DNL Data Governance] est également incorporée et appliquée lorsque vous apportez des modifications qui affectent les activations existantes (telles que les modifications apportées aux étiquettes de jeux de données, aux stratégies de fusion, aux définitions de segment, etc.). |
| Traçabilité des données pour l’application | Lorsqu’une stratégie d’utilisation des données est violée dans la plateforme de données clients en temps réel, l’interface utilisateur affiche une notification contenant des informations de traçabilité des données pour aider l’utilisateur à comprendre pourquoi les stratégies ont été violées et ce qu’il peut faire pour résoudre la violation. |


**Problèmes connus**

* Aucun

For more information about [!DNL Data Governance], see the [Data Governance overview](../../data-governance/home.md).

## Ingestion des données {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Adobe Experience Platform [!DNL Data Ingestion] provides multiple alternatives for ingesting data including Batch APIs, Streaming APIs, native Adobe connectors, data integration partners, or the Adobe Experience Platform UI.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Ingestion par lots partielle | L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont traitées par lots séparément. Des détails sont ajoutés aux lots infructueux pour expliquer pourquoi ils n’ont pas été validés. Vous trouverez plus d’informations sur l’ingestion par lots partielle dans la [documentation de l’ingestion par lots partielle](../../ingestion/batch-ingestion/partial.md). |

**Problèmes connus**

* Aucun

Pour en savoir plus sur l’ingestion de données dans Platform, consultez la [Documentation de Data Ingestion](../../ingestion/home.md).


## Destinations {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), destinations are pre-built integrations with destination platforms that activate data to those partners in a seamless way.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| Destinations de stockage dans le cloud | Real-time CDP can now deliver your segments as data files to your [!DNL Amazon S3] or SFTP cloud storage locations. Vous pouvez ainsi envoyer des audiences et leurs attributs de profils à vos systèmes internes au moyen de fichiers CSV ou séparés par des tabulations. |
| Destinations publicitaires | The [!DNL Google] destination card is now split into three destination cards, for the three different [!DNL Google] platforms currently supported in Real-time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Pour en savoir plus, consultez la [présentation des destinations](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] helps you to gain a better view of your customer and their behavior by bridging identities across devices and systems, allowing you to deliver impactful, personal digital experiences in real-time.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Graphique privé amélioré | Private Graph functionality has been enhanced to reduce graph generation latency from a weekly batch process to a daily refreshed graph, allowing [!DNL Identity Service] customers to access more up-to-date identity graphs and linkages. |

**Problèmes connus**

* Aucun

For more information about [!DNL Identity Service], see the [Identity Service overview](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Signaux obsolètes du connecteur d’Adobe Audience Manager | Les données au niveau du signal d’Audience Manager ne seront plus envoyées. Notez que l’adhésion aux segments pour les Caractéristiques et les Segments sera toujours incluse. Suite à ce changement, les jeux de données entrants ne seront plus générés. |
| Jeux de données renommés | Les jeux de données générés par le connecteur d’Audience Manager ont des noms et des descriptions à jour. |
| Enable [!DNL Profile] toggle in Audience Manger | [!DNL Profile] la bascule peut être activée ou désactivée pour promouvoir le jeu de données à [!DNL Real-time Customer Profile]. La bascule est activée par défaut. |
| Prise en charge de l’interface utilisateur pour les systèmes de stockage dans le cloud | New source connector for [!DNL Azure Data Lake Storage Gen2] in the UI. |
| Prise en charge de l’interface utilisateur pour les systèmes de gestion de la relation client | New source connector for [!DNL HubSpot], [!DNL Salesforce Service Cloud], and [!DNL ServiceNow] in the UI. |
| Prise en charge de l’interface utilisateur pour les systèmes de base de données | New source connector for [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server], and [!DNL MySQL] in the UI. |

**Problèmes connus**

* Aucun

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).