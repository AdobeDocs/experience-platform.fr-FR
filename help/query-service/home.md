---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Service  Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Présentation du service 

Adobe Experience Platform imprime des données à partir d’un large éventail de sources. Les spécialistes du marketing doivent comprendre ces données pour mieux comprendre leurs clients. Le service de Adobe Experience Platform facilite cette tâche en vous permettant d’utiliser le langage SQL standard pour  des données dans Platform. Grâce au service de , vous pouvez joindre n’importe quel jeu de données dans Data Lake et capturer les résultats de l’ sous forme d’un nouveau jeu de données à utiliser dans le cadre de l’apprentissage automatique ou dans le cadre de l’assimilation dans le client en temps réel. Ce donne une vue d’ensemble du rôle de  Service dans Experience Platform.

## Utilisation du service 

Le service de  de fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez créer des  SQL pour mieux analyser vos données. L&#39;interface utilisateur vous permet d&#39;écrire et d&#39;exécuter des  de, des  de précédemment exécutés et d&#39;accéder à des enregistrés par des utilisateurs au sein de votre organisation IMS. L’interface utilisateur est conçue pour être utilisée comme un sandbox afin de tester vos  de avant de les exécuter sur votre jeu de données plus large. Pour plus d’informations sur l’utilisation du service interactif dans Platform, consultez le guide [de l’interface utilisateur du service de](ui/overview.md)de. L’API RESTful offre une expérience similaire, vous permettant d’écrire et d’exécuter par programmation des  de, de programmer des  pour une utilisation et une répétition futures, ainsi que de créer des modèles pour les  que vous souhaitez écrire. Pour plus d&#39;informations sur l&#39;utilisation de l&#39;API de service , reportez-vous au guide [du développeur du service ](api/getting-started.md).

## Services de  et de plateforme d’expérience

Le service  interagit et peut être utilisé conjointement avec plusieurs services Experience Platform. Afin de tirer le meilleur parti des capacités du service , il est recommandé de se familiariser avec ces services et de connaître leur interaction avec le service .

### Espace de travail Data Science

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Data Science Workspace permet aux chercheurs de données de créer des recettes basées sur des données d’enregistrement et de séries chronologiques sur les clients et leurs  de , ce qui facilite les prédictions telles que la propension à acheter et les recommandations d’ de que l’individu est susceptible d’apprécier et d’utiliser. Vous pouvez utiliser SQL dans Data Science Workspace en intégrant le service de  dans JupyterLab, afin d’explorer, de transformer et d’analyser les données Adobe Analytics. Pour plus d’informations sur l’espace de travail Data Science, consultez l’aperçu de l’espace de travail Data Science Workspace et le guide d’intégration du service de  de données pour plus d’informations sur l’interaction de l’espace de travail Data Science avec le service de .

### Service de segmentation

Adobe Experience Platform Segmentation Service permet aux utilisateurs de diviser leurs clients en groupes plus petits qui partagent des caractéristiques similaires. Ces segments peuvent ensuite être évalués afin de fournir de meilleurs   sur vos données de en temps réel du client. Le service de  peut être utilisé pour fournir ce   de en exécutant desdonnées sur ce segment dans le lac Data. Pour plus d’informations sur la segmentation, reportez-vous à la présentation du service de segmentation et au guide PQL ( Language) pour plus d’informations sur l’analyse des segments.

## Étapes suivantes

En lisant ce , vous avez été initié à  Service et à son fonctionnement dans le cadre plus large d’Experience Platform. Pour plus d&#39;informations sur l&#39;interaction avec divers points de fin dans l&#39;API du service de , consultez le guide [du développeur du service de ](api/getting-started.md). Pour plus d’informations sur l’utilisation du service interactif dans Platform, veuillez lire le guide [de l’interface utilisateur du service](ui/overview.md)de plateforme. Pour un complet sur la connexion des clients externes au service , veuillez lire l&#39;aperçu [des clients du service](clients/overview.md).
