---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriels Data Science Workspace
topic: tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 17%

---


# [!DNL Data Science Workspace] didacticiels

Adobe Experience Platform [!DNL Data Science Workspace] uses machine learning and artificial intelligence to create insights from your data. Integrated into Adobe Experience Platform, [!DNL Data Science Workspace] helps you make predictions using your content and data assets across Adobe solutions. Les analystes de données de tout niveau de compétence disposent d’outils sophistiqués et faciles à utiliser qui aident au développement, à la formation et au réglage rapide de recettes d’apprentissage automatique pour vous faire bénéficier de tous les avantages de la technologie IA sans sa complexité.

Pour en savoir plus, commencez par lire la [présentation de Data Science Workspace](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

The [!DNL Sensei Machine Learning] API provides a mechanism for data scientists to organize and manage machine learning services, from algorithm onboarding through experimentation and to service deployment.

**Les guides suivants à l’intention des développeurs d’API sont disponibles :**
- [Moteurs](../data-science-workspace/api/engines.md) - Découvrez comment rechercher votre [!DNL Docker] registre, créer un moteur, créer un moteur de pipeline de fonctionnalités, récupérer les informations d&#39;un moteur, mettre à jour un moteur et supprimer un moteur.
- [MLInstances (recettes)](../data-science-workspace/api/mlinstances.md) - Découvrez comment créer une instance MLInstance, récupérer les informations d&#39;une instance MLInstance, mettre à jour une instance MLInstance et supprimer une instance MLInstance.
- [Expériences](../data-science-workspace/api/experiments.md) - Découvrez comment créer une expérience, récupérer une expérience ou une expérience exécute des informations, mettre à jour une expérience et supprimer une expérience.
- [Modèles](../data-science-workspace/api/models.md) - Découvrez comment enregistrer votre propre modèle, récupérer les informations d&#39;un modèle, mettre à jour un modèle, supprimer un modèle, créer un nouveau transcodage pour un modèle et récupérer les détails d&#39;un modèle transcodé.
- [MLServices](../data-science-workspace/api/mlservices.md) - Découvrez comment créer un MLService, récupérer les informations d&#39;un MLService, mettre à jour un MLService et supprimer un MLService.
- [Insights](../data-science-workspace/api/insights.md) - Découvrez comment récupérer les informations d&#39;un Insight, ajouter un nouveau Model Insight et récupérer une liste de mesures par défaut pour les algorithmes.

Pour en savoir plus et obtenir les valeurs requises pour effectuer des opérations CRUD avec l&#39;API d&#39;apprentissage automatique Sensei, consultez le guide [de](../data-science-workspace/api/getting-started.md)prise en main.

## How to use [!DNL JupyterLab] Notebooks

[!DNL JupyterLab] est une interface utilisateur web pour [!DNL Project Jupyter] et est étroitement intégré à Adobe Experience Platform. It provides an interactive development environment for data scientists to work with [!DNL Jupyter notebooks], code, and data. This document provides an overview of [!DNL JupyterLab] and its features as well as instructions to perform common actions.

**Ce guide vous aidera à :**
- Accédez à l&#39; [!DNL JupyterLab] interface et comprenez-la.
- Comprendre les cellules de code et les noyaux disponibles dans [!DNL JupyterLab].
- Comprendre la configuration du GPU et du serveur de mémoire dans [!DNL Python]/R.
- Lecture et requête [!DNL Platform] des données à l’aide de portables.
- Comprenez les limites de données des ordinateurs portables.

Pour en savoir plus, consultez le guide [d&#39;utilisation de](../data-science-workspace/jupyterlab/overview.md)JupyterLab.

## compresser les fichiers source pour la création de [!DNL Docker] recettes ;

Une [!DNL Docker] image vous permet de créer un package d’application avec toutes les parties nécessaires. Cela inclut les bibliothèques et autres dépendances dans un seul package. L&#39;image générée est transmise à l&#39; [!DNL Docker] [!DNL Azure Container Registry] utilisateur à l&#39;aide des informations d&#39;identification fournies lors du processus de création de la recette.

**Ce didacticiel vous aidera à :**
- Téléchargez les conditions préalables requises pour la création de recettes.
- Comprendre la création de modèles [!DNL Docker] basés sur le modèle.
- Créez une [!DNL Docker] image pour [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).
- Obtenez une URL de fichier [!DNL Docker] source.

Pour en savoir plus, suivez les fichiers source du [package dans un didacticiel](../data-science-workspace/models-recipes/package-source-files-recipe.md)de recette.

## Importer une recette

>[!NOTE]
>
>Ce didacticiel nécessite que vous disposiez d’une URL de fichier [!DNL Docker] source. Consultez les fichiers source du [package dans un didacticiel](../data-science-workspace/models-recipes/package-source-files-recipe.md) de recette si vous ne disposez pas d’une URL de fichier [!DNL Docker] source.

Les didacticiels sur les recettes d&#39;importation fournissent des informations sur la configuration et l&#39;importation d&#39;une recette assemblée. By the end of this tutorial, you can create, train, and evaluate a Model in Adobe Experience Platform [!DNL Data Science Workspace].

**Ce didacticiel vous aidera à :**
- Créez un ensemble de configurations pour une recette.
- Importez une recette [!DNL Docker] basée sur [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).

Pour en savoir plus, suivez le didacticiel [sur l&#39;](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) interface utilisateur de la recette préemballée ou le didacticiel [](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)API.

## Formation et évaluation d’un modèle

In Adobe Experience Platform [!DNL Data Science Workspace], a machine learning Model is created by incorporating an existing Recipe that is appropriate for the Model&#39;s intent. Le modèle est ensuite formé et évalué afin d’optimiser son efficience et son efficacité opérationnelles en affinant ses hyperparamètres associés. Les recettes sont réutilisables, ce qui signifie que plusieurs modèles peuvent être créés et adaptés à des fins spécifiques à l’aide d’une seule recette.

**Ce didacticiel vous aidera à :**
- Créez un modèle.
- Créez une session de formation pour votre modèle.
- Évaluez les exécutions de formation au modèle.

Pour commencer, suivez la formation et l’évaluation d’un didacticiel [d’](../data-science-workspace/models-recipes/train-evaluate-model-api.md) API de modèle ou du didacticiel [](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)IU.

## Optimisation d&#39;un modèle à l&#39;aide de la structure Model Insights

The Model Insights Framework provides the data scientist with tools in Adobe Experience Platform [!DNL Data Science Workspace] to make quick and informed choices for optimal machine learning models based on experiments. Le framework améliorera la vitesse et l’efficacité du processus d’apprentissage automatique et la facilité d’utilisation pour les analystes de données. Pour ce faire, un modèle par défaut est fourni pour chaque type d’algorithme d’apprentissage automatique afin de faciliter le réglage des modèles. Le résultat final permet aux analystes de données et aux analystes de données citoyens de prendre de meilleures décisions d’optimisation des modèles pour leurs clients finaux.

**Ce didacticiel vous aidera à :**
- Configurez le code de recette.
- Définissez des mesures personnalisées.
- Utilisez des mesures d’évaluation prédéfinies et des graphiques de visualisation.

Pour commencer, suivez le didacticiel sur l&#39; [optimisation d&#39;un modèle](../data-science-workspace/models-recipes/optimize-model.md).

## Score d’un modèle

Scoring in Adobe Experience Platform [!DNL Data Science Workspace] can be achieved by feeding input data into an existing trained Model. Les résultats de la notation sont ensuite stockés et consultables dans un jeu de données de sortie spécifié sous la forme d’un nouveau lot.

**Ce didacticiel vous aidera à :**
- Création d’une opération de notation.
- Vue de vos résultats de score.

To get started, follow the score a model [API tutorial](../data-science-workspace/models-recipes/score-model-api.md) or the [UI tutorial](../data-science-workspace/models-recipes/score-model-ui.md).

## Publication d’un modèle en tant que service

Adobe Experience Platform [!DNL Data Science Workspace] allows you to publish your Model as a service, enabling users within your IMS Organization to score data without the need for creating their own Models. This can be done using the [!DNL Platform] user interface or the [!DNL Sensei Machine Learning] API.

**Ce didacticiel vous aidera à :**
- Publiez un modèle en tant que service.
- Score des données à l’aide d’un service via la Galerie [!DNL Platform] de services.

Pour commencer, suivez le [tutoriel API](../data-science-workspace/models-recipes/publish-model-service-api.md) ou le [tutoriel UI](../data-science-workspace/models-recipes/publish-model-service-ui.md) pour publier un modèle en tant que service.

## Planification de la formation et de la notation pour un modèle

Adobe Experience Platform [!DNL Data Science Workspace] allows you to set up scheduled scoring and training runs on a machine learning service. L&#39;automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l&#39;efficacité d&#39;un service dans le temps en respectant les schémas de vos données.

**Ce didacticiel vous aidera à :**
- Configuration d’une notation planifiée
- Configuration d’une formation planifiée

Pour commencer, suivez le didacticiel [de](../data-science-workspace/models-recipes/schedule-models-ui.md)planification d’un modèle d’interface utilisateur.

## Création d’un pipeline de fonctionnalités

>[!NOTE]
>
>Actuellement, les pipelines de fonctionnalités ne sont disponibles que par API.

Adobe Experience Platform vous permet de créer et de créer des pipelines de fonctionnalités personnalisées pour effectuer l&#39;ingénierie de fonctionnalités à l&#39;échelle du [!DNL Sensei Machine Learning Framework Runtime].

**Ce guide vous aidera à :**
- Mettez en oeuvre les classes de pipeline de fonctionnalités.
- Créez un moteur de pipeline de fonctionnalités à l’aide de l’API.

Pour en savoir plus, consultez le didacticiel consacré à la [création d’un pipeline](../data-science-workspace/authoring/feature-pipeline.md)de fonctionnalités.

## Création d’une [!DNL Real-Time Machine Learning] application (alpha)

La combinaison d’un calcul transparent sur le Hub et sur le Hub [!DNL Edge] réduit considérablement la latence traditionnellement impliquée dans l’activation d’expériences hyper-personnalisées à la fois pertinentes et réactives. Par conséquent, [!DNL Real-time Machine Learning] fournit des inférences avec une latence incroyablement faible pour la prise de décision synchrone. Par exemple, le rendu du contenu d’une page Web personnalisée, l’apparition d’une offre et les remises pour réduire le taux de fréquentation tout en augmentant les conversions sur un site Web de stockage.

**Ce guide vous aidera à :**
- Comprendre l&#39; [!DNL Real-time Machine Learning] architecture.
- Comprendre le [!DNL Real-time Machine Learning] processus.
- Comprendre la fonctionnalité actuelle pour [!DNL Real-time Machine Learning].
- Fournissez les étapes suivantes pour créer les vôtres [!DNL Real-time Machine Learning model].

Pour en savoir plus, consultez la présentation [de l&#39;apprentissage automatique en temps](../data-science-workspace/real-time-machine-learning/home.md)réel.