---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Prise en main de l’apprentissage automatique en temps réel
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# Prise en main de l’apprentissage automatique en temps réel

>[!IMPORTANT]
>L&#39;apprentissage automatique en temps réel n&#39;est pas encore disponible pour tous les utilisateurs. Cette fonction est en alpha et est encore en cours de test. Ce document est sujet à changement.

Pour utiliser l’apprentissage automatique en temps réel, vous devez avoir accès à une organisation configurée avec Adobe Experience Platform et Data Science Workspace. De plus, vous devez disposer d&#39;un jeu de données dans Platform.

Les guides pour l&#39;apprentissage automatique en temps réel nécessitent une compréhension pratique des cahiers [Python 3, des cahiers](../jupyterlab/overview.md)Jupyter, des données et de l&#39;apprentissage automatique.

## Jeu de données dans Adobe Experience Platform

Pour début à l’aide de l’apprentissage automatique en temps réel, vous devez disposer d’un jeu de données renseigné dans Experience Platform. Vous avez la possibilité d&#39;utiliser un jeu de données externe et de le télécharger vers votre environnement JupyterLab ou de créer un nouveau jeu de données dans Platform si vous ne l&#39;avez pas déjà fait.

>[!NOTE]
>Si vous avez déjà un jeu de données à utiliser, vous pouvez ignorer les deux étapes suivantes.

### Utiliser un jeu de données externe

Pour en savoir plus sur l&#39;utilisation d&#39;un jeu de données externe tel que le transfert de données vers votre environnement JupyterLab, consultez le didacticiel sur l&#39; [analyse de vos données à l&#39;aide de portables](../jupyterlab/analyze-your-data.md#external-data).

### Créer un jeu de données

Pour créer un nouveau jeu de données destiné à l&#39;apprentissage automatique en temps réel, vous avez besoin d&#39;un schéma de données pour votre jeu de données. Ensuite, vous devez importer des données à l’aide du schéma que vous avez créé. Utilisez les didacticiels suivants pour créer et renseigner un jeu de données pour la plate-forme :

- [Création et remplissage d’un jeu de données dans l’API](../../catalog/datasets/create.md)
- [Création et remplissage d’un jeu de données dans l’interface utilisateur](../../ingestion/tutorials/ingest-batch-data.md)

## Git et Docker

Si vous envisagez de former un modèle à l&#39;aide du processus de recette en milieu de travail des sciences des données, Git et Docker sont requis.

>[!NOTE]
>Vous n&#39;avez pas besoin de télécharger Git and Docker si vous envisagez de former un modèle à l&#39;aide d&#39;un ordinateur portable Python ou si vous utilisez votre propre modèle ONNX.

- [Guide d&#39;installation Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Guide d&#39;installation du Docteur](https://docs.docker.com/get-docker/)

## Étapes suivantes

Une fois que vous avez préparé vos données pour l&#39;apprentissage automatique en temps réel, début en suivant le tutoriel sur la [formation d&#39;un modèle](./training-ml-model.md) pour apprendre à créer et télécharger un modèle ONNX dans la boutique de modèles d&#39;apprentissage automatique en temps réel.

