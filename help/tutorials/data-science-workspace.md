---
keywords: Experience Platform;accueil;rubriques populaires;dsw;DSW
solution: Experience Platform
title: Tutoriels Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace utilise l'apprentissage automatique et l'intelligence artificielle pour créer des informations à partir de vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe.
exl-id: 7cfd71b1-584f-4588-bbcd-bc42a08a0bc0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 19%

---

# [!DNL Data Science Workspace] didacticiels

Adobe Experience Platform [!DNL Data Science Workspace] utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour créer des informations à partir de vos données. Intégré dans Adobe Experience Platform, [!DNL Data Science Workspace] vous aide à faire des prédictions à l’aide de vos contenus et de vos ressources de données dans les solutions d’Adobe. Les analystes de données de tout niveau de compétence disposent d’outils sophistiqués et faciles à utiliser qui aident au développement, à la formation et au réglage rapide de recettes d’apprentissage automatique pour vous faire bénéficier de tous les avantages de la technologie IA sans sa complexité.

Pour en savoir plus, commencez par lire la [présentation de Data Science Workspace](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

L&#39;API [!DNL Sensei Machine Learning] fournit un mécanisme permettant aux chercheurs de données d&#39;organiser et de gérer les services d&#39;apprentissage automatique, de l&#39;intégration des algorithmes à l&#39;expérimentation en passant par le déploiement des services.

**Les guides suivants à l’intention des développeurs d’API sont disponibles :**
- [Moteurs](../data-science-workspace/api/engines.md)  - Découvrez comment rechercher votre  [!DNL Docker] registre, créer un moteur, créer un moteur de pipeline de fonctionnalités, récupérer les informations d&#39;un moteur, mettre à jour un moteur et supprimer un moteur.
- [MLInstances (recettes)](../data-science-workspace/api/mlinstances.md)  - Découvrez comment créer une instance MLInstance, récupérer les informations d&#39;une instance MLInstance, mettre à jour une instance MLInstance et supprimer une instance MLInstance.
- [Expériences](../data-science-workspace/api/experiments.md)  - Découvrez comment créer une expérience, récupérer une expérience ou une expérience exécute des informations, mettre à jour une expérience et supprimer une expérience.
- [Modèles](../data-science-workspace/api/models.md)  - Découvrez comment enregistrer votre propre modèle, récupérer les informations d&#39;un modèle, mettre à jour un modèle, supprimer un modèle, créer un nouveau transcodage pour un modèle et récupérer les détails d&#39;un modèle transcodé.
- [MLServices](../data-science-workspace/api/mlservices.md)  - Découvrez comment créer un MLService, récupérer les informations d&#39;un MLService, mettre à jour un MLService et supprimer un MLService.
- [Insights](../data-science-workspace/api/insights.md)  - Découvrez comment récupérer les informations d&#39;un Insight, ajouter un nouveau Model Insight et récupérer une liste de mesures par défaut pour les algorithmes.

Pour en savoir plus et obtenir les valeurs requises pour effectuer des opérations CRUD avec l&#39;API d&#39;apprentissage automatique Sensei, consultez le [guide de prise en main](../data-science-workspace/api/getting-started.md).

## Utilisation des [!DNL JupyterLab] portables

[!DNL JupyterLab] est une interface utilisateur web pour [!DNL Project Jupyter] et est étroitement intégré à Adobe Experience Platform. Il fournit un environnement de développement interactif pour que les chercheurs en données puissent travailler avec [!DNL Jupyter Notebooks], le code et les données. Ce document fournit un aperçu de [!DNL JupyterLab] et de ses fonctionnalités ainsi que des instructions pour effectuer des actions communes.

**Ce guide vous aidera à :**
- Accédez à l&#39;interface [!DNL JupyterLab] et comprenez-la.
- Comprendre les cellules de code et les noyaux disponibles dans [!DNL JupyterLab].
- Comprendre la configuration du GPU et du serveur de mémoire dans [!DNL Python]/R.

Pour en savoir plus, consultez le [Guide de l&#39;utilisateur de JupyterLab](../data-science-workspace/jupyterlab/overview.md).

## Accès aux données dans les portables JupyterLab

Actuellement, JupyterLab dans Data Science Workspace prend en charge les blocs-notes pour [!DNL Python], R, PySpark et Scala. Chaque noyau pris en charge fournit des fonctionnalités intégrées qui vous permettent de lire les données de Platform à partir d’un jeu de données dans un notebook. Cependant, la prise en charge de la pagination des données est limitée aux blocs-notes [!DNL Python] et R. Ce guide se concentre sur l&#39;utilisation des portables JupyterLab pour accéder à vos données.

**Ce guide vous aidera à :**
- Données de plateformes en lecture, écriture et requête à l&#39;aide de portables Python, R, PySpark ou Scala.
- Comprendre les limites de lecture de chaque type de bloc-notes.

Pour en savoir plus, consultez le [Guide du développeur d&#39;accès aux données d&#39;ordinateur portable JupyterLab](../data-science-workspace/jupyterlab/access-notebook-data.md)

## compresser les fichiers source pour la création de recettes [!DNL Docker] ;

Une image [!DNL Docker] vous permet de créer un package d&#39;application avec toutes les parties dont elle a besoin. Cela inclut les bibliothèques et autres dépendances dans un seul package. L&#39;image [!DNL Docker] créée est envoyée à [!DNL Azure Container Registry] à l&#39;aide des informations d&#39;identification qui vous ont été fournies lors du processus de création de la recette.

**Ce didacticiel vous aidera à :**
- Téléchargez les conditions préalables requises pour la création de recettes.
- Comprendre la création de modèles basés sur [!DNL Docker].
- Créez une image [!DNL Docker] pour [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).
- Obtenez une URL de fichier source [!DNL Docker].

Pour en savoir plus, suivez les [fichiers source du package dans un didacticiel de recette](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Importer une recette

>[!NOTE]
>
>Ce didacticiel nécessite que vous disposiez d’une URL de fichier source [!DNL Docker]. Consultez les fichiers source du [package dans un didacticiel de recette](../data-science-workspace/models-recipes/package-source-files-recipe.md) si vous ne disposez pas d’une URL de fichier source [!DNL Docker].

Les didacticiels sur les recettes d&#39;importation fournissent des informations sur la configuration et l&#39;importation d&#39;une recette assemblée. À la fin de ce didacticiel, vous pouvez créer, former et évaluer un modèle dans Adobe Experience Platform [!DNL Data Science Workspace].

**Ce didacticiel vous aidera à :**
- Créez un ensemble de configurations pour une recette.
- Importez une recette basée sur [!DNL Docker] pour [!DNL Python], R, PySpark ou Scala ([!DNL Spark]).

Pour en savoir plus, suivez le didacticiel [UI ](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) de l&#39;importation d&#39;une recette empaquetée ou le [didacticiel d&#39;API](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Formation et évaluation d’un modèle

Dans Adobe Experience Platform [!DNL Data Science Workspace], un modèle d&#39;apprentissage automatique est créé en incorporant une recette existante qui convient à l&#39;intention du modèle. Le modèle est ensuite formé et évalué afin d’optimiser son efficience et son efficacité opérationnelles en affinant ses hyperparamètres associés. Les recettes sont réutilisables, ce qui signifie que plusieurs modèles peuvent être créés et adaptés à des fins spécifiques à l’aide d’une seule recette.

**Ce didacticiel vous aidera à :**
- Créez un modèle.
- Créez une session de formation pour votre modèle.
- Évaluez les exécutions de formation au modèle.

Pour commencer, suivez la formation et l’évaluation d’un modèle [didacticiel d’API](../data-science-workspace/models-recipes/train-evaluate-model-api.md) ou du [didacticiel d’interface utilisateur](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Optimisation d&#39;un modèle à l&#39;aide de la structure Model Insights

Le cadre d&#39;analyse des modèles fournit aux scientifiques des données des outils à Adobe Experience Platform [!DNL Data Science Workspace] pour faire des choix rapides et éclairés en vue de modèles optimaux d&#39;apprentissage automatique basés sur des expériences. Le framework améliorera la vitesse et l’efficacité du processus d’apprentissage automatique et la facilité d’utilisation pour les analystes de données. Pour ce faire, un modèle par défaut est fourni pour chaque type d’algorithme d’apprentissage automatique afin de faciliter le réglage des modèles. Le résultat final permet aux analystes de données et aux analystes de données citoyens de prendre de meilleures décisions d’optimisation des modèles pour leurs clients finaux.

**Ce didacticiel vous aidera à :**
- Configurez le code de recette.
- Définissez des mesures personnalisées.
- Utilisez des mesures d’évaluation prédéfinies et des graphiques de visualisation.

Pour commencer, suivez le didacticiel sur [l&#39;optimisation d&#39;un modèle](../data-science-workspace/models-recipes/optimize-model.md).

## Score d’un modèle

Le score dans Adobe Experience Platform [!DNL Data Science Workspace] peut être obtenu en alimentant les données d&#39;entrée dans un modèle existant. Les résultats de la notation sont ensuite stockés et consultables dans un jeu de données de sortie spécifié sous la forme d’un nouveau lot.

**Ce didacticiel vous aidera à :**
- Création d’une opération de notation.
- Vue de vos résultats de score.

Pour commencer, suivez le score d&#39;un modèle [didacticiel d&#39;API](../data-science-workspace/models-recipes/score-model-api.md) ou le [didacticiel d&#39;interface utilisateur](../data-science-workspace/models-recipes/score-model-ui.md).

## Publication d’un modèle en tant que service

Adobe Experience Platform [!DNL Data Science Workspace] vous permet de publier votre modèle en tant que service, ce qui permet aux utilisateurs de votre organisation IMS de noter des données sans avoir à créer leurs propres modèles. Pour ce faire, vous pouvez utiliser l&#39;interface utilisateur [!DNL Platform] ou l&#39;API [!DNL Sensei Machine Learning].

**Ce didacticiel vous aidera à :**
- Publiez un modèle en tant que service.
- Score des données à l’aide d’un service via la [!DNL Platform] [!UICONTROL Galerie de services].

Pour commencer, suivez le [tutoriel API](../data-science-workspace/models-recipes/publish-model-service-api.md) ou le [tutoriel UI](../data-science-workspace/models-recipes/publish-model-service-ui.md) pour publier un modèle en tant que service.

## Planification de la formation et de la notation pour un modèle

Adobe Experience Platform [!DNL Data Science Workspace] vous permet de configurer des exécutions planifiées de notation et de formation sur un service d’apprentissage automatique. L&#39;automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l&#39;efficacité d&#39;un service dans le temps en respectant les schémas de vos données.

**Ce didacticiel vous aidera à :**
- Configuration d’une notation planifiée
- Configuration d’une formation planifiée

Pour commencer, suivez le [didacticiel sur l&#39;interface utilisateur du modèle ](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Création d’un pipeline de fonctionnalités

>[!NOTE]
>
>Actuellement, les pipelines de fonctionnalités ne sont disponibles que par API.

Adobe Experience Platform vous permet de créer et de créer des pipelines de fonctionnalités personnalisées pour effectuer l&#39;ingénierie de fonctionnalités à l&#39;échelle par le biais de [!DNL Sensei Machine Learning Framework Runtime].

**Ce guide vous aidera à :**
- Mettez en oeuvre les classes de pipeline de fonctionnalités.
- Créez un moteur de pipeline de fonctionnalités à l’aide de l’API.

Pour en savoir plus, consultez le didacticiel de [création d’un pipeline de fonctionnalités](../data-science-workspace/authoring/feature-pipeline.md).

## Créer une application [!DNL Real-Time Machine Learning] (alpha)

Une combinaison de calcul transparent sur le Hub et le [!DNL Edge] réduit considérablement la latence traditionnellement impliquée dans l’activation d’expériences hyper-personnalisées à la fois pertinentes et réactives. Par conséquent, [!DNL Real-time Machine Learning] fournit des inférences avec une latence incroyablement faible pour la prise de décision synchrone. Par exemple, le rendu du contenu d’une page Web personnalisée, l’apparition d’une offre et les remises pour réduire le taux de fréquentation tout en augmentant les conversions sur un site Web de stockage.

**Ce guide vous aidera à :**
- Comprendre l&#39;architecture [!DNL Real-time Machine Learning].
- Comprendre le flux de travaux [!DNL Real-time Machine Learning].
- Comprendre la fonctionnalité actuelle de [!DNL Real-time Machine Learning].
- Fournissez les étapes suivantes pour créer votre propre [!DNL Real-time Machine Learning model].

Pour en savoir plus, consultez la [Présentation de l&#39;apprentissage automatique en temps réel](../data-science-workspace/real-time-machine-learning/home.md).
