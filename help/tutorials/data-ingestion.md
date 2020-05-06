---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels sur l’importation de données
topic: tutorial
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Incorporation de données dans la plateforme d’expérience

Adobe Experience Platform rassemble les données provenant de plusieurs sources afin d’aider les spécialistes du marketing à mieux comprendre le comportement de leurs clients. L’importation de données de la plateforme Adobe Experience Platform représente les multiples méthodes par lesquelles la plateforme ingère des données à partir de ces sources, ainsi que la manière dont ces données sont conservées dans Data Lake pour être utilisées par les services Plateforme en aval. L&#39;importation de données comprend l&#39;assimilation par lots, l&#39;assimilation en flux continu et l&#39;assimilation à l&#39;aide des connecteurs source. Pour en savoir plus, lisez l&#39;aperçu [de l&#39;](../ingestion/home.md) importation de données ou passez directement à la documentation [](../sources/home.md)Sources.

## Création d’un connecteur source dans l’interface utilisateur et l’API

Les connecteurs de source vous permettent d’assimiler des données provenant de plusieurs sources, où elles peuvent ensuite être étiquetées, structurées et améliorées à l’aide des services de plate-forme. Pour commencer à créer un connecteur source, consultez l’aperçu [des](../sources/home.md)sources.

## Incorporer les données de lot

Adobe Experience Platform vous permet d’importer facilement des données dans la plate-forme sous forme de fichiers de commandes. Parmi les exemples de données à ingérer, citons les données de profil provenant d’un fichier plat dans un système de gestion de la relation client (par exemple un fichier de parquet) ou les données conformes à un schéma connu de modèle de données d’expérience (XDM) dans le registre des Schémas. Pour commencer, consultez le didacticiel [sur les données d’](../ingestion/tutorials/ingest-batch-data.md)assimilation dans la plate-forme.

## Mappage d’un fichier CSV à un Schéma XDM

Pour importer des données CSV dans Adobe Experience Platform, les données doivent être mises en correspondance avec un schéma de modèle de données d’expérience (XDM). Pour savoir comment mapper un fichier CSV à un schéma XDM à l’aide de l’interface utilisateur de la plate-forme d’expérience, suivez le [mappage d’un fichier CSV à un didacticiel](../ingestion/tutorials/map-a-csv-file.md)de schéma XDM.

## Création d’une connexion en flux continu

Pour début des données en flux continu sur la plateforme d’expérience, vous devez d’abord demander un point de terminaison HTTP. Vous avez la possibilité de configurer ce point de terminaison pour appliquer un comportement authentifié. Pour ce faire, vous pouvez utiliser l’interface utilisateur de la plate-forme ou les API de plate-forme d’expérience. Pour en savoir plus, suivez les didacticiels de [création d’une connexion en flux continu à l’aide de l’interface utilisateur](../ingestion/tutorials/create-streaming-connection-ui.md) ou de [création d’une connexion en flux continu à l’aide des API](../ingestion/tutorials/create-streaming-connection.md).

## Créer une connexion de flux continu authentifiée

La collecte de données authentifiées permet aux services Adobe Experience Platform, tels que le Profil et l’identité des clients en temps réel, de différencier les enregistrements provenant de sources approuvées des enregistrements provenant de sources non approuvées. Pour commencer, suivez le didacticiel pour [créer une connexion](../ingestion/tutorials/create-authenticated-streaming-connection.md)de flux continu authentifiée.

## Données d’enregistrement et de série chronologique du flux

Avec un jeu de données et des connexions filantes en place, vous pouvez diffuser des données d&#39;enregistrement ou de série chronologique dans la plate-forme. Pour commencer la diffusion en flux continu des données d’enregistrement, suivez le didacticiel [sur les données d’enregistrement de](../ingestion/tutorials/streaming-record-data.md)flux dans la plate-forme. Pour commencer la diffusion en flux continu des données de série chronologique, suivez les données de série chronologique de [flux dans la plate-forme](../ingestion/tutorials/streaming-time-series-data.md).

## Diffusion en continu de plusieurs messages dans une seule requête HTTP

Lors de la diffusion de données en flux continu vers Adobe Experience Platform, effectuer de nombreux appels HTTP peut s’avérer coûteux. Par exemple, au lieu de créer 200 requêtes HTTP avec des charges de 1 Ko, il est beaucoup plus efficace de créer 1 requête HTTP avec 200 messages de 1 Ko chacun, avec une charge utile unique de 200 Ko. Lorsqu’il est utilisé correctement, le regroupement de plusieurs messages au sein d’une même requête constitue un excellent moyen d’optimiser les données envoyées à la plateforme d’expérience. Pour savoir comment envoyer plusieurs messages à Experience Platform dans une seule requête HTTP à l’aide de l’assimilation en flux continu, suivez le didacticiel [sur l’](../ingestion/tutorials/streaming-multiple-messages.md)envoi de plusieurs messages.



