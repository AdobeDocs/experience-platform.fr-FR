---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query service;requête
solution: Experience Platform
title: Présentation de Query Service
description: Découvrez le rôle de Query Service dans Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 20%

---

# Présentation de Query Service

Adobe Experience Platform ingère des données à partir de sources diverses. Les marketeurs doivent comprendre ces données afin d’obtenir des informations sur leurs clients. Pour interroger des données dans Platform, vous pouvez utiliser SQL standard et Adobe Experience Platform Query Service. Vous pouvez utiliser Query Service pour joindre n’importe quel jeu de données dans le lac de données et capturer les résultats de la requête en tant que nouveau jeu de données à utiliser dans les rapports, l’apprentissage automatique ou pour l’ingestion dans [!DNL Real-Time Customer Profile]. Ce document donne une vue d’ensemble du rôle de Query Service dans Experience Platform.

Vous pouvez utiliser Query Service pour connecter le parcours client en ligne à hors ligne et comprendre l’attribution omnicanal de votre marque. La vidéo suivante montre comment une entreprise d’expérience peut utiliser Query Service pour traiter des cas d’utilisation clés et comment fonctionne Query Service.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilisation de Query Service {#usage}

Pour analyser vos données, créez et exécutez des requêtes SQL avec l’interface utilisateur de Query Service ou l’API RESTful.
Grâce à l’interface utilisateur de Query Service, vous pouvez écrire, exécuter et planifier des requêtes, afficher les requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs de votre entreprise. Vous pouvez également tester vos requêtes avant de les exécuter sur votre jeu de données plus large à l’aide de Query Editor. Consultez le [guide de l’interface utilisateur de Query Service](ui/overview.md) pour un aperçu de la fonctionnalité de l’interface utilisateur.

L’API RESTful offre une expérience similaire. Vous pouvez utiliser l’API Query Service pour écrire et exécuter des requêtes par programmation, créer et enregistrer des modèles pour les requêtes que vous souhaitez adapter ou planifier des requêtes pour une exécution automatisée. Pour plus d’informations sur l’utilisation de l’API Query Service, consultez le [guide de développement de Query Service](api/getting-started.md).

Pour commencer rapidement à utiliser les fonctionnalités de Query Service, il est recommandé de lire les documents suivants :

- [Directives générales pour l’exécution des requêtes](./best-practices/writing-queries.md)
- [Syntaxe SQL dans Query Service](./sql/syntax.md)
- [Création de jeux de données dérivés avec SQL](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## Query Service et services Experience Platform {#experience-platform-services}

Query Service interagit et peut être utilisé avec plusieurs services Experience Platform. Pour tirer le meilleur parti des fonctionnalités de Query Service, vous devez vous familiariser avec ces services et avec leur interaction avec Query Service. La [page d’entrée de la documentation Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=fr) fournit des résumés et des liens vers les fonctionnalités de la plateforme.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Les spécialistes des données peuvent utiliser le [!DNL Data Science Workspace] pour créer des recettes basées sur des données d’enregistrement et de série temporelle sur les clients et leurs activités. Ces recettes facilitent les prédictions telles que la propension à acheter et les offres recommandées que l’individu est susceptible d’apprécier et d’utiliser. Vous pouvez utiliser SQL dans [!DNL Data Science Workspace] en intégrant Query Service à [!DNL JupyterLab] pour explorer, transformer et analyser les données Adobe Analytics. Lisez la [[!DNL Data Science Workspace] présentation](../data-science-workspace/home.md) et le [ guide de connexion Jupyter Notebook](./clients/jupyter-notebook.md) pour plus d’informations sur la façon dont [!DNL Data Science Workspace] interagit avec Query Service.

### [!DNL Segmentation Service] {#segmentation}

Utilisez Adobe Experience Platform Segmentation Service pour diviser vos clients en groupes plus petits partageant des caractéristiques similaires. Ces audiences peuvent ensuite être évaluées afin de fournir une meilleure analyse de vos données Real-time Customer Profile. Vous pouvez utiliser Query Service pour exécuter des requêtes sur ces données d’audience dans le lac de données et fournir l’analyse. Lisez la [présentation de Segmentation Service](../segmentation/home.md) et le [[!DNL Profile Query Language] (PQL) guide](../segmentation/pql/overview.md) pour plus d’informations sur l’analyse des audiences.

## Cas d’utilisation {#use-cases}

Query Service offre une approche flexible de votre traitement des données qui a de nombreux objectifs. Entre autres, elle peut alléger le fardeau de la segmentation des spécialistes du marketing et contribuer à générer des audiences exploitables et des informations commerciales significatives. Les cas d’utilisation suivants présentent des exemples plus détaillés de la puissance de Query Service.

### Abandon de la navigation dans Adobe Analytics {#abandon-browse}

Cet [exemple d’abandon de la navigation est centré sur l’utilisation des données Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) pour créer une audience exploitable particulière. Query Service prend en charge une logique complexe de segmentation afin de calculer divers attributs personnalisés à utiliser en aval ou de simplifier considérablement la création de vos audiences.

## Génération d’informations avec des tableaux de bord personnalisés {#custom-dashboards}

Adobe Experience Platform vous permet dʼingérer, de stocker, de structurer et dʼextraire tous les jeux de données stockés, y compris les données comportementales, de gestion de la relation client et de point de vente. [!DNL Experience Platform's Query Service] vous permet dʼinterroger ces jeux de données et de répondre à des questions spécifiques sur lʼentreprise, puis de commencer à générer des informations pertinentes. Découvrez comment créer et gérer des tableaux de bord personnalisés dans lesquels vous pouvez créer, ajouter et modifier des widgets personnalisés pour visualiser des mesures clés avec des [ tableaux de bord définis par l’utilisateur ](../dashboards/user-defined-dashboards.md). Vous pouvez même [personnaliser vos propres rapports Real-Time CDP](../dashboards/data-models/cdp-insights-data-model-b2c.md) pour vos cas d’utilisation de marketing et d’indicateurs de performance clés en utilisant des requêtes SQL avec les modèles de données de Real-Time Customer Data Platform Insights.

## Étapes suivantes et ressources supplémentaires

Ce document vous a initié à Query Service et à son fonctionnement dans le cadre plus vaste d’Experience Platform. Pour continuer à découvrir les fonctionnalités de Query Service, nous vous recommandons de lire les documents suivants :

- [ Guide de développement de Query Service](api/getting-started.md) : pour plus d’informations sur l’interaction avec divers points de terminaison dans l’API Query Service.
- [ Guide de l’interface utilisateur de Query Service](ui/overview.md) : pour plus d’informations sur l’utilisation de Query Editor et de l’interface utilisateur.
- [ Présentation des clients de Query Service](clients/overview.md) : pour obtenir une liste complète de clients externes à connecter à Query Service.

Pour mieux vous préparer à exécuter des requêtes, regardez la vidéo suivante. Cette vidéo présente des conseils et des bonnes pratiques pour lʼexécution de requêtes dans lʼinterface de lʼéditeur de requêtes, les clients PSQL, les solutions Business Intelligence (BI) et lʼAPI HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
