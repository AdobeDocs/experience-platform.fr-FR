---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels sur l’insertion de données
topic: tutorial
translation-type: tm+mt
source-git-commit: 2020f4b88f81f2d4fe3cfbd91cd18119ae580f4f

---


# Incorporation de données dans la plateforme d’expérience

Adobe Experience Platform rassemble des données provenant de plusieurs sources afin d’aider les spécialistes du marketing à mieux comprendre le comportement de leurs clients. Adobe Experience Platform Data Ingestion représente les méthodes multiples par lesquelles Platform imprime des données à partir de ces sources, ainsi que la manière dont ces données sont conservées dans Data Lake pour être utilisées par les services Plateforme en aval. L’importation de données comprend l’assimilation par lot, l’assimilation en flux continu et l’assimilation à l’aide de connecteurs source. Pour en savoir plus, lisez l’aperçu [de l’administration des](../ingestion/home.md) données ou accédez directement à la documentation [sur les](../source-connectors/home.md)sources.

## Création d’un connecteur source dans l’interface utilisateur et l’API

Les connecteurs de source vous permettent d’assimiler des données provenant de plusieurs sources, où elles peuvent ensuite être étiquetées, structurées et améliorées à l’aide des services de plateforme. Pour commencer à créer un connecteur à l&#39;aide de l&#39;interface utilisateur, consultez la section [Création d&#39;un connecteur source dans la présentation](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/sources-ui-tutorial.md)de l&#39;interface utilisateur. Pour créer des connecteurs source à l’aide de l’API, rendez-vous sur la page [Création d’un connecteur source à l’aide de l’aperçu](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)de l’API du service de flux.

## Incorporer les données de lot

Adobe Experience Platform vous permet d’importer facilement des données dans la plate-forme sous forme de fichiers de commandes. Parmi les exemples de données à ingérer, citons les données  d’un fichier plat dans un système de gestion de la relation client (par exemple un fichier de parquet) ou les données conformes à un de modèle de données d’expérience (XDM) connu dans le registre de l’. Pour commencer, consultez le didacticiel [relatif à l’](../ingestion/tutorials/ingest-batch-data.md)assimilation des données dans la plateforme.

## Mappage d’un fichier CSV à un XDM 

Pour importer des données CSV dans Adobe Experience Platform, les données doivent être mappées à un  de modèle de données d’expérience (XDM). Pour savoir comment mapper un fichier CSV à un XDM à l’aide de l’interface utilisateur de la plateforme d’expérience, suivez le [didacticiel](../ingestion/tutorials/map-a-csv-file.md)Mappage d’un fichier CSV à un XDM.

## Création d’une connexion de flux continu

Pour  des données en flux continu à la plateforme Experience Platform, vous devez d’abord créer une connexion HTTP en flux continu. Lors de la création d’une connexion en flux continu, vous devez fournir des détails clés, tels que la source des données en flux continu, et indiquer si vous prévoyez d’envoyer des données à partir d’une source approuvée (authentifiée) ou non approuvée (non authentifiée). Vous pouvez le faire à l’aide de l’interface utilisateur de la plateforme ou des API de plateforme d’expérience. Pour en savoir plus, suivez les didacticiels pour [créer une connexion en flux continu à l’aide de l’interface utilisateur](../ingestion/tutorials/create-streaming-connection-ui.md) ou [créer une connexion en flux continu à l’aide des API](../ingestion/tutorials/create-streaming-connection.md).

## Création d’une connexion de flux continu authentifiée

La collecte de données authentifiées permet aux services d’Adobe Experience Platform, tels que les  et l’identité des clients en temps réel, de différencier les enregistrements provenant de sources approuvées des sources non approuvées. Pour commencer, suivez le didacticiel pour [créer une connexion](../ingestion/tutorials/create-authenticated-streaming-connection.md)de flux continu authentifiée.

## Données d’enregistrement de diffusion et de série chronologique

Avec un jeu de données et des connexions filmées en place, vous pouvez diffuser des données d’enregistrement ou de série chronologique dans la plateforme. Pour commencer la diffusion en flux continu des données d’enregistrement, suivez le didacticiel [sur les données d’enregistrement du](../ingestion/tutorials/streaming-record-data.md)flux dans la plateforme. Pour commencer la diffusion en flux continu des données de série chronologique, suivez les données de série chronologique du [flux dans Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Diffusion en continu de plusieurs messages dans une requête HTTP unique

Lors de la diffusion en flux continu de données vers Adobe Experience Platform, il peut s’avérer coûteux d’effectuer de nombreux appels HTTP. Par exemple, au lieu de créer 200 requêtes HTTP avec des charges de 1 Ko, il est beaucoup plus efficace de créer 1 requête HTTP avec 200 messages de 1 Ko chacun, avec une charge utile unique de 200 Ko. Lorsqu’il est utilisé correctement, le regroupement de plusieurs messages au sein d’une même requête constitue un excellent moyen d’optimiser les données envoyées à la plateforme d’expérience. Pour savoir comment envoyer plusieurs messages à Experience Platform dans une seule requête HTTP à l’aide de l’assimilation en flux continu, suivez le didacticiel [sur l’](../ingestion/tutorials/streaming-multiple-messages.md)envoi de plusieurs messages.



