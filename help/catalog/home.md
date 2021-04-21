---
keywords: Experience Platform ; accueil ; rubriques populaires ; service catalogue ; catalogue ; service catalogue ; emplacement des données ; emplacement des données ; Data Management ; data Management ; lignée ; lignée ; catalogue ; activer le jeu de données
solution: Experience Platform
title: Présentation du service de catalogue
topic-legacy: overview
description: Le service de catalogue constitue le système d’enregistrement de l’emplacement et de la liaison des données dans Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, le catalogue renferme les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 45%

---

# [!DNL Catalog Service] présentation

[!DNL Catalog Service] est le système d’enregistrement de l’emplacement et de la lignée des données dans Adobe Experience Platform. Bien que toutes les données ingérées dans [!DNL Experience Platform] soient stockées dans [!DNL Data Lake] sous forme de fichiers et de répertoires, [!DNL Catalog] contient les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

En d&#39;autres termes, [!DNL Catalog] agit comme un magasin de métadonnées ou un &quot;catalogue&quot; où vous pouvez trouver des informations sur vos données dans [!DNL Experience Platform]. Vous pouvez utiliser [!DNL Catalog] pour répondre aux questions suivantes :

* Où se trouvent mes données ?
* À quel stade de traitement ces données sont-elles arrivées ?
* Par quels systèmes ou processus mes données sont-elles passées ?
* Quelle quantité de données a été traitée avec succès ?
* Quelles erreurs se sont produites pendant le traitement ?

[!DNL Catalog] fournit une API RESTful qui vous permet de gérer par programmation  [!DNL Platform] les métadonnées à l’aide des opérations CRUD de base. Pour plus d’informations, consultez le [guide de développement du catalogue](api/getting-started.md).

## [!DNL Catalog] et  [!DNL Experience Platform] services

Les ressources suivies par [!DNL Catalog Service] sont utilisées par plusieurs services [!DNL Experience Platform]. Afin de tirer le meilleur parti des fonctionnalités [!DNL Catalog's], il est recommandé de se familiariser avec ces services et de connaître leur interaction avec [!DNL Catalog].

### [!DNL Experience Data Model] Système (XDM)

[!DNL Experience Data Model] (XDM) Le système est le cadre normalisé qui  [!DNL Platform] organise les données d’expérience client. [!DNL Experience Platform] tire parti des schémas XDM pour décrire la structure des données de manière cohérente et réutilisable.

Lorsque des données sont ingérées dans [!DNL Platform], la structure de ces données est mappée à un schéma XDM et stockée dans [!DNL Data Lake] dans un jeu de données. Les métadonnées de chaque jeu de données sont suivies par [!DNL Catalog Service], qui comprend une référence au schéma XDM auquel le jeu de données est conforme.

Pour obtenir des informations générales sur le système XDM, consultez la [présentation du système XDM](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] ingère des données provenant de plusieurs sources et conserve les enregistrements en tant que jeux de données dans le  [!DNL Data Lake]. [!DNL Catalog] suit les métadonnées de ces jeux de données, quelle que soit leur source ou leur méthode d’assimilation.

Lors de l’utilisation de la méthode d’assimilation par lot, [!DNL Catalog] effectue également le suivi des métadonnées supplémentaires pour les fichiers de commandes. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. [!DNL Catalog] effectue le suivi des métadonnées de ces fichiers de commandes, ainsi que des jeux de données dans lesquels ils sont conservés après l’assimilation. Les métadonnées de lot contiennent des informations sur le nombre d’enregistrements correctement ingérés, ainsi que sur les enregistrements ayant échoué et les messages d’erreur associés.

Pour plus d’informations, consultez la [Présentation de l’ingestion de données](../ingestion/home.md).

## [!DNL Catalog] objets

Comme indiqué dans la section précédente, [!DNL Catalog] suit les métadonnées de plusieurs types de ressources et d&#39;opérations utilisées par d&#39;autres services [!DNL Platform]. [!DNL Catalog] conserve son propre magasin d’&quot;objets&quot; qui encapsule ces métadonnées. [!DNL Catalog]Les objets sont des représentations interrogeables des données de qui vous permettent de rechercher, surveiller et étiqueter vos données sans avoir à accéder aux données elles-mêmes.[!DNL Platform]

Le tableau suivant décrit les différents types d&#39;objet pris en charge par [!DNL Catalog] :

| Objet | Point de terminaison de l’API | Définition |
|---|---|---|
| Compte | `/accounts` | Lors de la création de connexions source, les informations d’authentification doivent être renseignées. Un compte représente un ensemble d’informations d’authentification utilisées pour créer une connexion d’un type spécifique. Chaque connexion possède un ensemble de paramètres uniques qui sont conservés par [!DNL Catalog] et sécurisés dans un [!DNL Azure Key Vault]. |
| Lot | `/batches` | Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Un objet batch dans [!DNL Catalog] décrit les mesures d&#39;assimilation du lot (telles que le nombre d&#39;enregistrements traités ou la taille sur le disque) et peut également inclure des liens vers des jeux de données, des vues et d&#39;autres ressources qui ont été affectées par l&#39;opération de traitement par lot. |
| Connexion | `/connections` | Une connexion est une instance unique d’un connecteur source, propre à votre organisation et configurée à l’aide des informations d’authentification adéquates au type de connecteur. |
| Connecteur | `/connectors` | Les connecteurs définissent la manière dont les connexions sources doivent collecter les données d’autres applications d’Adobe (telles que Adobe Analytics et Adobe Audience Manager), les sources d’enregistrement de cloud tiers (telles que [!DNL Azure Blob], [!DNL Amazon S3], les serveurs FTP et les serveurs SFTP) et les systèmes de gestion de la relation client tiers (tels que [!DNL Microsoft Dynamics] et [!DNL Salesforce]). |
| Jeu de données | `/dataSets` | Un jeu de données est une structure de stockage et de gestion utilisée pour la collecte de données (généralement sous la forme d’un tableau) qui contient un schéma (des colonnes) et des champs (des lignes). Pour plus d&#39;informations, consultez l&#39;[aperçu des jeux de données](./datasets/overview.md). |
| Fichier de jeu de données | `/datasetFiles` | Les fichiers de jeux de données représentent des blocs de données qui ont été enregistrés sur [!DNL Platform]. Étant des enregistrements de fichiers littéraux, vous pouvez y trouver la taille du fichier, le nombre d’enregistrements qu’il contient, ainsi qu’une référence au lot qui a ingéré le fichier. |

## Étapes suivantes

Ce document présente [!DNL Catalog Service] et explique comment il fonctionne dans le cadre plus large de [!DNL Experience Platform]. Consultez le [[!DNL Catalog] guide du développeur](api/getting-started.md) pour savoir comment interagir avec les différents points de terminaison de cette API [!DNL Catalog]. Il vous est également recommandé de consulter le guide sur le [filtrage des données du catalogue](api/filter-data.md) afin de suivre les bonnes pratiques de limitation des données renvoyées dans les réponses de l’API.
