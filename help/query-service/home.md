---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Adobe Experience Platform Query Service
topic: overview
description: Ce document donne une vue d’ensemble du rôle de Query Service dans Experience Platform.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 30%

---


# [!DNL Query Service] aperçu

Adobe Experience Platform ingère des données à partir de sources diverses. Le grand défi qui attend les spécialistes du marketing : comprendre ces données afin de découvrir des informations sur leurs clients. Adobe Experience Platform [!DNL Query Service] facilitates that by allowing you to use standard SQL to query data in [!DNL Platform]. Using [!DNL Query Service], you can join any dataset in the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, machine learning, or for ingestion into [!DNL Real-time Customer Profile]. This document provides an overview of the role of [!DNL Query Service] within [!DNL Experience Platform].

[!DNL Query Service] permet aux marques de relier le parcours client en ligne au parcours client hors ligne et de comprendre l’attribution omni-canal. La vidéo suivante montre comment une entreprise peut tirer parti [!DNL Query Service] d&#39;une expérience pour traiter des cas d&#39;utilisation clés et comment [!DNL Query Service] fonctionne.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilisation de [!DNL Query Service]

[!DNL Query Service] fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez créer des requêtes SQL pour mieux analyser vos données. L’interface utilisateur vous permet d’écrire et d’exécuter des requêtes, de visualiser des requêtes précédemment exécutées et d’accéder à des requêtes enregistrés par des utilisateurs au sein de votre organisation IMS. L’interface utilisateur est conçue pour être utilisée en tant qu’environnement de test pour vos requêtes avant de les exécuter sur votre jeu de données plus vaste. More information on using the interactive service within [!DNL Platform] can be found in the [Query Service user interface guide](ui/overview.md). L’API RESTful offre une expérience similaire vous permettant d’écrire et d’exécuter par programmation des requêtes, de planifier des requêtes pour les utiliser et les répéter plus tard, ainsi que de créer des modèles pour les requêtes que vous souhaitez écrire. More information on using the [!DNL Query Service] API can be found in the [Query Service developer guide](api/getting-started.md).

## [!DNL Query Service] et [!DNL Experience Platform] services

[!DNL Query Service] interagit et peut être utilisé conjointement avec plusieurs [!DNL Experience Platform] services. In order to make the most out of [!DNL Query Service's] capabilities, it is recommended that you become familiar with these services and how they interact with [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] uses machine learning and artificial intelligence to gain insights from data stored within [!DNL Experience Platform]. [!DNL Data Science Workspace] permet aux scientifiques de données de créer des recettes basées sur des données d’enregistrement et de séries temporelles concernant les clients et leur activité, ce qui facilite les prédictions telles que la propension à acheter et les offres recommandées que l’individu est susceptible d’apprécier et de saisir. You can use SQL within [!DNL Data Science Workspace] by integrating [!DNL Query Service] into [!DNL JupyterLab], allowing you to explore, transform, and analyze Adobe Analytics data. Please read the [!DNL Data Science Workspace] overview for more information about [!DNL Data Science Workspace], and the [!DNL Query Service] integration guide for more information about how [!DNL Data Science Workspace] interacts with [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] allows users to divide their customers into smaller groups that share similar traits. These segments can subsequently be evaluated to provide better analysis on your [!DNL Real-time Customer Profile] data. [!DNL Query Service] peut être utilisé pour fournir cette analyse en exécutant des requêtes sur les données de ce segment dans le [!DNL Data Lake]. Please read the [!DNL Segmentation Service] overview for more information about segmentation, and the [!DNL Profile Query Language] (PQL) guide for more information on how to analyze segments.

### Cas d’utilisation de Looker BI

Adobe Experience Platform vous permet d&#39;assimiler, de stocker, de structurer et d&#39;extraire tous les jeux de données stockés, y compris les données comportementales, de gestion de la relation client et de point de vente. En utilisant [!DNL Experience Platform's Query Service]ces jeux de données, vous pouvez requête sur ces jeux de données et répondre à des questions spécifiques sur l’entreprise, puis début générant des informations d’impact. La vidéo suivante montre l&#39;utilité de la création de tableaux de bord dans les outils de Business Intelligence (BI) à l&#39;aide de [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Étapes suivantes et ressources supplémentaires

By reading this document, you have been introduced to [!DNL Query Service] and how it functions within the greater scope of [!DNL Experience Platform]. For more information on interacting with various endpoints within the [!DNL Query Service] API, please read the [Query Service developer guide](api/getting-started.md). For more information on using the interactive service within [!DNL Platform], please read the [Query Service user interface guide](ui/overview.md). For a comprehensive list on connecting external clients with [!DNL Query Service], please read the [Query Service clients overview](clients/overview.md).

Pour mieux vous préparer à exécuter des requêtes, regardez la vidéo suivante. Cette vidéo présente des conseils et les meilleures pratiques d’exécution des requêtes dans l’interface de l’éditeur de requêtes, les clients PSQL, les solutions Business Intelligence (BI) et l’API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
