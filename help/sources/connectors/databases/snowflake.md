---
title: Présentation du connecteur Source Snowflake
description: Découvrez comment connecter Snowflake à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 48%

---

# Source [!DNL Snowflake]

>[!IMPORTANT]
>
>* La source [!DNL Snowflake] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.
>* Par défaut, la source [!DNL Snowflake] interprète `null` comme une chaîne vide. Contactez votre représentant d’Adobe pour vous assurer que vos valeurs `null` sont correctement écrites en tant que `null` dans Adobe Experience Platform.
>* Pour que l’Experience Platform puisse ingérer des données, les fuseaux horaires de toutes les sources par lots basées sur un tableau doivent être configurés en UTC. Le seul horodatage pris en charge pour la source [!DNL Snowflake] est TIMESTAMP_NTZ avec l’heure UTC.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Platform peut se connecter à différents types de bases de données comme les entrepôts relationnels, NoSQL ou de données. [!DNL Snowflake] est compatible avec les fournisseurs de base de données.

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL Snowflake] à Platform à l’aide d’API ou de l’interface utilisateur :

## Connecter [!DNL Snowflake] à Platform à l’aide d’API

* [Création d’une connexion de base de Snowflake à l’aide de l’API Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Création d’un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connecter [!DNL Snowflake] à Platform à l’aide de l’interface utilisateur

* [Création d’une connexion source de Snowflake dans l’interface utilisateur](../../tutorials/ui/create/databases/snowflake.md)
* [Création d’un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
