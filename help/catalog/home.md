---
keywords: Experience Platform;accueil;rubriques populaires;service de catalogue;catalogue;Service de catalogue;emplacement des données;Emplacement des données;Gestion des données;gestion des données;Parenté;parenté;Catalogue;activer le jeu de données
solution: Experience Platform
title: Présentation de Catalog service
topic-legacy: overview
description: Le Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, le catalogue renferme les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: ht
source-wordcount: '805'
ht-degree: 100%

---

# Présentation de [!DNL Catalog Service]

Le [!DNL Catalog Service] est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans [!DNL Experience Platform] soient stockées dans le [!DNL Data Lake] sous forme de fichiers et de répertoires, le [!DNL Catalog] renferme les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

En d’autres termes, le [!DNL Catalog] fait office de banque de métadonnées ou de « catalogue » qui vous permet de trouver des informations sur vos données dans [!DNL Experience Platform]. Vous pouvez utiliser le [!DNL Catalog] pour répondre aux questions suivantes :

* Où se trouvent mes données ?
* À quel stade de traitement ces données sont-elles arrivées ?
* Par quels systèmes ou processus mes données sont-elles passées ?
* Quelle quantité de données a été traitée avec succès ?
* Quelles erreurs se sont produites pendant le traitement ?

Le [!DNL Catalog] propose une API RESTful qui vous permet de gérer par programmation les métadonnées de [!DNL Platform] à l’aide des opérations CRUD de base. Pour plus d’informations, consultez le [guide de développement du catalogue](api/getting-started.md).

## [!DNL Catalog] et les services de [!DNL Experience Platform]

Les ressources suivies par le [!DNL Catalog Service] sont utilisées par plusieurs services [!DNL Experience Platform]. Afin de tirer le meilleur parti des fonctionnalités du [!DNL Catalog's], il vous est recommandé de vous familiariser avec ces services et de connaître leurs interactions avec le [!DNL Catalog].

### Système d’[!DNL Experience Data Model] (XDM)

Le système d’ [!DNL Experience Data Model] (XDM) constitue le cadre normalisé à partir duquel [!DNL Platform] organise les données d’expérience client. [!DNL Experience Platform] tire parti des schémas XDM pour décrire la structure des données de manière cohérente et réutilisable.

Lorsque des données sont ingérées dans [!DNL Platform], leur structure est mappée vers un schéma XDM et stockée dans le [!DNL Data Lake] comme partie intégrante d’un jeu de données. Les métadonnées de chaque jeu de données sont suivies par le [!DNL Catalog Service], qui inclut une référence au schéma XDM auquel le jeu de données est conforme.

Pour obtenir des informations générales sur le système XDM, consultez la [présentation du système XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] ingère des données provenant de plusieurs sources et conserve les enregistrements en tant que jeux de données dans le [!DNL Data Lake]. Le [!DNL Catalog] suit les métadonnées de ces jeux de données, quelle que soit leur source ou leur méthode d’ingestion.

Lors de l’utilisation de la méthode d’ingestion par lots, le [!DNL Catalog] réalise également le suivi de métadonnées supplémentaires pour les fichiers de lots. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Le [!DNL Catalog] effectue le suivi des métadonnées de ces fichiers de lots, ainsi que des jeux de données dans lesquels ils sont conservés après ingestion. Les métadonnées de lot contiennent des informations sur le nombre d’enregistrements correctement ingérés, ainsi que sur les enregistrements ayant échoué et les messages d’erreur associés.

Pour plus d’informations, consultez la [Présentation de l’ingestion de données](../ingestion/home.md).

## Objets du [!DNL Catalog]

Comme indiqué dans la section précédente, le [!DNL Catalog] réalise le suivi des métadonnées pour plusieurs types de ressources et d’opérations utilisées par d’autres services [!DNL Platform]. Le [!DNL Catalog] conserve sa propre banque d’« objets » contenant ces métadonnées. Les objets du [!DNL Catalog] sont des représentations interrogeables des [!DNL Platform] données de qui vous permettent de rechercher, surveiller et étiqueter vos données sans avoir à accéder aux données elles-mêmes.

Le tableau suivant décrit les différents types d’objets pris en charge par le [!DNL Catalog] :

| Objet | Point de terminaison de l’API | Définition |
|---|---|---|
| Compte | `/accounts` | Lors de la création de connexions source, les informations d’authentification doivent être renseignées. Un compte représente un ensemble d’informations d’authentification utilisées pour créer une connexion d’un type spécifique. Chaque connexion comporte un ensemble de paramètres uniques qui sont conservés par le [!DNL Catalog] et sécurisés dans un [!DNL Azure Key Vault]. |
| Lot | `/batches` | Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Un objet de lot dans le [!DNL Catalog] décrit les mesures d’ingestion du lot, telles que le nombre d’enregistrements traités ou la taille sur le disque. Il peut également inclure des liens vers des jeux de données, des vues et d’autres ressources que l’opération par lot a affectées. |
| Connexion | `/connections` | Une connexion est une instance unique d’un connecteur source, propre à votre organisation et configurée à l’aide des informations d’authentification adéquates au type de connecteur. |
| Connecteur | `/connectors` | Les connecteurs définissent la manière dont les connexions sources sont utilisées pour collecter les données d’autres applications Adobe (telles qu’Adobe Analytics et Adobe Audience Manager), de sources tierces de stockage dans le cloud (comme [!DNL Azure Blob], [!DNL Amazon S3], serveurs FTP et SFTP) et de systèmes de gestion de la relation client tiers (notamment [!DNL Microsoft Dynamics] et [!DNL Salesforce]). |
| Jeu de données | `/dataSets` | Un jeu de données est une structure de stockage et de gestion utilisée pour la collecte de données (généralement sous la forme d’un tableau) qui contient un schéma (des colonnes) et des champs (des lignes). Pour plus d’informations, consultez la [présentation des jeux de données](./datasets/overview.md). |
| Fichier de jeu de données | `/datasetFiles` | Les fichiers de jeux de données représentent des blocs de données qui ont été enregistrés sur [!DNL Platform]. Étant des enregistrements de fichiers littéraux, vous pouvez y trouver la taille du fichier, le nombre d’enregistrements qu’il contient, ainsi qu’une référence au lot qui a ingéré le fichier. |

## Étapes suivantes

Ce document vous a présenté le [!DNL Catalog Service] et son fonctionnement dans le cadre plus large du système [!DNL Experience Platform]. Pour savoir comment interagir avec les différents points d’entrée de cette API du [!DNL Catalog], consultez le guide de développement du [[!DNL Catalog] ](api/getting-started.md). Il vous est également recommandé de consulter le guide sur le [filtrage des données du catalogue](api/filter-data.md) afin de suivre les bonnes pratiques de limitation des données renvoyées dans les réponses de l’API.
