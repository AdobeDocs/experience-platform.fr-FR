---
keywords: Experience Platform;guide de développement;Espace de travail de science des données;rubriques les plus consultées;machine learning en temps réel;
solution: Experience Platform
title: Prise en main du machine learning en temps réel
description: Le document suivant décrit les étapes requises pour créer un modèle de machine learning en temps réel dans Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 83%

---

# Prise en main du machine learning en temps réel (Alpha)

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

>[!IMPORTANT]
>
>Le machine learning en temps réel n’est pas encore disponible pour tous les utilisateurs et utilisatrices. Cette fonctionnalité est en version alpha et est encore en cours de test. Ce document est sujet à modification.

Pour utiliser le machine learning en temps réel, vous devez avoir accès à une organisation dotée d’Adobe Experience Platform et de [!DNL Data Science Workspace]. De plus, vous devez disposer d’un jeu de données complet à utiliser pour la formation et la notation.

Les guides sur le machine learning en temps réel nécessitent une compréhension pratique de Python 3, des [Notebooks Jupyter](../jupyterlab/overview.md), de la science des données et du machine learning.

**Termes clés :**

- **DSL :** langue spécifique au domaine.
- **Edge :** le service de notation du machine learning en temps réel peut être exécuté sur des grappes Edge plus proches de vos activations et applications.
- **Hub :** la version alpha actuelle exécute le service de notation du machine learning en temps réel sur le hub Adobe Experience Platform pendant que l’Edge Network est en cours de développement.
- **Nœud :** un nœud est l’unité fondamentale à partir de laquelle des graphiques sont formés. Chaque nœud effectue une tâche spécifique et ces nœuds peuvent être liés ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche effectuée par un nœud représente une opération sur les données d’entrée, telle qu’une transformation des données ou un schéma, ou une inférence de machine learning. Le nœud sort la valeur transformée ou déduite pour le ou les nœuds suivants.

## Jeux de données dans Adobe Experience Platform

Pour commencer à utiliser le machine learning en temps réel, vous devez avoir accès à un jeu de données. Vous avez la possibilité d’utiliser un jeu de données externe et de le charger dans votre environnement [!DNL JupyterLab] ou de créer un jeu de données dans Experience Platform si vous ne l’avez pas déjà fait.

>[!NOTE]
>
>Si vous possédez déjà un jeu de données à utiliser, vous pouvez passer aux [étapes suivantes](#next-steps).

### Utiliser un jeu de données externe

Pour en savoir plus sur l’utilisation d’un jeu de données externe, tel que le chargement de données dans votre environnement [!DNL JupyterLab], consultez le tutoriel sur l’[analyse de vos données à l’aide de notebooks](../jupyterlab/analyze-your-data.md#external-data).

### Créer un nouveau jeu de données

Pour créer un jeu de données à utiliser dans le machine learning en temps réel, vous avez besoin d’un schéma de données pour votre jeu de données. Ensuite, vous devez ingérer des données à l’aide du schéma que vous avez créé. Utilisez les tutoriels suivants pour créer et renseigner un jeu de données pour [!DNL Experience Platform] :

- [Créer et renseigner un jeu de données dans l’API](../../catalog/datasets/create.md)
- [Créer et renseigner un jeu de données dans l’interface utilisateur](../../ingestion/tutorials/ingest-batch-data.md)

## Étapes suivantes {#next-steps}

Une fois que vous avez préparé vos données pour le machine learning en temps réel, commencez par suivre le [guide d’utilisation du notebook de machine learning en temps réel](./rtml-authoring-notebook.md) pour savoir comment créer et charger un modèle ONNX dans la boutique de modèles de machine learning en temps réel.
