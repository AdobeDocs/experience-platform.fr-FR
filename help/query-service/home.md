---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de requête ; service de Requête ; requête
solution: Experience Platform
title: Présentation du service requête
topic-legacy: overview
description: Ce document donne une vue d’ensemble du rôle de Query Service dans Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 28%

---

# [!DNL Query Service] présentation

Adobe Experience Platform ingère des données à partir de sources diverses. Le grand défi qui attend les spécialistes du marketing : comprendre ces données afin de découvrir des informations sur leurs clients. Adobe Experience Platform [!DNL Query Service] facilite cela en vous permettant d&#39;utiliser des données SQL standard pour la requête dans [!DNL Platform]. [!DNL Query Service] vous permet de joindre n&#39;importe quel jeu de données dans [!DNL Data Lake] et de capturer les résultats de la requête sous la forme d&#39;un nouveau jeu de données à utiliser dans le rapports, l&#39;apprentissage automatique ou pour l&#39;assimilation dans [!DNL Real-time Customer Profile]. Ce document donne un aperçu du rôle de [!DNL Query Service] dans [!DNL Experience Platform].

[!DNL Query Service] permet aux marques de connecter le parcours client en ligne au  client hors ligne et de comprendre l’attribution entre canaux multiples. La vidéo suivante montre comment une entreprise peut tirer parti de [!DNL Query Service] pour traiter les cas d&#39;utilisation clés et comment [!DNL Query Service] fonctionne.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Utilisation de [!DNL Query Service]

[!DNL Query Service] fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez créer des requêtes SQL pour mieux analyser vos données. L’interface utilisateur vous permet d’écrire et d’exécuter des requêtes, de visualiser des requêtes précédemment exécutées et d’accéder à des requêtes enregistrés par des utilisateurs au sein de votre organisation IMS. L’interface utilisateur est conçue pour être utilisée en tant qu’environnement de test pour vos requêtes avant de les exécuter sur votre jeu de données plus vaste. Pour plus d&#39;informations sur l&#39;utilisation du service interactif dans [!DNL Platform], consultez le [Guide de l&#39;interface utilisateur du service de Requête](ui/overview.md). L’API RESTful offre une expérience similaire vous permettant d’écrire et d’exécuter par programmation des requêtes, de planifier des requêtes pour les utiliser et les répéter plus tard, ainsi que de créer des modèles pour les requêtes que vous souhaitez écrire. Pour plus d&#39;informations sur l&#39;utilisation de l&#39;API [!DNL Query Service], consultez le [Requête Service Developer Guide](api/getting-started.md).

## [!DNL Query Service] et  [!DNL Experience Platform] services

[!DNL Query Service] interagit et peut être utilisé conjointement avec plusieurs  [!DNL Experience Platform] services. Afin de tirer le meilleur parti des fonctionnalités [!DNL Query Service's], il est recommandé de se familiariser avec ces services et de connaître leur interaction avec [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour obtenir des informations sur les données stockées dans [!DNL Experience Platform]. [!DNL Data Science Workspace] permet aux scientifiques de données de créer des recettes basées sur des données d’enregistrement et de séries temporelles concernant les clients et leur activité, ce qui facilite les prédictions telles que la propension à acheter et les offres recommandées que l’individu est susceptible d’apprécier et de saisir. Vous pouvez utiliser SQL dans [!DNL Data Science Workspace] en intégrant [!DNL Query Service] dans [!DNL JupyterLab], ce qui vous permet d&#39;explorer, de transformer et d&#39;analyser les données Adobe Analytics. Veuillez consulter l&#39;[!DNL Data Science Workspace] vue d&#39;ensemble pour plus d&#39;informations sur [!DNL Data Science Workspace] et le guide d&#39;intégration [!DNL Query Service] pour plus d&#39;informations sur les interactions de [!DNL Data Science Workspace] avec [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] permet aux utilisateurs de diviser leurs clients en groupes plus petits qui partagent des caractéristiques similaires. Ces segments peuvent ensuite être évalués afin de fournir une meilleure analyse sur vos données [!DNL Real-time Customer Profile]. [!DNL Query Service] peut être utilisé pour fournir cette analyse en exécutant des requêtes sur les données de ce segment dans le  [!DNL Data Lake]. Pour plus d&#39;informations sur la segmentation, consultez l&#39;aperçu [!DNL Segmentation Service] et le guide [!DNL Profile Query Language] (PQL) pour plus d&#39;informations sur l&#39;analyse des segments.

### Cas d’utilisation de Looker BI

Adobe Experience Platform vous permet d&#39;assimiler, de stocker, de structurer et d&#39;extraire tous les jeux de données stockés, y compris les données comportementales, de gestion de la relation client et de point de vente. [!DNL Experience Platform's Query Service] vous permet de requête sur ces jeux de données et de répondre à des questions spécifiques sur l&#39;entreprise, puis de générer des débuts d&#39;informations pertinentes. La vidéo suivante montre l&#39;utilité de la création de tableaux de bord dans les outils de Business Intelligence (BI) à l&#39;aide de [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Étapes suivantes et ressources supplémentaires

En lisant ce document, vous avez été initié à [!DNL Query Service] et à son fonctionnement dans la portée plus large de [!DNL Experience Platform]. Pour plus d&#39;informations sur l&#39;interaction avec divers points de terminaison dans l&#39;API [!DNL Query Service], consultez le [Guide du développeur de Requête Service](api/getting-started.md). Pour plus d&#39;informations sur l&#39;utilisation du service interactif dans [!DNL Platform], consultez le [Guide de l&#39;interface utilisateur du service de Requête](ui/overview.md). Pour obtenir une liste complète sur la connexion des clients externes à [!DNL Query Service], veuillez consulter la [présentation des clients de Requête Service](clients/overview.md).

Pour mieux vous préparer à exécuter des requêtes, regardez la vidéo suivante. Cette vidéo présente des conseils et les meilleures pratiques d’exécution des requêtes dans l’interface de l’éditeur de requêtes, les clients PSQL, les solutions Business Intelligence (BI) et l’API HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
