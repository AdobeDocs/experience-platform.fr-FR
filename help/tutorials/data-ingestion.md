---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Tutoriels sur l’ingestion de données
topic-legacy: tutorial
type: Tutorial
description: Data Ingestion comprend l’ingestion par lots, l’ingestion par flux et l’ingestion à l’aide de connecteurs de sources.
exl-id: 51627acf-e90b-4911-aa54-4a59f3b6a8f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 49%

---

# Envoi de données dans [!DNL Experience Platform]

Adobe Experience Platform rassemble des données provenant de plusieurs sources afin d’aider les professionnels du marketing à mieux comprendre le comportement de leurs clients. L&#39;Adobe [!DNL Experience Platform Data Ingestion] représente les méthodes multiples par lesquelles [!DNL Platform] ingère des données provenant de ces sources, ainsi que la façon dont ces données sont conservées dans le lac Data pour être utilisées par [!DNL Platform services] en aval. [!DNL Data Ingestion] comprend l’ingestion par lots, l’ingestion par flux et l’ingestion à l’aide de connecteurs de sources. Pour en savoir plus, lisez la [présentation de Data Ingestion](../ingestion/home.md) ou accédez directement à la [documentation sur les sources](../sources/home.md).

## Création d’une connexion source dans l’interface utilisateur et l’API

Les connecteurs de source vous permettent d’assimiler des données provenant de plusieurs sources, où elles peuvent ensuite être étiquetées, structurées et améliorées à l’aide de [!DNL Platform services]. Pour commencer à créer un connecteur source, consultez l&#39;[aperçu des sources](../sources/home.md).

## Ingestion de données par lots

Adobe Experience Platform vous permet d’importer facilement des données dans [!DNL Platform] sous forme de fichiers de commandes. Parmi les exemples de données à ingérer, citons les données de profil provenant d&#39;un fichier plat dans un système de gestion de la relation client (tel qu&#39;un fichier Parquet) ou les données conformes à un schéma [!DNL Experience Data Model] (XDM) connu dans le registre des Schémas. Pour commencer, consultez le [tutoriel relatif à l’ingestion de données dans Platform](../ingestion/tutorials/ingest-batch-data.md).

## Mappage d’un fichier CSV à un schéma XDM

Pour importer des données CSV dans Adobe Experience Platform, les données doivent être mises en correspondance avec un schéma [!DNL Experience Data Model] (XDM). Pour savoir comment mapper un fichier CSV à un schéma XDM à l&#39;aide de l&#39;interface utilisateur [!DNL Experience Platform], suivez le didacticiel [mapper un fichier CSV à un schéma XDM](../ingestion/tutorials/map-a-csv-file.md).

## Création d’une connexion en continu

Pour début des données en flux continu à [!DNL Experience Platform], vous devez d’abord demander un point de terminaison HTTP. Vous avez la possibilité de configurer ce point de terminaison pour appliquer un comportement authentifié. Pour ce faire, vous pouvez utiliser l&#39;interface utilisateur [!DNL Platform] ou les API [!DNL Experience Platform]. Pour en savoir plus, suivez les tutoriels relatifs à la [création d’une connexion en continu à l’aide de l’interface utilisateur](../ingestion/tutorials/create-streaming-connection-ui.md) ou à la [création d’une connexion en continu à l’aide des API](../ingestion/tutorials/create-streaming-connection.md).

## Création d’une connexion en continu authentifiée

La collecte de données authentifiées permet aux services Adobe Experience Platform, tels que [!DNL Real-time Customer Profile] et [!DNL Identity], de faire la distinction entre les enregistrements provenant de sources approuvées et les sources non approuvées. Pour commencer, suivez le tutoriel relatif à la [création d’une connexion en continu authentifiée](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Diffusion de données d’enregistrement et de série temporelle en continu

Avec un jeu de données et des connexions en continu en place, vous pouvez diffuser des données d’enregistrement et de série temporelle en continu dans [!DNL Platform]. Pour commencer la diffusion en continu de données d’enregistrement, suivez le [tutoriel relatif à la diffusion en continu de données d’enregistrement dans Platform](../ingestion/tutorials/streaming-record-data.md). Pour commencer la diffusion en continu de données de série temporelle, suivez le [tutoriel relatif à la diffusion en continu de données de série temporelle dans Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Diffusion de plusieurs messages en continu dans une même requête HTTP

Lorsque vous diffusez des données en continu vers Adobe Experience Platform, effectuer de nombreux appels HTTP peut vous coûter cher. Par exemple, au lieu de créer 200 requêtes HTTP contenant des payloads de 1 Ko chacun, il est plus efficace de créer une requête HTTP contenant 200 messages de 1 Ko chacun avec un payload unique de 200 Ko. Lorsque cette fonctionnalité est utilisée correctement, regrouper plusieurs messages au sein d’une requête unique est une excellente manière d’optimiser les données envoyées vers [!DNL Experience Platform]. Pour savoir comment envoyer plusieurs messages à [!DNL Experience Platform] dans une seule requête HTTP à l&#39;aide de l&#39;assimilation en flux continu, suivez le [didacticiel sur l&#39;envoi de plusieurs messages](../ingestion/tutorials/streaming-multiple-messages.md).
