---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Prise en main de l’apprentissage automatique en temps réel
topic: Getting started
translation-type: tm+mt
source-git-commit: dc63ad0c0764355aed267eccd1bcc4965b04dba4
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Prise en main de l’apprentissage automatique en temps réel (Alpha)

>[!IMPORTANT]
>L&#39;apprentissage automatique en temps réel n&#39;est pas encore disponible pour tous les utilisateurs. Cette fonction est en alpha et est encore en cours de test. Ce document est sujet à changement.

Pour utiliser l’apprentissage automatique en temps réel, vous devez avoir accès à une organisation configurée avec Adobe Experience Platform et Data Science Workspace. De plus, vous devez disposer d’un jeu de données complet pour la formation et la notation.

Les guides pour l&#39;apprentissage automatique en temps réel exigent une compréhension pratique des cahiers [Python 3, des cahiers](../jupyterlab/overview.md)Jupyter, des données et de l&#39;apprentissage automatique.

Termes clés:

- **DSL :** Langue spécifique au domaine.
- **Edge :** Le service de notation en temps réel de l&#39;apprentissage automatique peut être exécuté sur des clusters Edge plus proches de vos activations et applications.
- **Hub :** L’alpha actuel exécute le service de notation d’apprentissage automatique en temps réel sur le hub Adobe Experience Platform pendant que le réseau Experience Edge Network est en cours de développement.
- **Noeud :** Un noeud est l’unité fondamentale dont les graphiques sont formés. Chaque noeud exécute une tâche spécifique et peut être chaîné ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche exécutée par un noeud représente une opération sur les données d’entrée, telle qu’une transformation de données ou de schéma, ou une inférence d’apprentissage automatique. Le noeud envoie la valeur transformée ou déduite au(x) noeud(s) suivant(s).

## Jeu de données dans Adobe Experience Platform

Pour début à l&#39;aide de l&#39;apprentissage automatique en temps réel, vous devez avoir accès à un jeu de données. Vous avez la possibilité d&#39;utiliser un jeu de données externe et de le télécharger vers votre environnement JupyterLab ou de créer un nouveau jeu de données dans Platform si vous ne l&#39;avez pas déjà fait.

>[!NOTE]
>Si vous avez déjà un jeu de données à utiliser, vous pouvez passer aux étapes [](#next-steps)suivantes.

### Utiliser un jeu de données externe

Pour en savoir plus sur l&#39;utilisation d&#39;un jeu de données externe tel que le transfert de données vers votre environnement JupyterLab, consultez le didacticiel sur l&#39; [analyse de vos données à l&#39;aide de portables](../jupyterlab/analyze-your-data.md#external-data).

### Créer un jeu de données

Pour créer un nouveau jeu de données destiné à l&#39;apprentissage automatique en temps réel, vous avez besoin d&#39;un schéma de données pour votre jeu de données. Ensuite, vous devez importer des données à l’aide du schéma que vous avez créé. Utilisez les didacticiels suivants pour créer et renseigner un jeu de données pour la plate-forme :

- [Création et remplissage d’un jeu de données dans l’API](../../catalog/datasets/create.md)
- [Création et remplissage d’un jeu de données dans l’interface utilisateur](../../ingestion/tutorials/ingest-batch-data.md)

## Étapes suivantes {#next-steps}

Une fois que vous avez préparé vos données pour l&#39;apprentissage automatique en temps réel, début en suivant le guide [d&#39;utilisation du portable d&#39;apprentissage automatique en temps](./rtml-authoring-notebook.md) réel pour apprendre à créer et à télécharger un modèle ONNX dans la boutique de modèles d&#39;apprentissage automatique en temps réel.

