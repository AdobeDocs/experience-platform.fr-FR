---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query service;requête
solution: Experience Platform
title: Présentation de Query Service
topic-legacy: overview
description: Ce document donne une vue d’ensemble du rôle de Query Service dans Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: c09a7a6198bf1ef3f94e53bdbdf3b0b93f6b2bd1
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 87%

---

# Présentation d’[!DNL Query Service]

Adobe Experience Platform ingère des données à partir de sources diverses. Le grand défi qui attend les spécialistes du marketing : comprendre ces données afin de découvrir des informations sur leurs clients. Adobe Experience Platform [!DNL Query Service] vous facilite la tâche en vous permettant dʼutiliser le langage SQL standard pour interroger des données dans [!DNL Platform]. Grâce à [!DNL Query Service], vous pouvez joindre nʼimporte quel jeu de données dans [!DNL Data Lake] et capturer les résultats de la requête sous forme dʼun nouveau jeu de données à utiliser dans un compte rendu des performances, dans le cadre de lʼapprentissage automatique ou pour être ingéré dans [!DNL Real-time Customer Profile]. Ce document donne une vue dʼensemble du rôle de [!DNL Query Service] dans [!DNL Experience Platform].

[!DNL Query Service] permet aux marques de relier le parcours client en ligne et hors ligne et de comprendre lʼattribution omnicanale. La vidéo suivante montre comment une entreprise orientée expérience peut tirer parti de [!DNL Query Service] pour traiter les cas dʼutilisation clés et la manière dont [!DNL Query Service] fonctionne.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilisation de [!DNL Query Service]

[!DNL Query Service] fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez créer des requêtes SQL pour mieux analyser vos données. L’interface utilisateur vous permet d’écrire et d’exécuter des requêtes, de visualiser des requêtes précédemment exécutées et d’accéder à des requêtes enregistrés par des utilisateurs au sein de votre organisation IMS. L’interface utilisateur est conçue pour être utilisée en tant qu’environnement de test pour vos requêtes avant de les exécuter sur votre jeu de données plus vaste. Pour plus dʼinformations sur lʼutilisation du service interactif dans [!DNL Platform], consultez le [guide de lʼinterface utilisateur de Query Service](ui/overview.md). L’API RESTful offre une expérience similaire vous permettant d’écrire et d’exécuter par programmation des requêtes, de planifier des requêtes pour les utiliser et les répéter plus tard, ainsi que de créer des modèles pour les requêtes que vous souhaitez écrire. Pour plus dʼinformations sur lʼutilisation de lʼAPI [!DNL Query Service], reportez-vous au [guide de développement de Query Service](api/getting-started.md).

## [!DNL Query Service] et les services de [!DNL Experience Platform]

[!DNL Query Service] interagit et peut être utilisé conjointement avec plusieurs services dʼ[!DNL Experience Platform]. Afin de tirer le meilleur parti des fonctionnalités de [!DNL Query Service's], il est recommandé de se familiariser avec ces services et de connaître leurs interactions avec [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilise lʼapprentissage automatique et lʼintelligence artificielle pour obtenir des informations à partir des données stockées dans [!DNL Experience Platform]. [!DNL Data Science Workspace] permet aux scientifiques de données de créer des recettes basées sur des données d’enregistrement et de séries temporelles concernant les clients et leur activité, ce qui facilite les prédictions telles que la propension à acheter et les offres recommandées que l’individu est susceptible d’apprécier et de saisir. Vous pouvez utiliser SQL dans [!DNL Data Science Workspace] en intégrant [!DNL Query Service] dans [!DNL JupyterLab], ce qui vous permettra dʼexplorer, de transformer et dʼanalyser les données dʼAdobe Analytics. Consultez la présentation de [!DNL Data Science Workspace] pour obtenir plus dʼinformations sur [!DNL Data Science Workspace], et le guide dʼintégration de [!DNL Query Service] pour plus dʼinformations sur les interactions entre [!DNL Data Science Workspace] et [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] permet aux utilisateurs de diviser leurs clients en plus petits groupes partageant des caractéristiques similaires. Ces segments peuvent ensuite être évalués afin de fournir une meilleure analyse de vos données [!DNL Real-time Customer Profile]. [!DNL Query Service] peut être utilisé pour fournir cette analyse en exécutant des requêtes sur ce segment de données dans [!DNL Data Lake]. Pour plus dʼinformations sur la segmentation, reportez-vous à la présentation de [!DNL Segmentation Service] et au guide de [!DNL Profile Query Language] (PQL) pour plus dʼinformations sur lʼanalyse des segments.

## Cas d&#39;utilisation

[!DNL Query Service] offre une approche flexible de votre traitement des données qui a de nombreux objectifs. Elle peut, entre autres, alléger la charge de la segmentation des marketeurs et contribuer à générer des audiences exploitables et des informations commerciales significatives. Les cas d’utilisation suivants présentent des exemples plus détaillés de la puissance de [!DNL Query Service].

### Abandon de navigation dans Adobe Analytics

Ceci [l’exemple d’abandon de navigation se concentre sur l’utilisation d’Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) pour créer une audience exploitable particulière. [!DNL Query Service] prend en charge une logique complexe de segmentation afin de calculer divers attributs personnalisés à utiliser en aval ou de simplifier considérablement la création de vos segments.

### Tableaux de bord Looker BI

Adobe Experience Platform vous permet dʼingérer, de stocker, de structurer et dʼextraire tous les jeux de données stockés, y compris les données comportementales, de gestion de la relation client et de point de vente. [!DNL Experience Platform's Query Service] vous permet dʼinterroger ces jeux de données et de répondre à des questions spécifiques sur lʼentreprise, puis de commencer à générer des informations pertinentes. La vidéo suivante montre lʼutilité de la création de tableaux de bord dans les outils de Business Intelligence (BI) à lʼaide de [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Étapes suivantes et ressources supplémentaires

Ce document vous a initié à [!DNL Query Service] et à son fonctionnement dans le cadre plus vaste dʼ[!DNL Experience Platform]. Pour plus dʼinformations sur les interactions avec divers points d’entrée dans lʼAPI [!DNL Query Service], consultez le [guide de développement de Query Service](api/getting-started.md). Pour plus dʼinformations sur lʼutilisation du service interactif dans [!DNL Platform], reportez-vous au [guide de lʼinterface utilisateur de Query Service](ui/overview.md). Pour une liste exhaustive portant sur la connexion des clients externes à [!DNL Query Service], reportez-vous à la [présentation des clients de Query Service](clients/overview.md).

Pour mieux vous préparer à exécuter des requêtes, regardez la vidéo suivante. Cette vidéo présente des conseils et des bonnes pratiques pour lʼexécution de requêtes dans lʼinterface de lʼéditeur de requêtes, les clients PSQL, les solutions Business Intelligence (BI) et lʼAPI HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
