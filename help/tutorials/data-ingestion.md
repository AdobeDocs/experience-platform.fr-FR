---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriels sur l’ingestion de données
topic: tutorial
type: Tutorial
description: Data Ingestion comprend l’ingestion par lots, l’ingestion par flux et l’ingestion à l’aide de connecteurs de sources.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 51%

---


# Ingest data into [!DNL Experience Platform]

Adobe Experience Platform rassemble des données provenant de plusieurs sources afin d’aider les professionnels du marketing à mieux comprendre le comportement de leurs clients. Adobe [!DNL Experience Platform Data Ingestion] represents the multiple methods by which [!DNL Platform] ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream [!DNL Platform services]. [!DNL Data Ingestion] comprend l’ingestion par lots, l’ingestion par flux et l’ingestion à l’aide de connecteurs de sources. Pour en savoir plus, lisez la [présentation de Data Ingestion](../ingestion/home.md) ou accédez directement à la [documentation sur les sources](../sources/home.md).

## Création d’un connecteur de sources dans l’interface utilisateur et l’API

Source connectors allow you to ingest data from multiple sources, where it can then be labeled, structured, and enhanced using [!DNL Platform services]. Pour commencer à créer un connecteur source, consultez l’aperçu [des](../sources/home.md)sources.

## Ingestion de données par lots

Adobe Experience Platform allows you to easily import data into [!DNL Platform] as batch files. Examples of data to be ingested may include profile data from a flat file in a CRM system (such as a parquet file) or data that conforms to a known [!DNL Experience Data Model] (XDM) schema in the Schema Registry. Pour commencer, consultez le [tutoriel relatif à l’ingestion de données dans Platform](../ingestion/tutorials/ingest-batch-data.md).

## Mappage d’un fichier CSV à un schéma XDM

In order to ingest CSV data into Adobe Experience Platform, the data must be mapped to an [!DNL Experience Data Model] (XDM) schema. For steps showing how to map a CSV file to an XDM schema using the [!DNL Experience Platform] user interface, follow the [map a CSV file to an XDM schema tutorial](../ingestion/tutorials/map-a-csv-file.md).

## Création d’une connexion en continu

Pour début des données en flux continu à [!DNL Experience Platform], vous devez d’abord demander un point de terminaison HTTP. Vous avez la possibilité de configurer ce point de terminaison pour appliquer un comportement authentifié. This can be done using the [!DNL Platform] user interface or [!DNL Experience Platform] APIs. Pour en savoir plus, suivez les tutoriels relatifs à la [création d’une connexion en continu à l’aide de l’interface utilisateur](../ingestion/tutorials/create-streaming-connection-ui.md) ou à la [création d’une connexion en continu à l’aide des API](../ingestion/tutorials/create-streaming-connection.md).

## Création d’une connexion en continu authentifiée

Authenticated Data Collection allows Adobe Experience Platform services, such as [!DNL Real-time Customer Profile] and [!DNL Identity], to differentiate between records coming from trusted sources and untrusted sources. Pour commencer, suivez le tutoriel relatif à la [création d’une connexion en continu authentifiée](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Diffusion de données d’enregistrement et de série temporelle en continu

Avec un jeu de données et des connexions en continu en place, vous pouvez diffuser des données d’enregistrement et de série temporelle en continu dans [!DNL Platform]. Pour commencer la diffusion en continu de données d’enregistrement, suivez le [tutoriel relatif à la diffusion en continu de données d’enregistrement dans Platform](../ingestion/tutorials/streaming-record-data.md). Pour commencer la diffusion en continu de données de série temporelle, suivez le [tutoriel relatif à la diffusion en continu de données de série temporelle dans Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Diffusion de plusieurs messages en continu dans une même requête HTTP

Lorsque vous diffusez des données en continu vers Adobe Experience Platform, effectuer de nombreux appels HTTP peut vous coûter cher. Par exemple, au lieu de créer 200 requêtes HTTP contenant des payloads de 1 Ko chacun, il est plus efficace de créer une requête HTTP contenant 200 messages de 1 Ko chacun avec un payload unique de 200 Ko. Lorsque cette fonctionnalité est utilisée correctement, regrouper plusieurs messages au sein d’une requête unique est une excellente manière d’optimiser les données envoyées vers [!DNL Experience Platform]. To learn how to send multiple messages to [!DNL Experience Platform] within a single HTTP request using streaming ingestion, follow the [sending multiple messages tutorial](../ingestion/tutorials/streaming-multiple-messages.md).



