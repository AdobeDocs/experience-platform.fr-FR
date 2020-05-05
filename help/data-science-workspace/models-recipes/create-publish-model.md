---
keywords: Experience Platform;machine learning model;Data Science Workspace;popular topics
solution: Experience Platform
title: Création et publication d’une présentation du modèle d’apprentissage automatique
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Création et publication d’une présentation du modèle d’apprentissage automatique

![](../images/models-recipes/model-walkthrough/objective.png)

Faites semblant de posséder un site Web de vente au détail en ligne. Lorsque vos clients effectuent des achats sur votre site Web de vente au détail, vous souhaitez leur présenter des recommandations de produits personnalisées afin d’exposer une variété d’autres produits de votre offre d’entreprise. Au cours de l’existence de votre site Web, vous avez continuellement rassemblé les données client et souhaitez utiliser ces données pour générer des recommandations de produits personnalisées.

Adobe Experience Platform Data Science Workspace vous permet d’atteindre votre objectif à l’aide de la recette [de recommandations de produits prédéfinie](../pre-built-recipes/product-recommendations.md). Suivez ce didacticiel pour découvrir comment accéder à vos données de vente au détail et les comprendre, créer et optimiser un modèle d’apprentissage automatique et générer des informations dans Data Science Workspace.

Ce didacticiel reflète le flux de travail de Data Science Workspace et décrit les étapes suivantes pour créer un modèle d’apprentissage automatique :

1. [Préparation de vos données](#prepare-your-data)
2. [Créer votre modèle](#author-your-model)
3. [Formation et évaluation de votre modèle](#train-and-evaluate-your-model)
4. [Opérationaliser votre modèle](#operationalize-your-model)

## Prise en main

Avant de commencer ce didacticiel, vous devez disposer des conditions préalables suivantes :

* Accès à Adobe Experience Platform. Si vous n’avez pas accès à une organisation IMS dans Experience Platform, contactez votre administrateur système avant de continuer.

* Ressources d’activation. Contactez votre gestionnaire de compte pour que les éléments suivants soient mis en service.
   * Recommandations Recette
   * Jeu de données d’entrée de Recommendations
   * Schéma d’entrée Recommendations
   * Jeu de données de sortie de recommandations
   * Schéma de sortie Recommendations
   * PostValues de l’ensemble de données d’or
   * Schéma d&#39;ensemble de données en or

* Téléchargez les trois fichiers Jupyter Notebook requis depuis le référentiel <a href="https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs" target="_blank">public Git d’</a>Adobe. Ils seront utilisés pour démontrer le flux de travaux JupyterLab dans Data Science Workspace.

* Une compréhension pratique des concepts clés suivants utilisés dans ce tutoriel :
   * [Modèle](../../xdm/home.md)de données d’expérience : Effort de normalisation mené par Adobe pour définir des schémas standard tels que Profil et ExperienceEvent, pour la gestion de l’expérience client.
   * Jeu de données : Un concept d’enregistrement et de gestion pour les données réelles. Instance instanciée physique d’un Schéma [](../../xdm/schema/field-dictionary.md)XDM.
   * Lots : Les jeux de données sont composés de lots. Un lot est un ensemble de données collectées sur une période donnée et traitées ensemble en une seule unité.
   * JupyterLab : [JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) est une interface web open-source pour Project Jupyter et est étroitement intégrée dans Experience Platform.

## Préparation de vos données {#prepare-your-data}

Pour créer un modèle d’apprentissage automatique qui fait des recommandations de produits personnalisées à vos clients, les achats précédents de clients sur votre site Web doivent être analysés. Cette section explique comment ces données sont ingérées dans la plate-forme via Adobe Analytics et comment ces données sont transformées en un jeu de données de fonctionnalités qui sera utilisé par votre modèle d’apprentissage automatique.

### Explorer les données et comprendre les schémas

1. Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com/) et cliquez sur **[!UICONTROL Datasets]** pour liste tous les jeux de données existants et sélectionnez le jeu de données que vous souhaitez explorer. Dans ce cas, le jeu de données Analytics **Golden Data Set postValues**.
   ![](../images/models-recipes/model-walkthrough/datasets_110.png)
2. Sélectionnez **[!UICONTROL Preview Dataset]** près de l’angle supérieur droit pour examiner les exemples d’enregistrements, puis cliquez sur **[!UICONTROL Close]**.
   ![](../images/models-recipes/model-walkthrough/golden_data_set_110.png)
3. Sélectionnez le lien sous Schéma dans le rail de droite pour vue du schéma du jeu de données, puis revenez à la page des détails du jeu de données.&quot;
   ![](../images/models-recipes/model-walkthrough/golden_schema_110.png)

Les autres jeux de données ont été préremplis avec des lots à des fins d’aperçu. Vous pouvez vue ces jeux de données en répétant les étapes ci-dessus.

| Nom du jeu de données | Schéma | Description |
| ----- | ----- | ----- |
| PostValues de l’ensemble de données d’or | schéma d&#39;ensemble de données en or | Données source Analytics de votre site Web |
| Jeu de données d’entrée de Recommendations | Schéma d’entrée Recommendations | Les données Analytics sont transformées en un jeu de données de formation à l’aide d’un pipeline de fonctionnalités. Ces données servent à former le modèle d’apprentissage automatique de Recommandations de produits. `itemid` et correspondent `userid` à un produit acheté par ce client. |
| Jeu de données de sortie de recommandations | Schéma de sortie Recommendations | Le jeu de données pour lequel les résultats d&#39;évaluation sont stockés contient la liste des produits recommandés pour chaque client. |

## Créer votre modèle {#author-your-model}

Le deuxième composant du cycle de vie de l&#39;espace de travail Data Science implique la création de recettes et de modèles. La Recette des recommandations de produits est conçue pour générer des recommandations de produits à grande échelle en utilisant les données d&#39;achat antérieures et l&#39;apprentissage automatique.

Les recettes sont la base d&#39;un modèle car elles contiennent des algorithmes d&#39;apprentissage automatique et une logique conçue pour résoudre des problèmes spécifiques. Plus important encore, les Recettes vous permettent de démocratiser l&#39;apprentissage automatique dans votre entreprise, en permettant à d&#39;autres utilisateurs d&#39;accéder à un modèle pour des cas d&#39;utilisation disparates sans écrire de code.

### Explorez la recette des recommandations de produits

1. Dans Adobe Experience Platform, accédez à **[!UICONTROL Models]** la colonne de navigation de gauche, puis cliquez **[!UICONTROL Recipes]** en haut pour vue une liste de recettes disponibles pour votre organisation.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. Recherchez et ouvrez le fichier fourni **[!UICONTROL Recommendations Recipe]** en cliquant sur son nom.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. Dans le rail de droite, cliquez sur **[!UICONTROL Recommendations Input Schema]** pour vue le schéma qui alimente la recette. Le schéma **[!UICONTROL itemId]** et **[!UICONTROL userId]** correspondent à un produit acheté (**[!UICONTROL interactionType]**) par ce client à un moment spécifique (**[!UICONTROL timestamp]**). Suivez les mêmes étapes pour consulter les champs du **[!UICONTROL Recommendations Output Schema]**.
   ![](../images/models-recipes/model-walkthrough/preview_schemas.png)

Vous avez maintenant passé en revue les schémas d’entrée et de sortie requis par la Recette des recommandations de produits. Vous pouvez maintenant passer à la section suivante pour découvrir comment créer, former et évaluer un modèle de recommandations de produits.

## Formation et évaluation de votre modèle {#train-and-evaluate-your-model}

Maintenant que vos données sont préparées et que la Recette est prête à être utilisée, vous pouvez créer, former et évaluer votre modèle d&#39;apprentissage automatique.

### Créer un modèle

Un modèle est l&#39;instance d&#39;une Recette, ce qui vous permet de vous former et de marquer des données à l&#39;échelle.

1. Dans Adobe Experience Platform, accédez à **[!UICONTROL Models]** la colonne de navigation de gauche, puis cliquez **[!UICONTROL Recipes]** en haut de la page pour afficher une liste de toutes les recettes disponibles pour votre entreprise.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. Recherchez et ouvrez le fichier fourni **[!UICONTROL Recommendations Recipe]** en cliquant sur son nom, en entrant la page d&#39;aperçu de la Recette. Cliquez **[!UICONTROL Create a Model]** soit à partir du centre (s&#39;il n&#39;y a pas de modèles existants), soit en haut à droite de la page Aperçu de la recette.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. Une liste des jeux de données d’entrée disponibles pour la formation s’affiche, sélectionnez **[!UICONTROL Recommendations Input Dataset]** puis cliquez sur **[!UICONTROL Next]**.
   ![](../images/models-recipes/model-walkthrough/select_dataset.png)
4. Nommez le modèle, par exemple &quot;Modèle de recommandations de produits&quot;. Les configurations disponibles pour le modèle sont répertoriées, contenant les paramètres des comportements de formation et de notation par défaut du modèle. Aucune modification n’est nécessaire, car ces configurations sont spécifiques à votre entreprise. Vérifiez les configurations et cliquez sur **[!UICONTROL Finish]**.
   ![](../images/models-recipes/model-walkthrough/configure_model.png)
5. Le modèle a maintenant été créé et la page *Aperçu* du modèle s&#39;affiche au cours d&#39;une nouvelle période de formation. Une exécution de formation est générée par défaut lors de la création d&#39;un modèle.
   ![](../images/models-recipes/model-walkthrough/model_post_creation.png)

Vous pouvez choisir d’attendre la fin de la session de formation ou de continuer à créer une nouvelle session de formation dans la section suivante.

### Formation du modèle à l’aide d’hyperparamètres personnalisés

1. Sur la page Aperçu *du* modèle, cliquez **[!UICONTROL Train]** en haut à droite pour créer une nouvelle session de formation. Sélectionnez le même jeu de données d&#39;entrée que celui utilisé lors de la création du modèle, puis cliquez sur **[!UICONTROL Next]**.
   ![](../images/models-recipes/model-walkthrough/training_select_dataset.png)
2. The *Configuration* page appears. Vous pouvez ici configurer la **[!UICONTROL num_recommendations]** valeur de la série d’exercices, également appelée Hyperparamètre. Un modèle formé et optimisé utilisera les paramètres Hyperparamètres les plus performants en fonction des résultats de l&#39;entraînement.

   Les hyperparamètres ne peuvent pas être appris. Par conséquent, ils doivent être affectés avant l’exécution de la formation. L&#39;ajustement d&#39;hyperparamètres peut modifier la précision du modèle formé. Comme l&#39;optimisation d&#39;un modèle est un processus itératif, il peut s&#39;avérer nécessaire de procéder à plusieurs exercices de formation avant d&#39;effectuer une évaluation satisfaisante.

   >[!TIP] Définissez **[!UICONTROL num_recommendations]** sur 10.

   ![](../images/models-recipes/model-walkthrough/configure_hyperparameter.png)
3. Un point de données supplémentaire apparaîtra sur le graphique d&#39;évaluation du modèle une fois la nouvelle période de formation terminée, cette opération peut prendre jusqu&#39;à plusieurs minutes.
   ![](../images/models-recipes/model-walkthrough/post_training_run.png)

### Évaluer le modèle

Chaque fois qu’une formation est terminée, vous pouvez vue les mesures d’évaluation qui en résultent afin de déterminer l’efficacité du modèle.

1. Consultez les mesures d&#39;évaluation (Précision et Rappel) pour chaque période de formation terminée en cliquant sur sur la période de formation.
2. Explorez les informations fournies pour chaque mesure d’évaluation. Plus ces mesures sont élevées, meilleure est la performance du modèle.
   ![](../images/models-recipes/model-walkthrough/evaluation_metrics.png)
3. Vous pouvez voir le jeu de données, le schéma et les paramètres de configuration utilisés pour chaque exécution de formation sur le rail droit.
4. Revenez à la page Modèle et identifiez les formations les plus performantes exécutées en observant leurs mesures d’évaluation.

## Opérationaliser votre modèle {#operationalize-your-model}

La dernière étape du flux de travaux Data Science consiste à rendre opérationnel votre modèle afin de recueillir et d’exploiter les informations de votre banque de données.

### Score et génération d’informations

1. Sur la page *Présentation* du modèle des recommandations de produit, cliquez sur le nom de la série de formation la plus performante, avec les valeurs de rappel et de précision les plus élevées.
2. Dans l’angle supérieur droit de la page des détails de l’exécution de la formation, cliquez sur **[!UICONTROL Score]**.
3. Sélectionnez le **[!UICONTROL Recommendations Input Dataset]** jeu de données d&#39;entrée de score, qui est le même jeu de données que celui utilisé lors de la création du modèle et de l&#39;exécution de ses exécutions de formation. Then, click **[!UICONTROL Next]**.
   ![](../images/models-recipes/model-walkthrough/scoring_input.png)
4. Sélectionnez le **[!UICONTROL Recommendations Output Dataset]** jeu de données de sortie de score. Les résultats de score seront stockés par lot dans ce jeu de données.
   ![](../images/models-recipes/model-walkthrough/scoring_output.png)
5. Examinez les configurations d’évaluation. Ces paramètres contiennent les jeux de données d’entrée et de sortie sélectionnés plus tôt, ainsi que les schémas appropriés. Cliquez sur **[!UICONTROL Finish]** pour commencer l’exécution de notation. L&#39;exécution peut prendre plusieurs minutes.
   ![](../images/models-recipes/model-walkthrough/scoring_configure.png)


### Vue des connaissances notées

Une fois l’exécution de score terminée, vous pourrez prévisualisation les résultats et vue les informations générées.

1. Sur la page des séries de résultats, cliquez sur la série de résultats terminée, puis cliquez sur **[!UICONTROL Preview Scoring Results Dataset]** le rail de droite.
   ![](../images/models-recipes/model-walkthrough/score_complete.png)
2. Dans le tableau de la prévisualisation, chaque ligne contient des recommandations de produit pour un client particulier, libellées **[!UICONTROL recommendations]** et **[!UICONTROL userId]** respectivement. Comme l’ **[!UICONTROL num_recommendations]** hyperparamètre a été défini sur 10 dans les exemples de captures d’écran, chaque ligne de recommandations peut contenir jusqu’à 10 identités de produit délimitées par un signe dièse (#).
   ![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## Étapes suivantes {#next-steps}

Bien joué, vous avez généré avec succès des recommandations de produits !

Ce didacticiel vous a présenté le flux de travail de Data Science Workspace, qui montre comment les données brutes non traitées peuvent être transformées en informations utiles par l’apprentissage automatique. Pour en savoir plus sur l’utilisation de Data Science Workspace, consultez le guide suivant sur la [création du schéma de vente au détail et du jeu de données](./create-retails-sales-dataset.md).