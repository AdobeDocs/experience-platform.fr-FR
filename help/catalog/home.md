---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;data location;Data Location;Data management;data management;Lineage;lineage;Catalog;enable dataset
solution: Experience Platform
title: Présentation du service de catalogue
topic: overview
description: Le service de catalogue constitue le système d’enregistrement de l’emplacement et de la liaison des données dans Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, le catalogue renferme les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 49%

---


# [!DNL Catalog Service] aperçu

[!DNL Catalog Service] est le système d’enregistrement de l’emplacement et de la lignée des données dans Adobe Experience Platform. While all data that is ingested into [!DNL Experience Platform] is stored in the [!DNL Data Lake] as files and directories, [!DNL Catalog] holds the metadata and description of those files and directories for lookup and monitoring purposes.

Simply put, [!DNL Catalog] acts as a metadata store or &quot;[!UICONTROL catalog]&quot; where you can find information about your data within [!DNL Experience Platform]. You can use [!DNL Catalog] to answer the following questions:

* Où se trouvent mes données ?
* À quel stade de traitement ces données sont-elles arrivées ?
* Par quels systèmes ou processus mes données sont-elles passées ?
* Quelle quantité de données a été traitée avec succès ?
* Quelles erreurs se sont produites pendant le traitement ?

[!DNL Catalog] fournit une API RESTful qui vous permet de gérer par programmation [!DNL Platform] les métadonnées à l’aide des opérations CRUD de base. Pour plus d’informations, consultez le [guide de développement du catalogue](api/getting-started.md).

## [!DNL Catalog] et [!DNL Experience Platform] services

Les ressources qui [!DNL Catalog Service] suivent sont utilisées par plusieurs [!DNL Experience Platform] services. In order to make the most of [!DNL Catalog's] capabilities, it is recommended that you become familiar with these services and how they interact with [!DNL Catalog].

### [!DNL Experience Data Model] Système (XDM)

[!DNL Experience Data Model] (XDM) Le système est le cadre normalisé qui [!DNL Platform] organise les données d’expérience client. [!DNL Experience Platform] tire parti des schémas XDM pour décrire la structure des données de manière cohérente et réutilisable.

When data is ingested into [!DNL Platform], the structure of that data is mapped to an XDM schema and stored within the [!DNL Data Lake] as part of a **dataset**. The metadata for each dataset is tracked by [!DNL Catalog Service], which includes a reference to the XDM schema that the dataset conforms to.

Pour obtenir des informations générales sur le système XDM, consultez la [présentation du système XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] ingère des données provenant de plusieurs sources et conserve les enregistrements en tant que jeux de données dans le [!DNL Data Lake]. [!DNL Catalog] suit les métadonnées de ces jeux de données, quelle que soit leur source ou leur méthode d’assimilation.

When using the batch ingestion method, [!DNL Catalog] also tracks additional metadata for **batch** files. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. [!DNL Catalog] effectue le suivi des métadonnées de ces fichiers de commandes, ainsi que des jeux de données dans lesquels ils sont conservés après l’assimilation. Les métadonnées de lot contiennent des informations sur le nombre d’enregistrements correctement ingérés, ainsi que sur les enregistrements ayant échoué et les messages d’erreur associés.

Pour plus d’informations, consultez la [Présentation de l’ingestion de données](../ingestion/home.md).

## [!DNL Catalog] objets

As outlined in the previous section, [!DNL Catalog] tracks metadata for several kinds of resources and operations that are used by other [!DNL Platform] services. [!DNL Catalog] conserve son propre magasin d’&quot;objets&quot; qui encapsule ces métadonnées. [!DNL Catalog]Les objets sont des représentations interrogeables des données de qui vous permettent de rechercher, surveiller et étiqueter vos données sans avoir à accéder aux données elles-mêmes.[!DNL Platform]

The following table outlines the different object types supported by [!DNL Catalog]:

| Objet | Point de terminaison de l’API | Définition |
|---|---|---|
| Compte | `/accounts` | Lors de la création de connexions source, les informations d’authentification doivent être renseignées. Un compte représente un ensemble d’informations d’authentification utilisées pour créer une connexion d’un type spécifique. Each connection has a set of unique parameters that are persisted by [!DNL Catalog] and secured in an [!DNL Azure Key Vault]. |
| Lot | `/batches` | Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. A batch object in [!DNL Catalog] outlines the batch&#39;s ingestion metrics (such as the number of records processed or size on disk) and may also include links to datasets, views, and other resources that were affected by the batch operation. |
| Connexion | `/connections` | Une connexion est une instance unique d’un connecteur source, propre à votre organisation et configurée à l’aide des informations d’authentification adéquates au type de connecteur. |
| Connecteur | `/connectors` | Connectors define how source connections are to gather data from other Adobe applications (such as Adobe Analytics and Adobe Audience Manager), third-party cloud storage sources (such as [!DNL Azure Blob], [!DNL Amazon S3], FTP servers, and SFTP servers), and third-party CRM systems (such as [!DNL Microsoft Dynamics] and [!DNL Salesforce]). |
| Jeu de données | `/dataSets` | Un jeu de données est une structure de stockage et de gestion utilisée pour la collecte de données (généralement sous la forme d’un tableau) qui contient un schéma (des colonnes) et des champs (des lignes). See the [datasets overview](./datasets/overview.md) for more information. |
| Fichier de jeu de données | `/datasetFiles` | Les fichiers de jeux de données représentent des blocs de données qui ont été enregistrés sur [!DNL Platform]. Étant des enregistrements de fichiers littéraux, vous pouvez y trouver la taille du fichier, le nombre d’enregistrements qu’il contient, ainsi qu’une référence au lot qui a ingéré le fichier. |

## Étapes suivantes

This document provided an introduction to [!DNL Catalog Service] and how it functions within the greater scope of [!DNL Experience Platform]. Pour savoir comment interagir avec les différents points de terminaison de cette API , consultez le [guide de développement du catalogue](api/getting-started.md). [!DNL Catalog] Il vous est également recommandé de consulter le guide sur le [filtrage des données du catalogue](api/filter-data.md) afin de suivre les bonnes pratiques de limitation des données renvoyées dans les réponses de l’API.