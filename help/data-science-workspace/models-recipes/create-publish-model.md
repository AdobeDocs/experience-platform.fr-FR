---
keywords: Experience Platform;modèle d’apprentissage automatique;Data Science Workspace;rubriques les plus consultées;créer et publier un modèle
solution: Experience Platform
title: Création et publication d’un modèle d’apprentissage automatique
type: Tutorial
description: Le guide suivant décrit les étapes requises pour créer et publier un modèle d’apprentissage automatique.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 12%

---


# Création et publication d’un modèle d’apprentissage automatique

Le guide suivant décrit les étapes requises pour créer et publier un modèle d’apprentissage automatique. Chaque section contient une description de ce que vous allez faire et un lien vers l’interface utilisateur et la documentation de l’API pour réaliser l’étape décrite.

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :

- Accès à [!DNL Adobe Experience Platform]. Si vous n’avez pas accès à une organisation IMS dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.

- Tous les tutoriels Data Science Workspace utilisent le modèle de propension Luma. Pour suivre cette procédure, vous devez avoir créé la variable [Schémas et jeux de données de modèle de propension Luma](./create-luma-data.md).

### Exploration des données et compréhension des schémas

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Jeux de données]** pour répertorier tous les jeux de données existants et sélectionner le jeu de données que vous souhaitez explorer. Dans ce cas, vous devez sélectionner la variable **Données web Luma** jeu de données.

![sélectionnez Jeu de données web Luma](../images/models-recipes/model-walkthrough/luma-dataset.png)

La page d’activité du jeu de données s’ouvre, répertoriant les informations relatives à votre jeu de données. Vous pouvez sélectionner **[!UICONTROL Aperçu du jeu de données]** près du coin supérieur droit pour examiner des exemples d’enregistrements. Vous pouvez également afficher le schéma du jeu de données sélectionné.

![prévisualisation des données web Luma](../images/models-recipes/model-walkthrough/preview-dataset.png)

Sélectionnez le lien du schéma dans le rail droit. Une fenêtre contextuelle s’affiche, en sélectionnant le lien sous **[!UICONTROL nom du schéma]** ouvre le schéma dans un nouvel onglet.

![aperçu du schéma de données web luma](../images/models-recipes/model-walkthrough/preview-schema.png)

Vous pouvez explorer plus en détail les données à l’aide du notebook d’analyse des données exploratoires (EDA) fourni. Ce notebook peut être utilisé pour aider à comprendre les modèles dans les données Luma, vérifier l’intégrité des données et résumer les données pertinentes pour le modèle de propension prédictive. Pour en savoir plus sur l’analyse des données exploratoires, rendez-vous sur la page [Documentation EDA](../jupyterlab/eda-notebook.md).

## Création de la recette de propension Luma {#author-your-model}

Un composant principal de la variable [!DNL Data Science Workspace] le cycle de vie implique la création de recettes et de modèles. Le modèle de propension de Luma est conçu pour générer une prédiction indiquant si les clients ont une forte propension à acheter un produit auprès de Luma.

Pour créer le modèle de propension Luma, le modèle de créateur de recettes est utilisé. Les recettes sont la base d’un modèle, car elles contiennent des algorithmes d’apprentissage automatique et une logique conçue pour résoudre des problèmes spécifiques. Plus important encore, les recettes vous permettent de démocratiser l’apprentissage automatique au sein de votre organisation, en permettant à d’autres utilisateurs d’accéder à un modèle pour des cas d’utilisation variés sans devoir coder.

Suivez la [créer un modèle à l’aide des notebooks JupyterLab ;](../jupyterlab/create-a-model.md) tutoriel pour créer la recette du modèle de propension Luma utilisée dans les tutoriels suivants.

## Importer et empaqueter une recette à partir de sources externes (*facultatif*)

Si vous souhaitez importer et empaqueter une recette à utiliser dans Data Science Workspace, vous devez regrouper vos fichiers source dans un fichier d’archive. Suivez la [regrouper les fichiers source dans une recette](./package-source-files-recipe.md) tutoriel . Ce tutoriel vous explique comment regrouper des fichiers source dans une recette, étape prérequise pour importer une recette dans Data Science Workspace. Une fois le tutoriel terminé, vous recevez une image Docker dans un Azure Container Registry, ainsi que l’URL d’image correspondante, c’est-à-dire un fichier d’archive.

Ce fichier d’archive peut être utilisé pour créer une recette dans Data Science Workspace en suivant le workflow d’importation de recette à l’aide de la fonction [Workflow de l’interface utilisateur](./import-packaged-recipe-ui.md) ou le [Workflow d’API](./import-packaged-recipe-api.md).

## Formation et évaluation d’un modèle {#train-and-evaluate-your-model}

Maintenant que vos données sont préparées et qu’une recette est prête, vous avez la possibilité de créer, de former et d’évaluer davantage votre modèle d’apprentissage automatique. Lors de l’utilisation du créateur de recettes, vous devez avoir déjà formé, noté et évalué votre modèle avant de le transformer en recette.

L’interface utilisateur et l’API de Data Science Workspace vous permettent de publier votre recette en tant que modèle. En outre, vous pouvez affiner davantage certains aspects spécifiques de votre modèle, tels que l’ajout, la suppression et la modification d’hyperparamètres.

### Création d’un modèle

Pour en savoir plus sur la création d’un modèle à l’aide de l’interface utilisateur, consultez la formation et l’évaluation d’un modèle dans Data Science Workspace. [Tutoriel sur l’interface utilisateur](./train-evaluate-model-ui.md) ou [Tutoriel sur l’API](./train-evaluate-model-api.md). Ce tutoriel fournit un exemple de création, de formation et de mise à jour d’hyperparamètres pour affiner votre modèle.

>[!NOTE]
>
> Les hyperparamètres ne peuvent pas être appris. Par conséquent, ils doivent être attribués avant les sessions d’entraînement. Le réglage d’hyperparamètres peut modifier la précision de votre modèle formé. L’optimisation d’un modèle étant un processus itératif, plusieurs opérations de formation peuvent être nécessaires avant qu’une évaluation satisfaisante ne soit réalisée.

## Notation d’un modèle {#score-a-model}

L’étape suivante de la création et de la publication d’un modèle consiste à rendre opérationnel votre modèle afin de recueillir et d’exploiter les insights du lac de données et de Real-Time Customer Profile.

La notation dans Data Science Workspace peut être réalisée en alimentant un modèle formé existant avec des données d’entrée. Les résultats de la notation sont ensuite stockés et consultables dans un jeu de données de sortie spécifié sous la forme d’un nouveau lot.

Pour savoir comment noter votre modèle, consultez la note d’un modèle. [Tutoriel sur l’interface utilisateur](./score-model-ui.md) ou [Tutoriel sur l’API](./score-model-api.md).

## Publication d’un modèle noté en tant que service

Data Science Workspace vous permet de publier votre modèle formé en tant que service. Cela permet aux utilisateurs de votre organisation IMS de noter des données sans avoir à créer leurs propres modèles.

Pour savoir comment publier un modèle en tant que service, rendez-vous sur la page [Tutoriel sur l’interface utilisateur](./publish-model-service-ui.md) ou [Tutoriel sur l’API](./publish-model-service-api.md).

### Planification de la formation automatisée d’un service

Une fois que vous avez publié un modèle en tant que service, vous pouvez configurer des exécutions de notation et de formation planifiées pour votre service d’apprentissage automatique. L’automatisation du processus de formation et de notation peut contribuer à maintenir et à améliorer l’efficacité d’un service tout au long du temps en suivant les schémas de vos données. Visitez le [planification d’un modèle dans l’interface utilisateur de Data Science Workspace](./schedule-models-ui.md) tutoriel .

>[!NOTE]
>
> Vous pouvez uniquement planifier un modèle pour la formation et la notation automatisées à partir de l’interface utilisateur.

## Étapes suivantes {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] fournit les outils et les ressources nécessaires pour créer, évaluer et utiliser des modèles d’apprentissage automatique afin de générer des prévisions et des insights sur les données. Lorsque des insights d’apprentissage automatique sont ingérés dans une [!DNL Profile]Jeu de données compatible, ces mêmes données sont également ingérées en tant que [!DNL Profile] enregistrements pouvant ensuite être segmentés à l’aide de [!DNL Adobe Experience Platform Segmentation Service].

À mesure que les données de profil et de série temporelle sont ingérées, Real-Time Customer Profile décide automatiquement d’inclure ou d’exclure ces données des segments par le biais d’un processus continu appelé segmentation par flux, avant de les fusionner avec les données existantes et de mettre à jour la vue d’union. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients de meilleures expériences personnalisées lorsqu’ils interagissent avec votre marque.

Consultez le tutoriel pour [enrichissement de Real-time Customer Profile avec des insights d’apprentissage automatique](./enrich-profile.md) pour en savoir plus sur l’utilisation des insights d’apprentissage automatique.
