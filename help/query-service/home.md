---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query service;requête
solution: Experience Platform
title: Présentation de Query Service
description: Découvrez le rôle de Query Service dans Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e06519978ed9c6128be53a15cef3046a0dbc2a16
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 25%

---

# Présentation de Query Service

Adobe Experience Platform ingère des données à partir de sources diverses. Les marketeurs doivent comprendre ces données afin d’obtenir des informations sur leurs clients. Pour interroger des données dans Platform, vous pouvez utiliser SQL standard et Adobe Experience Platform Query Service. Vous pouvez utiliser Query Service pour joindre n’importe quel jeu de données dans le lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, l’apprentissage automatique ou pour ingestion dans . [!DNL Real-Time Customer Profile]. Ce document donne une vue d’ensemble du rôle de Query Service dans Experience Platform.

Vous pouvez utiliser Query Service pour connecter le parcours client en ligne à hors ligne et comprendre l’attribution omnicanal de votre marque. La vidéo suivante montre comment une entreprise d’expérience peut utiliser Query Service pour traiter des cas d’utilisation clés et comment fonctionne Query Service.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilisation de Query Service {#usage}

Pour analyser vos données, vous pouvez utiliser l’interface utilisateur de Query Service et une API RESTful, à partir de laquelle vous pouvez créer des requêtes SQL. L’interface utilisateur vous permet d’écrire et d’exécuter des requêtes, de visualiser des requêtes précédemment exécutées et d’accéder à des requêtes enregistrées par des utilisateurs et utilisatrices au sein de votre organisation. Vous pouvez utiliser l’éditeur de requêtes comme un environnement de test pour tester vos requêtes avant de les exécuter sur votre jeu de données plus vaste. Voir [Guide de l’interface utilisateur de Query Service](ui/overview.md) pour plus d’informations sur l’utilisation de l’interface utilisateur. L’API RESTful offre une expérience similaire. Vous pouvez utiliser l’API Query Service pour écrire et exécuter des requêtes par programmation, planifier des requêtes pour une utilisation et une répétition futures, ainsi que créer des modèles pour les requêtes que vous souhaitez écrire. Pour plus d’informations sur l’utilisation de l’API de Query Service, reportez-vous au [guide de développement de Query Service](api/getting-started.md).

## Query Service et services Experience Platform {#experience-platform-services}

Query Service interagit et peut être utilisé avec plusieurs services Experience Platform. Pour tirer le meilleur parti des fonctionnalités de Query Service, vous devez vous familiariser avec ces services et avec leur interaction avec Query Service. La variable [Page d’entrée de la documentation Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=fr) fournit des résumés et des liens vers les fonctionnalités de la plateforme.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Les spécialistes des données peuvent utiliser la variable [!DNL Data Science Workspace] pour créer des recettes basées sur des données d’enregistrement et de série temporelle concernant les clients et leurs activités. Ces recettes facilitent les prédictions telles que la propension à acheter et les offres recommandées que l’individu est susceptible d’apprécier et d’utiliser. Vous pouvez utiliser SQL dans [!DNL Data Science Workspace] en intégrant Query Service à [!DNL JupyterLab] pour explorer, transformer et analyser les données Adobe Analytics. Lisez la section [[!DNL Data Science Workspace] aperçu](../data-science-workspace/home.md) et la variable [Guide de connexion Jypiter Notebook](./clients/jupyter-notebook.md) pour plus d’informations sur la manière dont [!DNL Data Science Workspace] interagit avec Query Service.

### [!DNL Segmentation Service] {#segmentation}

Utilisez Adobe Experience Platform Segmentation Service pour diviser vos clients en groupes plus petits partageant des caractéristiques similaires. Ces audiences peuvent ensuite être évaluées afin de fournir une meilleure analyse de vos données Real-time Customer Profile. Vous pouvez utiliser Query Service pour exécuter des requêtes sur ces données d’audience dans le lac de données et fournir l’analyse. Lisez la section [Présentation de Segmentation Service](../segmentation/home.md) et la variable [[!DNL Profile Query Language] Guide (PQL)](../segmentation/pql/overview.md) pour plus d’informations sur l’analyse des audiences.

## Cas d’utilisation {#use-cases}

Query Service offre une approche flexible de votre traitement des données qui a de nombreux objectifs. Entre autres, elle peut alléger le fardeau de la segmentation des spécialistes du marketing et contribuer à générer des audiences exploitables et des informations commerciales significatives. Les cas d’utilisation suivants présentent des exemples plus détaillés de la puissance de Query Service.

### Abandon de la navigation dans Adobe Analytics {#abandon-browse}

Cet [exemple d’abandon de la navigation est centré sur l’utilisation des données Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) pour créer une audience exploitable particulière. Query Service prend en charge une logique complexe de segmentation afin de calculer divers attributs personnalisés à utiliser en aval ou de simplifier considérablement la création de vos audiences.

## Génération d’informations avec des tableaux de bord personnalisés {#custom-dashboards}

Adobe Experience Platform vous permet dʼingérer, de stocker, de structurer et dʼextraire tous les jeux de données stockés, y compris les données comportementales, de gestion de la relation client et de point de vente. [!DNL Experience Platform's Query Service] vous permet dʼinterroger ces jeux de données et de répondre à des questions spécifiques sur lʼentreprise, puis de commencer à générer des informations pertinentes. Découvrez comment créer et gérer des tableaux de bord personnalisés dans lesquels vous pouvez créer, ajouter et modifier des widgets personnalisés pour visualiser des mesures clés avec [tableaux de bord définis par l’utilisateur](../dashboards/user-defined-dashboards.md). Vous pouvez même [personnaliser vos propres rapports Real-Time CDP ;](../dashboards/cdp-insights-data-model.md) pour vos cas d’utilisation marketing et IPC en utilisant des requêtes SQL avec les modèles de données Real-time Customer Data Platform Insights.

## Étapes suivantes et ressources supplémentaires

Ce document vous a initié à Query Service et à son fonctionnement dans le cadre plus vaste d’Experience Platform. Pour continuer à découvrir les fonctionnalités de Query Service, nous vous recommandons de lire les documents suivants :

- La variable [Guide de développement de Query Service](api/getting-started.md): pour plus d’informations sur l’interaction avec divers points de terminaison dans l’API Query Service.
- La variable [Guide de l’interface utilisateur de Query Service](ui/overview.md): pour plus d’informations sur l’utilisation de Query Editor et de l’interface utilisateur.
- La variable [Présentation des clients de Query Service](clients/overview.md): pour obtenir une liste complète des clients externes à qui se connecter à Query Service.

Pour mieux vous préparer à exécuter des requêtes, regardez la vidéo suivante. Cette vidéo présente des conseils et des bonnes pratiques pour lʼexécution de requêtes dans lʼinterface de lʼéditeur de requêtes, les clients PSQL, les solutions Business Intelligence (BI) et lʼAPI HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
