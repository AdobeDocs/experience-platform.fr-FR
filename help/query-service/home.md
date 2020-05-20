---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Requête Service
topic: overview
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---


# Présentation du service Requête

Adobe Experience Platform ingère des données provenant de sources très diverses. Pour les spécialistes du marketing, l’un des principaux défis consiste à comprendre ces données afin d’obtenir des informations sur leurs clients. Adobe Experience Platform Requête Service facilite cette tâche en vous permettant d’utiliser des données de requête SQL standard dans Platform. Requête Service vous permet de joindre n’importe quel jeu de données dans Data Lake et de capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans le rapports, l’apprentissage automatique ou pour l’assimilation dans le Profil client en temps réel. Ce document présente un aperçu du rôle de Requête Service dans Experience Platform.

## Utilisation de Requête Service

Requête Service fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez créer des requêtes SQL pour mieux analyser vos données. L&#39;interface utilisateur vous permet d&#39;écrire et d&#39;exécuter des requêtes, des vues de requêtes précédemment exécutées et des requêtes d&#39;accès enregistrées par les utilisateurs de votre organisation IMS. L’interface utilisateur est destinée à être utilisée comme sandbox pour tester vos requêtes avant de les exécuter sur votre jeu de données plus large. Pour plus d’informations sur l’utilisation du service interactif dans Platform, consultez le guide [de l’interface utilisateur de](ui/overview.md)Requête Service. L’API RESTful offre une expérience similaire, vous permettant d’écrire et d’exécuter par programmation des requêtes, de planifier des requêtes pour une utilisation et une répétition futures, ainsi que de créer des modèles pour les requêtes que vous souhaitez écrire. Pour plus d&#39;informations sur l&#39;utilisation de l&#39;API Requête Service, consultez le guide [du développeur](api/getting-started.md)Requête Service.

## Services de Requête et de plate-forme d’expérience

Requête Service interagit et peut être utilisé conjointement avec plusieurs services Experience Platform. Afin de tirer le meilleur parti des fonctionnalités de Requête Service, il est recommandé de se familiariser avec ces services et de savoir comment ils interagissent avec Requête Service.

### Espace de travail Data Science

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Data Science Workspace permet aux chercheurs en données de créer des recettes basées sur des données de série chronologique et d&#39;enregistrement sur les clients et leurs activités, ce qui facilite les prédictions telles que la propension à acheter et les offres recommandées que l&#39;individu est susceptible d&#39;apprécier et d&#39;utiliser. Vous pouvez utiliser SQL dans Data Science Workspace en intégrant Requête Service dans JupyterLab, ce qui vous permet d’explorer, de transformer et d’analyser les données Adobe Analytics. Pour plus d’informations sur Data Science Workspace et sur le guide d’intégration de Requête Service, consultez l’aperçu de Data Science Workspace. Pour en savoir plus sur les interactions entre Data Science Workspace et Requête Service, consultez le Guide d’intégration de Data Science Workspace.

### Service de segmentation

Adobe Experience Platform Segmentation Service permet aux utilisateurs de diviser leurs clients en groupes plus petits qui partagent des caractéristiques similaires. Ces segments peuvent ensuite être évalués afin de fournir une meilleure analyse sur vos données de Profil client en temps réel. Requête Service peut être utilisé pour fournir cette analyse en exécutant des requêtes sur ces données de segment dans Data Lake. Pour plus d&#39;informations sur la segmentation, consultez l&#39;aperçu du service de segmentation et le guide PQL (Profil Requête Language).

## Étapes suivantes

En lisant ce document, vous avez été initié à Requête Service et à son fonctionnement dans le cadre plus large de Experience Platform. Pour plus d&#39;informations sur l&#39;interaction avec divers points de terminaison dans l&#39;API Requête Service, consultez le guide [du développeur](api/getting-started.md)Requête Service. Pour plus d&#39;informations sur l&#39;utilisation du service interactif dans Platform, veuillez lire le guide [de l&#39;interface utilisateur de](ui/overview.md)Requête Service. Pour obtenir une liste complète sur la connexion de clients externes à Requête Service, veuillez lire l&#39;aperçu [des clients de](clients/overview.md)Requête Service.
