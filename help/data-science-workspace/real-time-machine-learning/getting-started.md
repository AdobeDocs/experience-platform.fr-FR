---
keywords: Experience Platform ; guide du développeur ; Espace de travail des données ; sujets populaires ; apprentissage automatique en temps réel ;
solution: Experience Platform
title: Prise en main de l'apprentissage automatique en temps réel
topic-legacy: Getting started
description: Le document suivant décrit les étapes requises pour créer un modèle d’apprentissage automatique en temps réel dans Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Prise en main de l’apprentissage automatique en temps réel (Alpha)

>[!IMPORTANT]
>
>L&#39;apprentissage automatique en temps réel n&#39;est pas encore disponible pour tous les utilisateurs. Cette fonction est en alpha et est encore en cours de test. Ce document est sujet à changement.

Pour utiliser l&#39;apprentissage automatique en temps réel, vous devez avoir accès à une organisation configurée avec Adobe Experience Platform et [!DNL Data Science Workspace]. De plus, vous devez disposer d’un jeu de données complet pour la formation et la notation.

Les guides pour l&#39;apprentissage automatique en temps réel exigent une compréhension pratique de Python 3, [Portables Jupyter](../jupyterlab/overview.md), de la science des données et de l&#39;apprentissage automatique.

**Termes clés:**

- **DSL : langue spécifique au** domaine.
- **Le service de notation** d&#39;apprentissage automatique en temps réel peut être exécuté sur des clusters Edge plus proches de vos activations et applications.
- **Hub :** l’alpha actuel exécute le service de score d’apprentissage automatique en temps réel sur le Adobe Experience Platform Hub tandis que le réseau Experience Edge Network est en cours de développement.
- **Noeud :** un noeud est l’unité fondamentale dont les graphiques sont formés. Chaque noeud exécute une tâche spécifique et peut être chaîné ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche exécutée par un noeud représente une opération sur les données d’entrée, telle qu’une transformation de données ou de schéma, ou une inférence d’apprentissage automatique. Le noeud envoie la valeur transformée ou déduite au(x) noeud(s) suivant(s).

## Jeu de données au Adobe Experience Platform

Pour début à l&#39;aide de l&#39;apprentissage automatique en temps réel, vous devez avoir accès à un jeu de données. Vous avez la possibilité d&#39;utiliser un jeu de données externe et de le télécharger vers votre environnement [!DNL JupyterLab] ou de créer un nouveau jeu de données dans Platform si vous ne l&#39;avez pas déjà fait.

>[!NOTE]
>
>Si vous avez déjà un jeu de données à utiliser, vous pouvez passer à [Étapes suivantes](#next-steps).

### Utiliser un jeu de données externe

Pour en savoir plus sur l&#39;utilisation d&#39;un jeu de données externe tel que le transfert de données vers votre environnement [!DNL JupyterLab], consultez le didacticiel sur l&#39;[analyse de vos données à l&#39;aide de blocs-notes](../jupyterlab/analyze-your-data.md#external-data).

### Création d’un nouveau jeu de données

Pour créer un nouveau jeu de données destiné à l&#39;apprentissage automatique en temps réel, vous avez besoin d&#39;un schéma de données pour votre jeu de données. Ensuite, vous devez importer des données à l’aide du schéma que vous avez créé. Utilisez les didacticiels suivants pour créer et renseigner un jeu de données pour [!DNL Platform] :

- [Création et remplissage d’un jeu de données dans l’API](../../catalog/datasets/create.md)
- [Création et remplissage d’un jeu de données dans l’interface utilisateur](../../ingestion/tutorials/ingest-batch-data.md)

## Étapes suivantes {#next-steps}

Une fois que vous avez préparé vos données pour l&#39;apprentissage automatique en temps réel, début en suivant le [Guide d&#39;utilisation du bloc-notes d&#39;apprentissage automatique en temps réel](./rtml-authoring-notebook.md) pour savoir comment créer et télécharger un modèle ONNX dans le magasin de modèles d&#39;apprentissage automatique en temps réel.
