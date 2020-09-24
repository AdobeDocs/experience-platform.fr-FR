---
keywords: Experience Platform;machine learning model;Data Science Workspace;popular topics;create and publish a model
solution: Experience Platform
title: Guide pas-à-pas de création et de publication d’un modèle d’apprentissage automatique
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace vous donne les moyens d’atteindre votre objectif à l’aide de la recette des recommandations de produits prédéfinie. Suivez ce tutoriel pour découvrir comment accéder à vos données de vente au détail et les comprendre, créer et optimiser un modèle d’apprentissage automatique et générer des insights dans Data Science Workspace.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 83%

---


# Guide pas-à-pas de création et de publication d’un modèle d’apprentissage automatique

![](../images/models-recipes/model-walkthrough/objective.png)

Imaginons que vous possédez un site web de vente en ligne. Lorsque vos clients achètent sur votre site web de vente en ligne, vous souhaitez leur présenter des recommandations de produits personnalisées afin d’exposer une variété d’autres produits proposés par votre entreprise. Au cours de l’existence de votre site web, vous avez continuellement rassemblé des données clients et souhaitez utiliser ces données d’une manière ou d’une autre pour générer des recommandations de produits personnalisées.

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] fournit les moyens d&#39;atteindre votre objectif à l&#39;aide de la Recette [](../pre-built-recipes/product-recommendations.md)du produit prédéfinie Recommendations. Suivez ce tutoriel pour découvrir comment accéder à vos données de vente au détail et les comprendre, créer et optimiser un modèle d’apprentissage automatique et générer des insights dans [!DNL Data Science Workspace].

This tutorial reflects the workflow of [!DNL Data Science Workspace], and covers the following steps for creating a machine learning Model:

1. [Préparation de vos données](#prepare-your-data)
2. [Création de votre modèle](#author-your-model)
3. [Formation et évaluation de votre modèle](#train-and-evaluate-your-model)
4. [Exploitation de votre modèle](#operationalize-your-model)

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :

* Accès à [!DNL Adobe Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.

* Ressources d’activation. Contactez le représentant de votre compte pour que les éléments suivants soient mis en service.
   * Recette des recommandations
   * Jeu de données d’entrée des recommandations
   * Schéma d’entrée des recommandations
   * Jeu de données de sortie des recommandations
   * Schéma de sortie des recommandations
   * Valeurs de publication du jeu de données favori
   * Schéma du jeu de données favori

* Download the three required [!DNL Jupyter Notebook] files from the [Adobe public [!DNL Git] repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs), these will be used to demonstrate the [!DNL JupyterLab] workflow in [!DNL Data Science Workspace].

* Une connaissance concrète des concepts clés suivants employés dans ce tutoriel :
   * [[ !Modèle de données d’expérience DNL]](../../xdm/home.md): Effort de normalisation mené par l’Adobe pour définir des schémas standard tels que [!DNL Profile] et ExperienceEvent, pour la gestion de l’expérience client.
   * Jeux de données : construction de stockage et de gestion pour les données réelles. Instance instanciée physique d’un [schéma XDM](../../xdm/schema/field-dictionary.md).
   * Lots : les jeux de données sont constitués de lots. Un lot est un ensemble de données collectées sur une période donnée et traitées ensemble comme une seule unité.
   * [!DNL JupyterLab]: [[ !DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) est une interface web open-source pour Project [!DNL Jupyter] et est étroitement intégrée dans [!DNL Experience Platform].

## Préparation de vos données {#prepare-your-data}

Pour créer un modèle d’apprentissage automatique qui recommande des produits personnalisés à vos clients, vous devez analyser les achats précédents de clients sur votre site web. This section explores how this data is ingested into [!DNL Platform] through [!DNL Adobe Analytics], and how that data is transformed into a Feature dataset to be used by your machine learning Model.

### Exploration des données et compréhension des schémas

1. Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com/) et cliquez sur **[!UICONTROL Jeux de données]** pour faire la liste de tous les jeux de données existants et sélectionnez le jeu de données à explorer. In this case, the [!DNL Analytics] dataset **Golden Data Set postValues**.
   ![](../images/models-recipes/model-walkthrough/datasets_110.png)
2. Cliquez sur **[!UICONTROL Prévisualiser le jeu de données]** près du coin supérieur droit pour examiner les enregistrements d’exemples, puis cliquez sur **[!UICONTROL Fermer]**.
   ![](../images/models-recipes/model-walkthrough/golden_data_set_110.png)
3. Cliquez sur le lien sous Schéma dans le rail de droite pour afficher le schéma pour le jeu de données, puis revenez à la page des détails du jeu de données.
   ![](../images/models-recipes/model-walkthrough/golden_schema_110.png)

Les autres jeux de données ont été préremplis avec des lots à des fins d’aperçu. Vous pouvez afficher ces jeux de données en répétant les étapes ci-dessus.

| Nom du jeu de données | Schéma | Description |
| ----- | ----- | ----- |
| Valeurs de publication du jeu de données favori | Schéma du jeu de données favori | [!DNL Analytics]Données source de votre site web |
| Jeu de données d’entrée des recommandations | Schéma d’entrée des recommandations | The [!DNL Analytics] data is transformed into a training dataset using a feature pipeline. Ces données sont utilisées pour former le modèle d’apprentissage automatique de recommandations de produits. `itemid` et `userid` correspondent à un produit acheté par ce client. |
| Jeu de données de sortie des recommandations | Schéma de sortie des recommandations | Le jeu de données pour lequel les résultats de notation sont stockés contient la liste des produits recommandés pour chaque client. |

## Création de votre modèle {#author-your-model}

The second component of the [!DNL Data Science Workspace] lifecycle involves authoring Recipes and Models. La recette des recommandations de produits est conçue pour générer des recommandations de produits à grande échelle en utilisant les données d’achats antérieurs et l’apprentissage automatique.

Les recettes sont la base d’un modèle puisqu’elles contiennent des algorithmes d’apprentissage automatique et une logique conçue pour résoudre des problèmes spécifiques. Plus important encore, les recettes vous permettent de démocratiser l’apprentissage automatique au sein de votre organisation, en permettant à d’autres utilisateurs d’accéder à un modèle pour des cas d’utilisation variés sans devoir coder.

### Exploration de la recette des recommandations de produits

1. In [!DNL Adobe Experience Platform], navigate to **[!UICONTROL Models]** from the left navigation column, then click **[!UICONTROL Recipes]** at the top to view a list of available Recipes for your organization.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. Recherchez et ouvrez la **[!UICONTROL recette de recommandations]** fournie en cliquant sur son nom.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. Dans le rail de droite, cliquez sur **[!UICONTROL Schéma d’entrée des recommandations]** pour afficher le schéma qui alimente la recette. Les champs de schéma **[!UICONTROL itemId]** et **[!UICONTROL userId]** correspondent à un produit acheté (**[!UICONTROL interactionType]**) par ce client à un moment spécifique (**[!UICONTROL horodatage]**). Suivez les mêmes étapes pour consulter le **[!UICONTROL Schéma de sortie des recommandations]**.
   ![](../images/models-recipes/model-walkthrough/preview_schemas.png)

Vous avez maintenant examiné les schémas d’entrée et de sortie requis par la recette des recommandations de produits. Vous pouvez maintenant passer à la section suivante pour savoir comment créer, entraîner et évaluer un modèle de recommandations de produits.

## Formation et évaluation de votre modèle {#train-and-evaluate-your-model}

Maintenant que vos données sont préparées et que la recette est prête à être utilisée, vous pouvez créer, entraîner et évaluer votre modèle d’apprentissage automatique.

### Création d’un modèle

Un modèle est une instance de recette qui permet l’entraînement et l’évaluation de données à grande échelle.

1. In [!DNL Adobe Experience Platform], navigate to **[!UICONTROL Models]** from the left navigation column, then click **[!UICONTROL Recipes]** at the top of the page to display a list of all available Recipes for your organization..
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. Recherchez et ouvrez la **[!UICONTROL recette de recommandations]** fournie en cliquant sur son nom, en entrant sur la page de présentation de la recette. Cliquez sur **[!UICONTROL Créer un modèle]**, soit à partir du centre (s’il n’existe aucun modèle), soit en haut à droite de la page de présentation de la recette.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. Une liste de jeux de données d’entrée disponibles pour l’entraînement s’affiche. Sélectionnez **[!UICONTROL Jeu de données d’entrée des recommandations]** et cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/model-walkthrough/select_dataset.png)
4. Donnez un nom au modèle, par exemple « Modèle de recommandations de produits ». Les configurations disponibles pour le modèle sont répertoriées, contenant les paramètres des comportements de formation et de notation par défaut du modèle. Aucune modification n’est nécessaire, car ces configurations sont propres à votre organisation. Vérifiez les configurations et cliquez sur **[!UICONTROL Terminer]**.
   ![](../images/models-recipes/model-walkthrough/configure_model.png)
5. Le modèle a maintenant été créé et la page de *présentation* du modèle s’affiche dans une nouvelle session d’entraînement. Une session d’entraînement est générée par défaut lors de la création d’un modèle.
   ![](../images/models-recipes/model-walkthrough/model_post_creation.png)

Vous pouvez choisir d’attendre la fin de la session d’entraînement ou continuer à créer une session d’entraînement dans la section suivante.

### Entraînement du modèle à l’aide d’hyperparamètres personnalisés

1. Sur la page de *présentation du modèle*, cliquez sur **[!UICONTROL Entraîner]** près du coin supérieur droit pour créer une session d’entraînement. Sélectionnez le même jeu de données d’entrée que celui utilisé lors de la création du modèle, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/model-walkthrough/training_select_dataset.png)
2. La page de *configuration* s’affiche. Vous pouvez y configurer ici la valeur **[!UICONTROL num_recommendations]** de la session d’entraînement, également connue sous le nom d’hyperparamètre. Un modèle entraîné et optimisé utilisera les hyperparamètres les plus performants en fonction des résultats de la session d’entraînement.

   Les hyperparamètres ne peuvent pas être appris. Par conséquent, ils doivent être attribués avant les sessions d’entraînement. L’ajustement d’hyperparamètres peut modifier la précision du modèle entraîné. L’optimisation d’un modèle étant un processus itératif, il peut être nécessaire de procéder à plusieurs sessions d’entraînement avant d’effectuer une évaluation satisfaisante.

   >[!TIP]
   >
   >Définissez **[!UICONTROL num_recommendations]** sur 10.

   ![](../images/models-recipes/model-walkthrough/configure_hyperparameter.png)
3. Un point de données supplémentaire apparaîtra sur le graphique d’évaluation du modèle une fois la nouvelle session d’entraînement terminée, ce qui peut prendre plusieurs minutes.
   ![](../images/models-recipes/model-walkthrough/post_training_run.png)

### Évaluation du modèle

Chaque fois qu’une session d’entraînement se termine, vous pouvez afficher les mesures d’évaluation qui en résultent pour déterminer l’efficacité du modèle.

1. Vérifiez les mesures d’évaluation (précision et rappel) pour chaque session d’entraînement terminée en cliquant sur la session d’entraînement.
2. Explorez les informations fournies pour chaque mesure d’évaluation. Plus ces mesures sont élevées, plus le modèle est performant.
   ![](../images/models-recipes/model-walkthrough/evaluation_metrics.png)
3. Vous pouvez voir le jeu de données, les schémas et les paramètres de configuration utilisés pour chaque session d’entraînement sur le rail droit.
4. Revenez à la page Modèle et identifiez les sessions d’entraînement les plus performantes en observant leurs mesures d’évaluation.

## Exploitation de votre modèle {#operationalize-your-model}

La dernière étape du workflow Data Science consiste à rendre opérationnel votre modèle afin de recueillir et d’exploiter les insights de votre banque de données.

### Évaluation et génération d’insights

1. Sur la page de *présentation* du modèle de recommandations de produits, cliquez sur le nom de la session d’entraînement la plus performante, avec les valeurs de rappel et de précision les plus élevées.
2. Dans la partie supérieure droite de la page des détails de la session d’entraînement, cliquez sur **[!UICONTROL Évaluer]**.
3. Sélectionnez le **[!UICONTROL jeu de données d’entrée des recommandations]** comme jeu de données d’entrée de notation, qui est le même jeu de données que celui utilisé lors de la création du modèle et de l’exécution de ses sessions d’entraînement. Cliquez ensuite sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/model-walkthrough/scoring_input.png)
4. Sélectionnez le **[!UICONTROL jeu de données de sortie des recommandations]** comme jeu de données de sortie de notation. Les résultats de notation seront stockés dans ce jeu de données sous la forme d’un lot.
   ![](../images/models-recipes/model-walkthrough/scoring_output.png)
5. Vérifiez les configurations de notation. Ces paramètres contiennent les jeux de données d’entrée et de sortie sélectionnés plus tôt, ainsi que les schémas appropriés. Cliquez sur **[!UICONTROL Terminer]** pour lancer l’opération de notation. Cela peut prendre plusieurs minutes.
   ![](../images/models-recipes/model-walkthrough/scoring_configure.png)


### Affichage des insights évalués

Une fois l’opération de notation terminée, vous serez en mesure de prévisualiser les résultats et d’afficher les insights générés.

1. Sur la page des opérations de notation, cliquez sur l’opération de notation terminée, puis cliquez sur **[!UICONTROL Aperçu du jeu de données des résultats de la notation]** sur le rail de droite.
   ![](../images/models-recipes/model-walkthrough/score_complete.png)
2. Dans le tableau de prévisualisation, chaque ligne contient des recommandations de produits pour un client en particulier, respectivement libellés **[!UICONTROL recommendations]** et **[!UICONTROL userId]**. Puisque l’hyperparamètre **[!UICONTROL num_recommendations]** a été défini sur 10 dans les exemples de captures d’écran, chaque ligne de recommandations peut contenir jusqu’à 10 identités de produit délimitées par un signe dièse (#).
   ![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## Étapes suivantes {#next-steps}

Bien joué, vous avez généré avec succès des recommandations de produits.

This tutorial introduced you to the workflow of [!DNL Data Science Workspace], demonstrating how raw unprocessed data can be turned into useful information through machine learning. To learn more about using the [!DNL Data Science Workspace], continue to the next guide on [creating the retail sales schema and dataset](./create-retails-sales-dataset.md).