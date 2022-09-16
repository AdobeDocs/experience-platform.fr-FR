---
keywords: Experience Platform;guide de développement;Data Science Workspace;rubriques les plus consultées;apprentissage automatique en temps réel ;
solution: Experience Platform
title: Prise en main de l’apprentissage automatique en temps réel
topic-legacy: Getting started
description: Le document suivant décrit les étapes requises pour créer un modèle d’apprentissage automatique en temps réel dans Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Prise en main de l’apprentissage automatique en temps réel (Alpha)

>[!IMPORTANT]
>
>L’apprentissage automatique en temps réel n’est pas encore disponible pour tous les utilisateurs. Cette fonctionnalité est en version alpha et est encore en cours de test. Ce document peut faire l’objet de modifications.

Pour utiliser l’apprentissage automatique en temps réel, vous devez avoir accès à une organisation configurée avec Adobe Experience Platform et [!DNL Data Science Workspace]. De plus, vous devez disposer d’un jeu de données complet à utiliser dans la formation et la notation.

Les guides de l’apprentissage automatique en temps réel nécessitent une compréhension pratique de Python 3, [Notebooks Jupyter](../jupyterlab/overview.md), la science des données et l’apprentissage automatique.

**Termes clés:**

- **DSL :** Langue spécifique au domaine.
- **Edge :** Le service de notation d’apprentissage automatique en temps réel peut être exécuté sur des grappes Edge plus proches de vos activations et applications.
- **Hub :** L’alpha actuel exécute le service de notation de l’apprentissage automatique en temps réel sur Adobe Experience Platform Hub pendant que le réseau Experience Edge est en cours de développement.
- **Noeud :** Un noeud est l’unité fondamentale de laquelle des graphiques sont formés. Chaque noeud effectue une tâche spécifique et peut être lié ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche effectuée par un noeud représente une opération sur les données d’entrée, telle qu’une transformation des données ou un schéma, ou une inférence d’apprentissage automatique. Le noeud sort la valeur transformée ou déduite au(x) noeud(s) suivant(s).

## Jeux de données dans Adobe Experience Platform

Pour commencer à utiliser l’apprentissage automatique en temps réel, vous devez avoir accès à un jeu de données. Vous avez la possibilité d’utiliser un jeu de données externe et de le charger dans votre [!DNL JupyterLab] ou créez un jeu de données dans Platform si vous ne l’avez pas déjà fait.

>[!NOTE]
>
>Si vous souhaitez déjà utiliser un jeu de données, vous pouvez passer à [Étapes suivantes](#next-steps).

### Utilisation d’un jeu de données externe

Pour en savoir plus sur l’utilisation d’un jeu de données externe, tel que le chargement de données dans votre [!DNL JupyterLab] environnement, consultez le tutoriel sur [analyse de vos données à l’aide de notebooks](../jupyterlab/analyze-your-data.md#external-data).

### Création d’un nouveau jeu de données

Pour créer un jeu de données à utiliser dans l’apprentissage automatique en temps réel, vous avez besoin d’un schéma de données pour votre jeu de données. Ensuite, vous devez ingérer des données à l’aide du schéma que vous avez créé. Utilisez les tutoriels suivants pour créer et renseigner un jeu de données pour [!DNL Platform]:

- [Création et remplissage d’un jeu de données dans l’API](../../catalog/datasets/create.md)
- [Création et remplissage d’un jeu de données dans l’interface utilisateur](../../ingestion/tutorials/ingest-batch-data.md)

## Étapes suivantes {#next-steps}

Une fois que vous avez préparé vos données pour l’apprentissage automatique en temps réel, commencez par suivre la [Guide d’utilisation du notebook d’apprentissage automatique en temps réel](./rtml-authoring-notebook.md) pour savoir comment créer et charger un modèle ONNX dans la boutique de modèles d’apprentissage automatique en temps réel.
