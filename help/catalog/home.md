---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation du service de catalogue
topic: overview
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Présentation du service de catalogue

Le service de catalogue est le système d’enregistrement de l’emplacement et de la lignée des données dans Adobe Experience Platform. Bien que toutes les données assimilées à la plateforme Experience Platform soient stockées dans Data Lake sous forme de fichiers et de répertoires, Catalog contient les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

En d’autres termes, le catalogue agit comme un magasin de métadonnées ou un &quot;catalogue&quot; dans lequel vous pouvez trouver des informations sur vos données dans Experience Platform. Vous pouvez utiliser le catalogue pour répondre aux questions suivantes :

* Où se trouvent mes données ?
* À quel stade de traitement ces données sont-elles traitées ?
* Quels systèmes ou processus ont agi sur mes données ?
* Combien de données ont été traitées avec succès ?
* Quelles erreurs se sont produites pendant le traitement ?

Le catalogue fournit une API RESTful qui vous permet de gérer par programmation les métadonnées de plateforme à l’aide des opérations CRUD de base. Pour plus d’informations, consultez le guide [du développeur de](api/getting-started.md) catalogue.

## Services de catalogue et de plateforme d’expérience

Les ressources suivies par le service Catalog sont utilisées par plusieurs services Experience Platform. Afin de tirer le meilleur parti des fonctionnalités du catalogue, il est recommandé de se familiariser avec ces services et de connaître leur interaction avec le catalogue.

### Système XDM (Experience Data Model)

Le système de modèle de données d’expérience (XDM) est le cadre normalisé par lequel la plateforme organise les données d’expérience client. Experience Platform tire parti des XDM pour décrire la structure des données de manière cohérente et réutilisable.

Lorsque des données sont assimilées à une plateforme, la structure de ces données est mappée à un  XDM et stockée dans Data Lake dans le cadre d’un **jeu de données**. Les métadonnées de chaque jeu de données sont suivies par le service de catalogue, qui inclut une référence au XDM  auquel le jeu de données est conforme.

Pour plus d&#39;informations sur le système XDM, consultez la présentation [du système](../xdm/home.md)XDM.

### Ingestion des données

Experience Platform imprime des données provenant de plusieurs sources et conserve les enregistrements en tant que jeux de données dans Data Lake. Le catalogue suit les métadonnées de ces jeux de données, quelle que soit leur source ou leur méthode d’assimilation.

Lors de l’utilisation de la méthode d’assimilation par lot, Catalog effectue également le suivi de métadonnées supplémentaires pour les fichiers **par lot** . Les lots sont des unités de données composées d’un ou de plusieurs fichiers à assimiler en une seule unité. Le catalogue effectue le suivi des métadonnées de ces fichiers de commandes, ainsi que des jeux de données dans lesquels ils sont conservés après l’importation. Les métadonnées de lot contiennent des informations sur le nombre d’enregistrements correctement assimilés, ainsi que sur les enregistrements ayant échoué et les messages d’erreur associés.

See the [data ingestion overview](../ingestion/home.md) for more information.

## Objets de catalogue

Comme indiqué dans la section précédente, le catalogue effectue le suivi des métadonnées pour plusieurs types de ressources et d’opérations utilisées par d’autres services de plateforme. Le catalogue conserve son propre magasin d’&quot;objets&quot; qui encapsule ces métadonnées. Les objets de catalogue sont des représentations interrogeables des données de la plateforme qui vous permettent de rechercher, surveiller et étiqueter vos données sans avoir à accéder aux données elles-mêmes.

Le tableau suivant décrit les différents types d’objet pris en charge par Catalog :

| Objet | Point de terminaison API | Définition |
|---|---|---|
| Compte | `/accounts` | Lors de la création de connexions source, les informations d’identification d’authentification doivent être fournies. Un compte représente un ensemble d’informations d’identification d’authentification utilisées pour créer une connexion d’un type spécifique. Chaque connexion comporte un ensemble de paramètres uniques qui sont conservés par le catalogue et sécurisés dans un coffre de clés Azure. |
| Lot | `/batches` | Les lots sont des unités de données composées d’un ou de plusieurs fichiers à assimiler en une seule unité. Un objet batch dans le catalogue décrit les mesures d’assimilation du lot (telles que le nombre d’enregistrements traités ou la taille sur le disque) et peut également inclure des liens vers des jeux de données, des  et d’autres ressources qui ont été affectées par l’opération du lot. |
| Connexion | `/connections` | Une connexion est une instance unique d’un connecteur source, propre à votre organisation et configurée à l’aide des informations d’identification d’authentification appropriées pour le type de connecteur. |
| Connecteur | `/connectors` | Les connecteurs définissent la manière dont les connexions sources sont utilisées pour collecter les données d’autres applications Adobe (telles qu’Adobe Analytics et Adobe   Manager), de sources de de cloud tiers (telles que Azure Blob, Amazon S3, des serveurs FTP et des serveurs SFTP) et de systèmes de gestion de la relation client tiers (tels que Microsoft Dynamics et Salesforce). |
| Jeu de données | `/dataSets` | Un jeu de données est un concept  de  et de gestion utilisé pour la collecte de données (généralement sous la forme d’un tableau) qui contient un (des colonnes) et des champs (des lignes). |
| Fichier de données | `/datasetFiles` | Les fichiers de jeux de données représentent des blocs de données qui ont été enregistrés sur la plateforme. En tant qu’enregistrements de fichiers littéraux, vous pouvez y trouver la taille du fichier, le nombre d’enregistrements qu’il contient, ainsi qu’une référence au lot qui a assimilé le fichier. |

## Étapes suivantes

Ce présente le service de catalogue et son fonctionnement dans le cadre plus large de la plateforme d’expérience. Pour savoir comment interagir avec les différents points de fin de cette API de catalogue, consultez le guide [du développeur de](api/getting-started.md) catalogue. Il est également recommandé de consulter le guide sur le [filtrage des données](api/filter-data.md) du catalogue afin de suivre les bonnes pratiques de limitation des données renvoyées dans les réponses de l’API.