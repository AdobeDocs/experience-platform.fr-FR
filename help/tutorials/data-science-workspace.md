---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels sur l’espace de travail Data Science
topic: tutorial
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---


# Didacticiels sur l’espace de travail Data Science

Adobe Experience Platform Data Science Workspace utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour créer des informations à partir de vos données. Intégré dans l’Adobe Experience Platform, Data Science Workspace vous permet de faire des prédictions à l’aide de vos contenus et de vos ressources de données dans les solutions Adobe. Les chercheurs en données de tous les niveaux de compétence disposent d&#39;outils sophistiqués et faciles à utiliser qui permettent le développement rapide, la formation et l&#39;affinement des recettes d&#39;apprentissage automatique - tous les avantages de la technologie de l&#39;IA, sans la complexité.

Pour en savoir plus, lisez tout d’abord l’aperçu [de](../data-science-workspace/home.md)Data Science Workspace.

## API d&#39;apprentissage automatique Sensei

L&#39;API d&#39;apprentissage automatique Sensei fournit un mécanisme permettant aux chercheurs de données d&#39;organiser et de gérer les services d&#39;apprentissage automatique, de l&#39;intégration d&#39;algorithmes à l&#39;expérimentation en passant par le déploiement de services.

**Les guides suivants à l’intention des développeurs d’API sont disponibles :**
- [Moteurs](../data-science-workspace/api/engines.md) - Découvrez comment rechercher votre registre Docker, créer un moteur, créer un moteur de pipeline de fonctionnalités, récupérer les informations d&#39;un moteur, mettre à jour un moteur et supprimer un moteur.
- [MLInstances (recettes)](../data-science-workspace/api/mlinstances.md) - Découvrez comment créer une instance MLInstance, récupérer les informations d&#39;une instance MLInstance, mettre à jour une instance MLInstance et supprimer une instance MLInstance.
- [Expériences](../data-science-workspace/api/experiments.md) - Découvrez comment créer une expérience, récupérer une expérience ou une expérience exécute des informations, mettre à jour une expérience et supprimer une expérience.
- [Modèles](../data-science-workspace/api/models.md) - Découvrez comment enregistrer votre propre modèle, récupérer les informations d&#39;un modèle, mettre à jour un modèle, supprimer un modèle, créer un nouveau transcodage pour un modèle et récupérer les détails d&#39;un modèle transcodé.
- [MLServices](../data-science-workspace/api/mlservices.md) - Découvrez comment créer un MLService, récupérer les informations d&#39;un MLService, mettre à jour un MLService et supprimer un MLService.
- [Insights](../data-science-workspace/api/insights.md) - Découvrez comment récupérer les informations d&#39;un Insight, ajouter un nouveau Model Insight et récupérer une liste de mesures par défaut pour les algorithmes.

Pour en savoir plus et obtenir les valeurs requises pour effectuer des opérations CRUD avec l&#39;API d&#39;apprentissage automatique Sensei, consultez le guide [de](../data-science-workspace/api/getting-started.md)prise en main.

## Utilisation des portables JupyterLab

[!DNL JupyterLab] est une interface utilisateur web pour [!DNL Project Jupyter] et est étroitement intégrée à l’Adobe Experience Platform. Il fournit un environnement de développement interactif pour que les chercheurs en données puissent travailler avec des ordinateurs portables, du code et des données Jupyter. Ce document présente un aperçu de [!DNL JupyterLab] et de ses fonctionnalités, ainsi que des instructions pour effectuer des actions communes.

**Ce guide vous aidera à :**
- Accédez à l&#39; [!DNL JupyterLab] interface et comprenez-la.
- Comprendre les cellules de code et les noyaux disponibles dans [!DNL JupyterLab].
- Comprendre la configuration du GPU et du serveur de mémoire dans Python/R.
- Lecture et requête [!DNL Platform] des données à l’aide de portables.
- Comprenez les limites de données des ordinateurs portables.

Pour en savoir plus, consultez le guide [d&#39;utilisation de](../data-science-workspace/jupyterlab/overview.md)JupyterLab.

## Fichiers source de package pour la création de recettes Docker

Une image Docker vous permet de créer un package d&#39;application avec toutes les pièces dont elle a besoin. Cela inclut les bibliothèques et autres dépendances dans un seul package. L&#39;image Docker construite est envoyée au Registre du Conteneur Azure à l&#39;aide des informations d&#39;identification qui vous ont été fournies pendant le processus de création de la recette.

**Ce didacticiel vous aidera à :**
- Téléchargez les conditions préalables requises pour la création de recettes.
- Comprendre la création de modèles basée sur Docker.
- Créez une image Docker pour Python, R, PySpark ou Scala (Spark).
- Procurez-vous une URL de fichier source Docker.

Pour en savoir plus, suivez les fichiers source du [package dans un didacticiel](../data-science-workspace/models-recipes/package-source-files-recipe.md)de recette.

## Importer une recette

>[!NOTE]
>Ce didacticiel nécessite que vous disposiez d&#39;une URL de fichier source Docker. Consultez les fichiers source du [package dans un didacticiel](../data-science-workspace/models-recipes/package-source-files-recipe.md) de recette si vous n&#39;avez pas d&#39;URL de fichier source Docker.

Les didacticiels sur les recettes d&#39;importation fournissent des informations sur la configuration et l&#39;importation d&#39;une recette assemblée. D&#39;ici la fin de ce didacticiel, vous pouvez créer, former et évaluer un modèle dans l&#39;espace de travail Adobe Experience Platform Data Science.

**Ce didacticiel vous aidera à :**
- Créez un ensemble de configurations pour une recette.
- Importez une recette basée sur un Docker pour Python, R, PySpark ou Scala (Spark).

Pour en savoir plus, suivez le didacticiel [sur l&#39;](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) interface utilisateur de la recette préemballée ou le didacticiel [](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)API.

## Formation et évaluation d’un modèle

Dans Adobe Experience Platform Data Science Workspace, un modèle d&#39;apprentissage automatique est créé en incorporant une recette existante qui convient à l&#39;intention du modèle. Le modèle est ensuite formé et évalué afin d&#39;optimiser son efficacité et son efficacité d&#39;exploitation en affinant ses Hyperparamètres associés. Les recettes sont réutilisables, ce qui signifie que plusieurs modèles peuvent être créés et adaptés à des fins spécifiques avec une seule Recette.

**Ce didacticiel vous aidera à :**
- Créez un modèle.
- Créez une session de formation pour votre modèle.
- Évaluez les exécutions de formation au modèle.

Pour commencer, suivez la formation et l’évaluation d’un didacticiel [d’](../data-science-workspace/models-recipes/train-evaluate-model-api.md) API de modèle ou du didacticiel [](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)IU.

## Optimisation d&#39;un modèle à l&#39;aide de la structure Model Insights

Le cadre d&#39;analyse de modèle fournit aux chercheurs en données des outils dans l&#39;espace de travail des sciences des données d&#39;Adobe Experience Platform pour faire des choix rapides et éclairés pour des modèles d&#39;apprentissage automatique optimaux basés sur des expériences. Le cadre améliorera la vitesse et l&#39;efficacité du processus d&#39;apprentissage automatique et améliorera la facilité d&#39;utilisation pour les chercheurs en données. Pour ce faire, vous fournissez un modèle par défaut pour chaque type d’algorithme d’apprentissage automatique afin de faciliter le réglage des modèles. Le résultat final permet aux spécialistes des données et aux scientifiques des données citoyens de prendre de meilleures décisions d&#39;optimisation des modèles pour leurs clients finaux.

**Ce didacticiel vous aidera à :**
- Configurez le code de recette.
- Définissez des mesures personnalisées.
- Utilisez des mesures d’évaluation prédéfinies et des graphiques de visualisation.

Pour commencer, suivez le didacticiel sur l&#39; [optimisation d&#39;un modèle](../data-science-workspace/models-recipes/optimize-model.md).

## Score d’un modèle

Le score dans l&#39;espace de travail des données d&#39;Adobe Experience Platform peut être obtenu en alimentant les données d&#39;entrée dans un modèle existant. Les résultats de score sont ensuite stockés et visibles dans un jeu de données de sortie spécifié en tant que nouveau lot.

**Ce didacticiel vous aidera à :**
- Créez une nouvelle série de scores.
- Vue de vos résultats de score.

Pour commencer, suivez le didacticiel [sur l’](../data-science-workspace/models-recipes/score-model-api.md) API du modèle ou le didacticiel [](../data-science-workspace/models-recipes/score-model-ui.md)IU.

## Publication d’un modèle en tant que service

Adobe Experience Platform Data Science Workspace vous permet de publier votre modèle en tant que service, ce qui permet aux utilisateurs de votre organisation IMS de noter des données sans avoir à créer leurs propres modèles. Vous pouvez le faire à l’aide de l’interface [!DNL Platform] utilisateur ou de l’API d’apprentissage automatique Sensei.

**Ce didacticiel vous aidera à :**
- Publiez un modèle en tant que service.
- Score des données à l’aide d’un service via la Galerie de [!DNL Platform] services.

Pour commencer, suivez le didacticiel [Publier un modèle en tant que](../data-science-workspace/models-recipes/publish-model-service-api.md) API de service ou le didacticiel [](../data-science-workspace/models-recipes/publish-model-service-ui.md)IU.

## Planification de la formation et de la notation pour un modèle

Adobe Experience Platform Data Science Workspace vous permet de configurer des exécutions planifiées de notation et de formation sur un service d’apprentissage automatique. L&#39;automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l&#39;efficacité d&#39;un service dans le temps en respectant les schémas de vos données.

**Ce didacticiel vous aidera à :**
- Configuration d’un score planifié
- Configuration de la formation planifiée

Pour commencer, suivez le didacticiel [de](../data-science-workspace/models-recipes/schedule-models-ui.md)planification d’un modèle d’interface utilisateur.

## Création d’un pipeline de fonctionnalités

>[!NOTE]
>Actuellement, les pipelines de fonctionnalités ne sont disponibles que par API.

L&#39;Adobe Experience Platform vous permet de créer et de créer des pipelines de fonctions personnalisées pour effectuer l&#39;ingénierie de fonctions à l&#39;échelle via le cadre d&#39;exécution Sensei Machine Learning Framework.

**Ce guide vous aidera à :**
- Mettez en oeuvre les classes de pipeline de fonctionnalités.
- Créez un moteur de pipeline de fonctionnalités à l’aide de l’API.

Pour en savoir plus, consultez le didacticiel consacré à la [création d’un pipeline](../data-science-workspace/authoring/feature-pipeline.md)de fonctionnalités.

## Création d’une application d’apprentissage automatique en temps réel (alpha)

La combinaison d’un calcul transparent sur le Hub et sur le Hub [!DNL Edge] réduit considérablement la latence traditionnellement impliquée dans l’activation d’expériences hyper-personnalisées à la fois pertinentes et réactives. Par conséquent, l&#39;apprentissage automatique en temps réel fournit des inférences avec une latence incroyablement faible pour la prise de décision synchrone. Par exemple, le rendu du contenu d’une page Web personnalisée, l’apparition d’une offre et les remises pour réduire le taux de fréquentation tout en augmentant les conversions sur un site Web de stockage.

**Ce guide vous aidera à :**
- Comprendre l&#39;architecture d&#39;apprentissage automatique en temps réel.
- Comprendre le processus d’apprentissage automatique en temps réel.
- Comprendre la fonctionnalité actuelle de l&#39;apprentissage automatique en temps réel.
- Fournissez les étapes suivantes pour créer votre propre modèle d&#39;apprentissage automatique en temps réel.

Pour en savoir plus, consultez la présentation [de l&#39;apprentissage automatique en temps](../data-science-workspace/real-time-machine-learning/home.md)réel.