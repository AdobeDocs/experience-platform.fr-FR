---
keywords: Experience Platform;modèle d’apprentissage automatique;Data Science Workspace;rubriques les plus consultées;créer et publier un modèle
solution: Experience Platform
title: Création et publication d’un modèle d’apprentissage automatique
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace vous donne les moyens d’atteindre votre objectif à l’aide de la recette des recommandations de produits prédéfinie. Suivez ce tutoriel pour découvrir comment accéder à vos données de vente au détail et les comprendre, créer et optimiser un modèle d’apprentissage automatique et générer des insights dans Data Science Workspace.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 41%

---

# Création et publication d’un modèle d’apprentissage automatique

![](../images/models-recipes/model-walkthrough/objective.png)

Imaginons que vous possédez un site web de vente en ligne. Lorsque vos clients achètent sur votre site web de vente en ligne, vous souhaitez leur présenter des recommandations de produits personnalisées afin d’exposer une variété d’autres produits proposés par votre entreprise. Au cours de l’existence de votre site web, vous avez continuellement rassemblé des données clients et souhaitez utiliser ces données d’une manière ou d’une autre pour générer des recommandations de produits personnalisées.

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] fournit les moyens d’atteindre votre objectif à l’aide de la recette [ Recommendations de ](../pre-built-recipes/product-recommendations.md)produit prédéfinie. Suivez ce tutoriel pour découvrir comment accéder à vos données de vente au détail et les comprendre, créer et optimiser un modèle d’apprentissage automatique et générer des insights dans [!DNL Data Science Workspace].

Ce tutoriel reflète le processus de [!DNL Data Science Workspace] et couvre les étapes suivantes pour créer un modèle d’apprentissage automatique :

1. [Préparation de vos données](#prepare-your-data)
2. [Création de votre modèle](#author-your-model)
3. [Formation et évaluation de votre modèle](#train-and-evaluate-your-model)
4. [Exploitation de votre modèle](#operationalize-your-model)

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :

- Accès à [!DNL Adobe Experience Platform]. Si vous n’avez pas accès à une organisation IMS dans [!DNL Experience Platform], contactez votre administrateur système avant de poursuivre.

- Ressources d’activation. Contactez le représentant de votre compte pour que les éléments suivants soient mis en service.
   - Recette des recommandations
   - Jeu de données d’entrée des recommandations
   - Schéma d’entrée des recommandations
   - Jeu de données de sortie des recommandations
   - Schéma de sortie des recommandations
   - Valeurs de publication du jeu de données favori
   - Schéma du jeu de données favori

- Téléchargez les trois fichiers [!DNL Jupyter Notebook] requis à partir du [référentiel  [!DNL Git] Adobe public](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs). Ils serviront à démontrer le workflow [!DNL JupyterLab] dans [!DNL Data Science Workspace].

Une connaissance concrète des concepts clés suivants employés dans ce tutoriel :
- [[!DNL Experience Data Model]](../../xdm/home.md): L’effort de normalisation conduit par Adobe pour définir des schémas standard tels que  [!DNL Profile] et ExperienceEvent, pour la gestion de l’expérience client.
- Jeux de données : construction de stockage et de gestion pour les données réelles. Instance instanciée physique d’un [schéma XDM](../../xdm/schema/field-dictionary.md).
- Lots : les jeux de données sont constitués de lots. Un lot est un ensemble de données collectées sur une période donnée et traitées ensemble comme une seule unité.
- [!DNL JupyterLab]:  [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) est une interface web open source pour Project  [!DNL Jupyter] et est étroitement intégrée à  [!DNL Experience Platform].

## Préparation de vos données {#prepare-your-data}

Pour créer un modèle d’apprentissage automatique qui recommande des produits personnalisés à vos clients, vous devez analyser les achats précédents de clients sur votre site web. Cette section explique comment ces données sont ingérées dans [!DNL Platform] par [!DNL Adobe Analytics] et comment elles sont transformées en jeu de données de fonctionnalités à utiliser par votre modèle d’apprentissage automatique.

### Exploration des données et compréhension des schémas

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Jeux de données]** pour répertorier tous les jeux de données existants et sélectionner le jeu de données que vous souhaitez explorer. Dans ce cas, le [!DNL Analytics] jeu de données **Valeurs de publication du jeu de données favori**.

![](../images/models-recipes/model-walkthrough/dataset-browse.png)

La page d’activité du jeu de données s’ouvre, répertoriant les informations relatives à votre jeu de données. Vous pouvez sélectionner **[!UICONTROL Aperçu du jeu de données]** près du coin supérieur droit pour examiner les exemples d’enregistrements. Vous pouvez également afficher le schéma du jeu de données sélectionné. Sélectionnez le lien du schéma dans le rail droit. Une fenêtre contextuelle s’affiche, en sélectionnant le lien sous **[!UICONTROL nom du schéma]** pour ouvrir le schéma dans un nouvel onglet.

![](../images/models-recipes/model-walkthrough/dataset-activity.png)


![](../images/models-recipes/model-walkthrough/schema-view.png)

Les autres jeux de données ont été préremplis avec des lots à des fins d’aperçu. Vous pouvez afficher ces jeux de données en répétant les étapes ci-dessus.

| Nom du jeu de données | Schéma | Description |
| ----- | ----- | ----- |
| Valeurs de publication du jeu de données favori | Schéma du jeu de données favori | [!DNL Analytics]Données source de votre site web |
| Jeu de données d’entrée des recommandations | Schéma d’entrée des recommandations | Les données [!DNL Analytics] sont transformées en jeu de données d’apprentissage à l’aide d’un pipeline de fonctionnalités. Ces données sont utilisées pour former le modèle d’apprentissage automatique de recommandations de produits. `itemid` et `userid` correspondent à un produit acheté par ce client. |
| Jeu de données de sortie des recommandations | Schéma de sortie des recommandations | Le jeu de données pour lequel les résultats de notation sont stockés contient la liste des produits recommandés pour chaque client. |

## Création de votre modèle {#author-your-model}

Le deuxième composant du cycle de vie [!DNL Data Science Workspace] implique la création de recettes et de modèles. La recette des recommandations de produits est conçue pour générer des recommandations de produits à grande échelle en utilisant les données d’achats antérieurs et l’apprentissage automatique.

Les recettes sont la base d’un modèle puisqu’elles contiennent des algorithmes d’apprentissage automatique et une logique conçue pour résoudre des problèmes spécifiques. Plus important encore, les recettes vous permettent de démocratiser l’apprentissage automatique au sein de votre organisation, en permettant à d’autres utilisateurs d’accéder à un modèle pour des cas d’utilisation variés sans devoir coder.

### Exploration de la recette des recommandations de produits

Dans Experience Platform, accédez à **[!UICONTROL Modèles]** dans la colonne de navigation de gauche, puis sélectionnez **[!UICONTROL Recettes]** dans la barre de navigation supérieure pour afficher la liste des recettes disponibles pour votre organisation.

![](../images/models-recipes/model-walkthrough/recipe-tab.png)

Recherchez et ouvrez ensuite la **[!UICONTROL recette Recommendations]** fournie en sélectionnant son nom. La page de présentation de la recette s’affiche.

![](../images/models-recipes/model-walkthrough/Recipe-view.png)

Ensuite, dans le rail de droite, sélectionnez **[!UICONTROL Recommendations Input Schema]** pour afficher le schéma qui alimente la recette. Les champs de schéma &quot;[!UICONTROL itemId]&quot; et &quot;[!UICONTROL userId]&quot; correspondent à un produit acheté ([!UICONTROL interactionType]) par ce client à un moment spécifique ([!UICONTROL horodatage]). Suivez les mêmes étapes pour consulter le **[!UICONTROL Schéma de sortie des recommandations]**.

![](../images/models-recipes/model-walkthrough/input-output.png)

Vous avez maintenant examiné les schémas d’entrée et de sortie requis par la recette des recommandations de produits. Passez à la section suivante pour savoir comment créer, former et évaluer un modèle Recommendations de produit.

## Formation et évaluation de votre modèle {#train-and-evaluate-your-model}

Maintenant que vos données sont préparées et que la recette est prête, vous pouvez créer, former et évaluer votre modèle d’apprentissage automatique.

### Création d’un modèle

Un modèle est une instance de recette qui permet l’entraînement et l’évaluation de données à grande échelle.

Dans Experience Platform, accédez à **[!UICONTROL Modèles]** dans la colonne de navigation de gauche, puis sélectionnez **[!UICONTROL Recettes]** dans la barre de navigation supérieure. Elle affiche une liste des recettes disponibles pour votre organisation. Sélectionnez la recette de recommandation de produit.

![](../images/models-recipes/model-walkthrough/recipe-tab.png)

Sur la page de recette, sélectionnez **[!UICONTROL Créer un modèle]**.

![créer un modèle](../images/models-recipes/model-walkthrough/create-model-recipe.png)

Le processus de création de modèle commence par la sélection d’une recette. Sélectionnez la **[!UICONTROL recette Recommendations]** , puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit.

![](../images/models-recipes/model-walkthrough/create-model.png)

Indiquez ensuite un nom de modèle. Les configurations disponibles pour le modèle sont répertoriées avec des paramètres pour les comportements de formation et de notation par défaut du modèle. Vérifiez les configurations et sélectionnez **[!UICONTROL Terminer]**.

![](../images/models-recipes/model-walkthrough/configure-model.png)

Vous êtes redirigé vers la page d’aperçu de vos modèles avec une nouvelle session d’entraînement. Une session d’entraînement est générée par défaut lors de la création d’un modèle.

![](../images/models-recipes/model-walkthrough/model-overview.png)

Vous pouvez choisir d’attendre la fin de la session d’entraînement ou continuer à créer une session d’entraînement dans la section suivante.

### Entraînement du modèle à l’aide d’hyperparamètres personnalisés

Sur la page **Aperçu du modèle**, sélectionnez **[!UICONTROL Former]** près du coin supérieur droit pour créer une nouvelle opération de formation. Sélectionnez le même jeu de données d’entrée que celui utilisé lors de la création du modèle et sélectionnez **[!UICONTROL Suivant]**.

![](../images/models-recipes/model-walkthrough/select-train.png)

La page de **[!UICONTROL configuration]** s’affiche. Ici, vous pouvez configurer la valeur des exécutions de formation `num_recommendations`, également appelée hyperparamètre. Un modèle formé et optimisé utilisera les hyperparamètres les plus performants en fonction des résultats de l’opération de formation.

Les hyperparamètres ne peuvent pas être appris. Par conséquent, ils doivent être attribués avant les sessions d’entraînement. Le réglage d’hyperparamètres peut modifier la précision du modèle formé. L’optimisation d’un modèle étant un processus itératif, plusieurs opérations de formation peuvent être nécessaires avant qu’une évaluation satisfaisante ne soit réalisée.

>[!TIP]
>
>Définissez `num_recommendations` sur 10.

![](../images/models-recipes/model-walkthrough/training-configuration.png)

D’autres points de données s’affichent sur le graphique d’évaluation du modèle. Cette opération peut prendre plusieurs minutes une fois l’exécution terminée.

![](../images/models-recipes/model-walkthrough/training-graphs.png)

### Évaluation du modèle

Chaque fois qu’une session d’entraînement se termine, vous pouvez afficher les mesures d’évaluation qui en résultent pour déterminer l’efficacité du modèle.

Pour passer en revue les mesures d’évaluation (précision et rappel) pour chaque session d’entraînement terminée, sélectionnez la session d’entraînement.

![](../images/models-recipes/model-walkthrough/select-training-run.png)

Vous pouvez explorer les informations fournies pour chaque mesure d’évaluation. Plus ces mesures sont élevées, plus le modèle est performant.

![](../images/models-recipes/model-walkthrough/metrics.png)

Vous pouvez voir le jeu de données, les schémas et les paramètres de configuration utilisés pour chaque session d’entraînement sur le rail droit. Revenez à la page Modèle et identifiez les sessions d’entraînement les plus performantes en observant leurs mesures d’évaluation.

## Exploitation de votre modèle {#operationalize-your-model}

La dernière étape du workflow Data Science consiste à rendre opérationnel votre modèle afin de recueillir et d’exploiter les insights de votre banque de données.

### Évaluation et génération d’insights

Sur la page d’aperçu du modèle de recommandations de produits, sélectionnez le nom de la session d’entraînement la plus performante, avec les valeurs de rappel et de précision les plus élevées.

![noter la meilleure opération](../images/models-recipes/model-walkthrough/select-training-run.png)

Ensuite, en haut à droite de la page des détails de l’opération de formation, sélectionnez **[!UICONTROL Score]**.

![sélectionner un score](../images/models-recipes/model-walkthrough/select-score.png)

Sélectionnez ensuite le **[!UICONTROL jeu de données d’entrée Recommendations]** comme jeu de données d’entrée de notation, qui est le même jeu de données que celui utilisé lors de la création du modèle et de l’exécution de ses opérations de formation. Sélectionnez ensuite **[!UICONTROL Suivant]**.

![](../images/models-recipes/model-walkthrough/score-input.png)

Une fois que vous disposez de votre jeu de données d’entrée, sélectionnez le **[!UICONTROL jeu de données de sortie Recommendations]** comme jeu de données de sortie de notation. Les résultats de notation sont stockés dans ce jeu de données sous la forme d’un lot.

![](../images/models-recipes/model-walkthrough/score-output.png)

Enfin, passez en revue les configurations de notation. Ces paramètres contiennent les jeux de données d’entrée et de sortie que vous avez sélectionnés précédemment, ainsi que les schémas appropriés. Sélectionnez **[!UICONTROL Terminer]** pour lancer l’opération de notation. Cela peut prendre plusieurs minutes.

![](../images/models-recipes/model-walkthrough/score-finish.png)

### Affichage des insights évalués

Une fois l’opération de notation terminée, vous pouvez prévisualiser les résultats et afficher les informations générées.

Sur la page des opérations de notation, sélectionnez l’opération de notation terminée, puis sélectionnez **[!UICONTROL Aperçu du jeu de données des résultats de la notation]** sur le rail de droite.

![](../images/models-recipes/model-walkthrough/preview-scores.png)

Dans le tableau de prévisualisation, chaque ligne contient des recommandations de produits pour un client en particulier, respectivement libellés [!UICONTROL recommendations] et [!UICONTROL userId]. Puisque l’hyperparamètre [!UICONTROL num_recommendations] a été défini sur 10 dans les exemples de captures d’écran, chaque ligne de recommandations peut contenir jusqu’à 10 identités de produit délimitées par un signe dièse (#).

![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## Étapes suivantes {#next-steps}

Ce tutoriel vous a présenté le workflow de [!DNL Data Science Workspace], en montrant comment les données brutes non traitées peuvent être transformées en informations utiles grâce à l’apprentissage automatique. Pour en savoir plus sur l’utilisation de [!DNL Data Science Workspace], consultez le guide suivant sur la [création du schéma et du jeu de données des ventes au détail](./create-retails-sales-dataset.md).
