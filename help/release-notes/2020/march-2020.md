---
title: Notes de mise à jour d’Adobe Experience Platform - Mars 2020
description: Les notes de mise à jour de mars 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: notes de mise à jour ;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 61%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 11 mars 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [Gouvernance des données](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Gouvernance des données {#governance}

[!DNL Experience Platform] permet aux entreprises de rassembler des données issues de plusieurs systèmes d’entreprise afin de permettre aux professionnels du marketing d’identifier, de comprendre et d’impliquer les clients avec plus d’efficacité. [!DNL Experience Platform] comprend une infrastructure de gouvernance des données de bout en bout pour assurer l’utilisation appropriée des données au sein des [!DNL Experience Platform] et lors du partage entre les systèmes.

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans [!DNL Experience Platform] à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’accès aux données et le contrôle d’accès aux données pour les actions marketing.

**Nouvelles fonctionnalités**

>[!NOTE]
>
>Certaines des nouvelles fonctionnalités suivantes sont actuellement en version bêta et ne sont pas disponibles pour tous les utilisateurs. Les fonctionnalités en version bêta peuvent être modifiées.

| Fonctionnalité | Description |
| ------- | ----------- |
| Application automatisée des politiques d’utilisation des données pour les [!DNL Real-Time Customer Data Platform] | Les politiques d’utilisation des données sont désormais appliquées dans le workflow d’activation des données vers les destinations. La gouvernance des données est aussi intégrée et appliquée lors de modifications affectant les activations existantes (telles que les modifications des libellés des jeux de données, des politiques de fusion, des définitions de segment, etc.). |
| Traçabilité des données pour l’application | Lorsqu’une politique d’utilisation des données est enfreinte dans Real-Time CDP, l’interface utilisateur affiche une notification contenant des informations sur la parenté des données afin d’aider l’utilisateur ou l’utilisatrice à comprendre pourquoi les politiques ont été enfreintes et ce qu’il ou elle peut faire pour résoudre la violation. |


**Problèmes connus**

* Aucun

Pour plus d’informations sur la gouvernance des données, consultez la [présentation de la gouvernance des données](../../data-governance/home.md).

## Ingestion des données {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Adobe Experience Platform [!DNL Data Ingestion] propose plusieurs alternatives pour l’ingestion de données, notamment des API Batch, des API Streaming, des connecteurs Adobe natifs, des partenaires d’intégration de données ou l’interface utilisateur de Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Ingestion par lots partielle | L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont traitées par lots séparément. Des détails sont ajoutés aux lots infructueux pour expliquer pourquoi ils n’ont pas été validés. Vous trouverez plus d’informations sur l’ingestion par lots partielle dans la [documentation de l’ingestion par lots partielle](../../ingestion/batch-ingestion/partial.md). |

**Problèmes connus**

* Aucune

Pour en savoir plus sur l’ingestion de données dans Experience Platform, consultez la [documentation sur l’ingestion de données](../../ingestion/home.md).


## Destinations {#destinations}

Dans [Real-Time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations préconfigurées à des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| Destinations de stockage dans le cloud | Real-Time CDP peut désormais diffuser vos segments sous forme de fichiers de données vers vos emplacements de stockage cloud [!DNL Amazon S3] ou SFTP. Vous pouvez ainsi envoyer des audiences et leurs attributs de profils à vos systèmes internes au moyen de fichiers CSV ou séparés par des tabulations. |
| Destinations publicitaires | La carte de destination [!DNL Google] est désormais divisée en trois cartes de destination, pour les trois différentes plateformes de [!DNL Google] actuellement prises en charge dans Real-Time CDP : [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Pour en savoir plus, consultez la [présentation des destinations](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Proposer des expériences digitales pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Graphique privé amélioré | La fonctionnalité de graphique privé a été améliorée afin de réduire la latence de génération de graphique, passant d’un traitement par lots hebdomadaire à un graphique actualisé quotidiennement, ce qui permet aux clients [!DNL Identity Service] d’accéder à des graphiques d’identités et à des liens plus récents. |

**Problèmes connus**

* Aucune

Pour plus d’informations sur [!DNL Identity Service], consultez la présentation d’Identity Service [&#128279;](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Signaux obsolètes du connecteur d’Adobe Audience Manager | Les données au niveau du signal d’Audience Manager ne seront plus envoyées. Notez que l’adhésion aux segments pour les Caractéristiques et les Segments sera toujours incluse. Suite à ce changement, les jeux de données entrants ne seront plus générés. |
| Jeux de données renommés | Les jeux de données générés par le connecteur d’Audience Manager ont des noms et des descriptions à jour. |
| Activer le bouton [!DNL Profile] dans Audience Manager | [!DNL Profile] bouton (bascule) peut être activé ou désactivé pour convertir un jeu de données en [!DNL Real-Time Customer Profile]. La bascule est activée par défaut. |
| Prise en charge de l’interface utilisateur pour les systèmes de stockage dans le cloud | Nouveau connecteur source pour [!DNL Azure Data Lake Storage Gen2] dans l’interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes de gestion de la relation client | Nouveau connecteur source pour [!DNL HubSpot], [!DNL Salesforce Service Cloud] et [!DNL ServiceNow] dans l’interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes de base de données | Nouveau connecteur source pour [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] et [!DNL MySQL] dans l’interface utilisateur. |

**Problèmes connus**

* Aucun

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
