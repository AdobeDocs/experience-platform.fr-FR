---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience le 10 juin 2020
doc-type: release notes
last-update: June 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: b6cfdf56c20065bdc3e8a9fedf6007ddd74eaeaa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 6%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 10 juin 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Espace de travail Data Science](#dsw)
- [Sources](#sources)

## Espace de travail Data Science {#dsw}

Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour générer des informations à partir de vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous permet de faire des prédictions à l’aide de vos contenus et de vos ressources de données dans les solutions Adobe.

Data Science Workspace a travaillé sur de nouveaux moyens pour permettre de meilleures expériences et prédictions grâce à l’utilisation de l’apprentissage automatique en temps réel. L&#39;apprentissage automatique en temps réel permet de créer, tester et déployer des modèles d&#39;apprentissage automatique préformés sur mesure ou importés dans des formats de modèles interopérables standard du secteur pour un score/activation en temps réel via un point de terminaison API.

Notez que l&#39;apprentissage automatique en temps réel est en alpha et est encore en cours de développement.

| Fonction | Description |
|--- | ---|
| JupyterLab Launcher Démarrage ML en temps réel | Le JupyterLab Launcher inclut désormais un ordinateur portable Python pour Real-time Machine Learning (Alpha). |

Pour plus d&#39;informations sur l&#39;alpha d&#39;apprentissage automatique en temps réel, consultez la présentation [de l&#39;apprentissage automatique en temps](../../data-science-workspace/real-time-machine-learning/home.md)réel.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plate-forme. Vous pouvez ingérer des données à partir de diverses sources, telles que des applications Adobe, des enregistrements basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent d’authentifier et de vous connecter à des systèmes d’enregistrement externes et à des services de gestion de la relation client, de définir les heures d’exécution d’assimilation et de gérer le débit d’assimilation des données.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ------- | ----------- |
| Prise en charge d’API et d’interface utilisateur supplémentaires pour les systèmes d’enregistrement cloud | Nouveau connecteur source pour Apache HDFS |
| Prise en charge supplémentaire des API et de l’interface utilisateur pour les bases de données | Nouveau connecteur source pour Couchbase. |

Pour en savoir plus sur les sources, consultez l’aperçu [des](../../sources/home.md)sources.
