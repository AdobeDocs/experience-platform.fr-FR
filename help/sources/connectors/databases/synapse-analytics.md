---
keywords: Experience Platform;accueil;rubriques les plus consultées;Azure synapse Analytics;azure synapse Analytics;Synapse;synapse
solution: Experience Platform
title: Présentation du connecteur source Azure synapse Analytics
topic-legacy: overview
description: Découvrez comment connecter Azure synapse Analytics à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 9%

---

# [!DNL Azure Synapse Analytics] connector

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’une base de données tierce. [!DNL Platform] peuvent se connecter à différents types de bases de données, telles que les entrepôts relationnels, NoSQL ou de données. [!DNL Azure Synapse Analytics] est compatible avec les fournisseurs de base de données.

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Pour plus d’informations, consultez la page [liste autorisée d’adresses IP](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Le connecteur source [!DNL Azure Synapse Analytics] ne prend actuellement pas en charge la connectivité de la même région à Platform. Cela signifie que si votre instance Azure utilise la même région réseau que Platform, une connexion aux sources Platform ne peut pas être établie. Actuellement, seule la connectivité inter-régions est prise en charge. Pour plus d’informations, contactez votre gestionnaire de compte d’Adobe.

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Azure Synapse Analytics] à [!DNL Platform] à l’aide des API ou de l’interface utilisateur :

## Connectez [!DNL Azure Synapse Analytics] à [!DNL Platform] à l’aide des API

- [Création d’une connexion de base Analytics d’Azure synapse à l’aide de l’API Flow Service](../../tutorials/api/create/databases/synapse-analytics.md)
- [Explorer la structure et le contenu des données d’une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Création d’un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connectez [!DNL Azure Synapse Analytics] à [!DNL Platform] à l’aide de l’interface utilisateur.

- [Création d’une connexion source Analytics d’Azure synapse dans l’interface utilisateur](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Création d’un flux de données pour une connexion à la source de la base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
