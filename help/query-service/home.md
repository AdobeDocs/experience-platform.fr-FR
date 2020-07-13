---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Query Service
topic: overview
translation-type: tm+mt
source-git-commit: cfd767a05ad4c1dd43ac2bdde1966f9c89f5d219
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 81%

---


# Présentation de Query Service

Adobe Experience Platform ingère des données à partir de sources diverses. Le grand défi qui attend les spécialistes du marketing : comprendre ces données afin de découvrir des informations sur leurs clients. Adobe Experience Platform Query Service vous facilite la tâche en vous permettant d’utiliser le langage SQL standard pour interroger des données dans Platform. Grâce à Query Service, vous pouvez joindre n’importe quel jeu de données dans le lac de données et capturer les résultats de la requête sous forme d’un nouveau jeu de données à utiliser dans un compte rendu des performances, dans le cadre de l’apprentissage automatique ou pour être ingéré dans Real-time Customer Profile. Ce document donne une vue d’ensemble du rôle de Query Service dans Experience Platform.

Requête Service permet aux marques de relier le parcours client en ligne à hors ligne et de comprendre l’attribution entre canaux multiples. La vidéo suivante montre comment une entreprise peut tirer parti de Requête Service pour traiter les cas d&#39;utilisation clés et comment fonctionne Requête Service.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilisation de Query Service

Query Service fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez créer des requêtes SQL pour mieux analyser vos données. L’interface utilisateur vous permet d’écrire et d’exécuter des requêtes, de visualiser des requêtes précédemment exécutées et d’accéder à des requêtes enregistrés par des utilisateurs au sein de votre organisation IMS. L’interface utilisateur est conçue pour être utilisée en tant qu’environnement de test pour vos requêtes avant de les exécuter sur votre jeu de données plus vaste. Pour plus d’informations sur l’utilisation du service interactif dans Platform, consultez le [guide de l’interface utilisateur de Query Service](ui/overview.md). L’API RESTful offre une expérience similaire vous permettant d’écrire et d’exécuter par programmation des requêtes, de planifier des requêtes pour les utiliser et les répéter plus tard, ainsi que de créer des modèles pour les requêtes que vous souhaitez écrire. Pour plus d’informations sur l’utilisation de l’API de Query Service, reportez-vous au [guide de développement de Query Service](api/getting-started.md).

## Query Service et services Experience Platform

Query Service interagit et peut être utilisé conjointement avec plusieurs services d’Experience Platform. Afin de tirer le meilleur parti des capacités de Query Service, il est recommandé de se familiariser avec ces services et de connaître leurs interactions avec Query Service.

### Data Science Workspace

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Data Science Workspace permet aux scientifiques de données de créer des recettes basées sur des données d’enregistrement et de séries temporelles concernant les clients et leur activité, ce qui facilite les prédictions telles que la propension à acheter et les offres recommandées que l’individu est susceptible d’apprécier et de saisir. Vous pouvez utiliser SQL dans Data Science Workspace en intégrant Query Service à JupyterLab, ce qui vous permettra d’explorer, de transformer et d’analyser les données d’Adobe Analytics. Pour plus d’informations sur Data Science Workspace, consultez la présentation de Data Science Workspace et le guide d’intégration de Query Service pour plus d’informations sur les interactions entre Data Science Workspace et Query Service.

### Segmentation Service

Adobe Experience Platform Segmentation Service permet aux utilisateurs de diviser leurs clients en plus petits groupes partageant des caractéristiques similaires. Ces segments peuvent ensuite être évalués afin de fournir une meilleure analyse de vos données Real-time Customer Profile. Query Service peut être utilisé pour fournir cette analyse en exécutant des requêtes sur ce segment de données au sein du lac de données. Pour plus d’informations sur la segmentation, reportez-vous à la présentation de Segmentation Service et au guide PQL (Langage de requête de profil) pour plus d’informations sur l’analyse des segments.

### Cas d’utilisation de Looker BI

Avec l&#39;Adobe Experience Platform, vous pouvez ingérer, stocker, structurer et extraire tous les jeux de données stockés — y compris les données comportementales, CRM et de point de vente. En utilisant [!DNL Experience Platform's Query Service]ces jeux de données, vous pouvez requête sur ces jeux de données et répondre à des questions spécifiques sur l’entreprise, puis début générant des informations d’impact. La vidéo suivante montre l&#39;utilité de la création de tableaux de bord dans les outils de Business Intelligence (BI) à l&#39;aide de [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Étapes suivantes et ressources supplémentaires

Ce document vous a initié à Query Service et à son fonctionnement dans le cadre plus vaste d’Experience Platform. Pour plus d’informations sur les interactions avec divers points de terminaison dans l’API de Query Service, consultez le [guide de développement de Query Service](api/getting-started.md). Pour plus d’informations sur l’utilisation du service interactif dans Platform, reportez-vous au [guide de l’interface utilisateur de Query Service](ui/overview.md). Pour une liste exhaustive portant sur la connexion des clients externes à Query Service, reportez-vous à la [présentation des clients de Query Service](clients/overview.md).

Pour mieux vous préparer à exécuter des requêtes, regardez la vidéo suivante. Cette vidéo présente des conseils et les meilleures pratiques d’exécution des requêtes dans l’interface de l’éditeur de requêtes, les clients PSQL, les solutions Business Intelligence (BI) et l’API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
