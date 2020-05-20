---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation du service de catalogue
topic: overview
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---


# Présentation du service de catalogue

Catalog Service est le système d’enregistrement de l’emplacement et du lignage des données dans Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans Data Lake sous forme de fichiers et de répertoires, Catalog contient les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

En d’autres termes, le catalogue agit comme un magasin de métadonnées ou un &quot;catalogue&quot; dans lequel vous pouvez trouver des informations sur vos données dans la plate-forme d’expérience. Vous pouvez utiliser Catalog pour répondre aux questions suivantes :

* Où se trouvent mes données ?
* À quel stade de traitement ces données sont-elles traitées ?
* Quels systèmes ou processus ont agi sur mes données ?
* Combien de données ont été traitées avec succès ?
* Quelles erreurs se sont produites pendant le traitement ?

Le catalogue fournit une API RESTful qui vous permet de gérer par programmation les métadonnées de la plate-forme à l’aide des opérations CRUD de base. Consultez le guide [du développeur de](api/getting-started.md) catalogue pour plus d’informations.

## Services de catalogue et de plate-forme d’expérience

Les ressources suivies par le service Catalog sont utilisées par plusieurs services Experience Platform. Afin de tirer le meilleur parti des fonctionnalités du catalogue, il est recommandé de se familiariser avec ces services et de connaître leur interaction avec le catalogue.

### Système de modèle de données d’expérience (XDM)

Le système de modèle de données d’expérience (XDM) est le cadre normalisé par lequel la plate-forme organise les données d’expérience client. Experience Platform tire parti des schémas XDM pour décrire la structure des données de manière cohérente et réutilisable.

Lorsque des données sont ingérées dans la plate-forme, la structure de ces données est mappée à un schéma XDM et stockée dans Data Lake dans le cadre d’un jeu de **données**. Les métadonnées de chaque jeu de données sont suivies par Catalog Service, qui inclut une référence au schéma XDM auquel le jeu de données est conforme.

Pour plus d&#39;informations sur XDM System, consultez l&#39;aperçu [du système](../xdm/home.md)XDM.

### Incorporation de données

Experience Platform ingère des données provenant de plusieurs sources et conserve les enregistrements en tant que jeux de données dans Data Lake. Le catalogue suit les métadonnées de ces jeux de données, quelle que soit leur source ou leur méthode d’assimilation.

Lors de l’utilisation de la méthode d’assimilation par lot, Catalog effectue également le suivi de métadonnées supplémentaires pour les fichiers **par lot** . Les lots sont des unités de données composées d’un ou de plusieurs fichiers à assimiler en une seule unité. Le catalogue suit les métadonnées de ces fichiers de commandes, ainsi que les jeux de données dans lesquels ils sont conservés après l’assimilation. Les métadonnées de lot incluent des informations sur le nombre d’enregistrements correctement assimilés, ainsi que sur les enregistrements ayant échoué et les messages d’erreur associés.

See the [data ingestion overview](../ingestion/home.md) for more information.

## Objets catalogue

Comme indiqué dans la section précédente, le catalogue effectue le suivi des métadonnées pour plusieurs types de ressources et d’opérations qui sont utilisées par d’autres services de plate-forme. Catalog gère son propre magasin d’&quot;objets&quot; qui encapsule ces métadonnées. Les objets de catalogue sont des représentations interrogeables des données de la plate-forme qui vous permettent de rechercher, surveiller et étiqueter vos données sans avoir à accéder aux données elles-mêmes.

Le tableau suivant décrit les différents types d’objet pris en charge par Catalog :

| Objet | Point de terminaison API | Définition |
|---|---|---|
| Compte | `/accounts` | Lors de la création de connexions source, les informations d’identification d’authentification doivent être fournies. Un compte représente un ensemble d’informations d’identification d’authentification utilisées pour créer une connexion d’un type spécifique. Chaque connexion possède un ensemble de paramètres uniques qui sont conservés par Catalog et sécurisés dans un coffre de clés Azure. |
| Lot | `/batches` | Les lots sont des unités de données composées d’un ou de plusieurs fichiers à assimiler en une seule unité. Un objet batch du catalogue décrit les mesures d&#39;assimilation du lot (telles que le nombre d&#39;enregistrements traités ou la taille sur le disque) et peut également inclure des liens vers des jeux de données, des vues et d&#39;autres ressources qui ont été affectées par l&#39;opération de traitement par lot. |
| Connexion | `/connections` | Une connexion est une instance unique d&#39;un connecteur source, propre à votre organisation et configurée à l&#39;aide des informations d&#39;identification d&#39;authentification appropriées pour le type de connecteur. |
| Connecteur | `/connectors` | Les connecteurs définissent la manière dont les connexions sources doivent collecter les données d’autres applications Adobe (telles qu’Adobe Analytics et Adobe Audience Manager), de sources d’enregistrement de cloud tierces (telles que Azure Blob, Amazon S3, des serveurs FTP et des serveurs SFTP) et de systèmes de gestion de la relation client tiers (tels que Microsoft Dynamics et Salesforce). |
| Jeu de données | `/dataSets` | Un jeu de données est un concept d&#39;enregistrement et de gestion utilisé pour la collecte de données (généralement un tableau) qui contient un schéma (colonnes) et des champs (lignes). |
| Fichier de données | `/datasetFiles` | Les fichiers de jeux de données représentent des blocs de données qui ont été enregistrés sur la plate-forme. En tant qu’enregistrements de fichiers littéraux, vous pouvez trouver la taille du fichier, le nombre d’enregistrements qu’il contient, ainsi qu’une référence au lot qui a assimilé le fichier. |

## Étapes suivantes

Ce document présente le service de catalogue et son fonctionnement dans le cadre plus large de la plate-forme d’expérience. Consultez le guide [du développeur de](api/getting-started.md) catalogue pour savoir comment interagir avec les différents points de terminaison de cette API de catalogue. Il est recommandé de se reporter également au guide sur le [filtrage des données](api/filter-data.md) du catalogue afin de suivre les meilleures pratiques de limitation des données renvoyées dans les réponses de l’API.