---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Présentation détaillée de Data Science Workspace
topic: Walkthrough
description: Ce document fournit une présentation détaillée d’Adobe Experience Platform Data Science Workspace. Plus précisément, le processus général par lequel un chercheur de données doit résoudre un problème à l’aide de l’apprentissage automatique.
translation-type: tm+mt
source-git-commit: 0d76b14599bc6b6089f9c760ef6a6be3a19243d4
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 33%

---


# [!DNL Data Science Workspace] parcours

This document provides a walkthrough for Adobe Experience Platform [!DNL Data Science Workspace]. Ce didacticiel présente un flux de travail général des chercheurs en données et explique comment ils peuvent aborder et résoudre un problème à l’aide de l’apprentissage automatique.

## Conditions préalables

- Compte Adobe ID enregistré
   - The Adobe ID account must have been added to an Organization with access to Adobe Experience Platform and [!DNL Data Science Workspace].

## Cas d’utilisation au détail

Un détaillant doit faire face à de nombreux défis pour rester compétitif sur le marché actuel. L&#39;une des principales préoccupations du détaillant est de décider du prix optimal d&#39;un produit et de prévoir les tendances de vente. Grâce à un modèle de prévision précis, un détaillant serait en mesure de trouver la relation entre les politiques de demande et de tarification et de prendre des décisions de prix optimisées pour maximiser les ventes et les recettes.

## Solution du spécialiste des données

La solution d&#39;un chercheur en données consiste à exploiter la richesse des informations historiques fournies par un détaillant, à prédire les tendances futures et à optimiser les décisions de prix. Cette procédure pas à pas utilise les données des ventes passées pour former un modèle d&#39;apprentissage automatique et utilise ce modèle pour prédire les tendances futures des ventes. Ainsi, vous pouvez générer des informations pour vous aider à apporter des modifications de tarification optimales.

Cet aperçu reflète les étapes qu&#39;un chercheur de données suivrait pour créer un jeu de données et un modèle pour prédire les ventes hebdomadaires. Ce didacticiel couvre les sections suivantes de l&#39;exemple de carnet de vente au détail sur Adobe Experience Platform [!DNL Data Science Workspace]:

- [Configuration](#setup)
- [Exploration des données](#exploring-data)
- [Conception des fonctionnalités](#feature-engineering)
- [Formation et vérification](#training-and-verification)

### Ordinateurs portables dans [!DNL Data Science Workspace]

Dans l’interface utilisateur de Adobe Experience Platform, sélectionnez **[!UICONTROL Ordinateurs portables]** dans l’onglet Science **[!UICONTROL des]** données pour accéder à la page d’aperçu [!UICONTROL Ordinateurs portables] . Dans cette page, sélectionnez l&#39; [!DNL JupyterLab] onglet pour lancer votre [!DNL JupyterLab] environnement. Le landing page par défaut pour [!DNL JupyterLab] est le **[!UICONTROL lanceur]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

Ce didacticiel utilise [!DNL Python] 3 dans [!DNL JupyterLab Notebooks] pour montrer comment accéder aux données et les explorer. Sur la page du lanceur, vous trouverez des notebooks d’exemple. L&#39;exemple de bloc-notes **[!UICONTROL Ventes]** au détail est utilisé dans les exemples fournis ci-dessous.

### Configuration {#setup}

Avec le bloc-notes Ventes au détail ouvert, la première chose à faire est de charger les bibliothèques requises pour votre flux de travail. La liste suivante décrit brièvement chacune des bibliothèques utilisées dans les exemples dans les étapes suivantes.

- **insensible**: Bibliothèque informatique scientifique qui ajoute la prise en charge de grandes matrices et matrices multidimensionnelles
- **pandas**: Bibliothèque qui offre les structures de données et les opérations utilisées pour la manipulation et l’analyse des données
- **matplotlib.pyplot**: Chargement d’une bibliothèque fournissant une expérience de type MATLAB lors du mappage
- **seaborn** : Bibliothèque de visualisation de données d’interface de haut niveau basée sur matplotlib
- **sklearn**: Bibliothèque d’apprentissage automatique qui comprend des algorithmes de classification, de régression, de vecteur de prise en charge et de cluster
- **avertissements**: Bibliothèque qui contrôle les messages d’avertissement

### Exploration des données {#exploring-data}

#### Chargement des données

Une fois les bibliothèques chargées, vous pouvez début d’examiner les données. The following [!DNL Python] code uses pandas&#39; `DataFrame` data structure and the [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) function to read the CSV hosted on [!DNL Github] into the pandas DataFrame:

![](./images/walkthrough/read_csv.png)

La structure de données du DataFrame de pandas est une structure de données étiquetées en deux dimensions. To quickly see the dimensions of your data, you can use `df.shape`. Cette opération renvoie un tuple qui représente les dimensions du DataFrame :

![](./images/walkthrough/df_shape.png)

Enfin, vous pouvez prévisualisation à quoi ressemblent vos données. You can use `df.head(n)` to view the first `n` rows of the DataFrame:

![](./images/walkthrough/df_head.png)

#### Résumé statistique

We can leverage [!DNL Python's] pandas library to get the data type of each attribute. La sortie de l’appel suivant nous donnera des informations sur le nombre d’entrées et le type de données pour chacune des colonnes :

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Ces informations sont utiles, car elles aident à identifier la méthode de traitement de ces données.

Regardons maintenant le résumé statistique. Seuls les types de données numériques s’affichent. `date`, `storeType` et `isHoliday` ne sont donc pas générés :

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Vous pouvez ainsi voir qu’il y a 6 435 instances pour chaque caractéristique. Nous obtenons également des informations statistiques, telles que la moyenne, l’écart type, le minimum, le maximum et les plages interquartiles. Cela nous permet d’identifier les variations de données. Dans la section suivante, vous allez passer en revue la visualisation qui fonctionne avec ces informations pour nous donner une compréhension complète de vos données.

Looking at the minimum and maximum values for `store`, you can see that there are 45 unique stores the data represents. Les `storeTypes` permettent également de différencier les boutiques. you can see the distribution of `storeTypes` by doing the following:

![](./images/walkthrough/df_groupby.png)

Ici, nous avons 22 boutiques `storeType A`, 17 boutiques `storeType B` et 6 boutiques `storeType C`.

#### Visualisation des données

Maintenant que vous connaissez les valeurs de vos blocs de données, vous souhaitez ajouter à cela des visualisations afin de rendre les choses plus claires et plus faciles à identifier. Ces graphiques servent également à transmettre les résultats à une audience.

#### Graphiques unidimensionnels

Les graphiques unidimensionnels sont des tracés représentant une seule variable. La boîte à moustaches est un graphique unidimensionnel couramment utilisé pour visualiser les données.

En utilisant votre jeu de données de vente au détail d&#39;avant, vous pouvez générer le schéma de boîte et de whisky pour chacun des 45 magasins et leurs ventes hebdomadaires. Le graphique est généré à l’aide de la fonction `seaborn.boxplot`.

![](./images/walkthrough/box_whisker.png)

Un graphique de boîte à moustaches sert à illustrer la distribution des données. Les lignes extérieures du graphique représentent les quartiles supérieur et inférieur, tandis que la boîte s’étend sur la plage interquartile. La ligne dans la zone indique la médiane. Tout point de données plus de 1,5 fois supérieur ou inférieur au quartile est marqué sous forme de cercle. Ces points sont considérés comme des valeurs aberrantes.

Ensuite, vous pouvez tracer les ventes hebdomadaires avec le temps. Vous n&#39;afficherez que la sortie de la première boutique. Le code du notebook génère 6 tracés correspondant à 6 des 45 boutiques de notre jeu de données.

![](./images/walkthrough/weekly_sales.png)

Ce diagramme permet de comparer les ventes hebdomadaires sur une période de 2 ans. Nous pouvons facilement repérer les motifs des pics et des creux de ventes au fil du temps.

#### Graphiques multidimensionnels

Les graphiques multidimensionnels servent à visualiser les interactions entre les variables. Grâce à cette visualisation, les spécialistes des données peuvent vérifier s’il existe des corrélations ou des motifs entre les variables. La matrice de corrélation est un graphique multidimensionnel couramment utilisé. Avec une matrice de corrélation, les dépendances entre les différentes variables sont quantifiées à l’aide d’un coefficient de corrélation.

En utilisant le même jeu de données de vente au détail, vous pouvez générer la matrice de corrélation.

![](./images/walkthrough/correlation_1.png)

Notez la diagonale de 1 au centre. Elle indique que lorsqu’une variable est comparée à elle-même, elle présente une corrélation positive entière. Une corrélation positive élevée aura une magnitude proche de 1, tandis que les corrélations faibles seront plus proches de 0. Une corrélation négative s’affiche sous la forme d’un coefficient négatif, indiquant une tendance inverse.

### Conception des fonctionnalités {#feature-engineering}

Dans cette section, l’ingénierie des fonctionnalités permet d’apporter des modifications à votre jeu de données de vente au détail en effectuant les opérations suivantes :

- Ajout de colonnes pour la semaine et l’année
- Convertir storeType en variable indicateur
- Convertir isHoliday en variable numérique
- Prévision des ventes hebdomadaires de la semaine prochaine

#### Ajout de colonnes pour la semaine et l’année

The current format for date (`2010-02-05`) can make it hard to differentiate that the data is for every week. Pour cette raison, vous devez convertir la date en semaine et année.

![](./images/walkthrough/date_to_week_year.png)

À présent, la semaine et la date s’affichent comme suit :

![](./images/walkthrough/date_week_year.png)

#### Conversion de storeType en variable indicatrice

Next, you want to convert the storeType column to columns representing each `storeType`. There are 3 store types, (`A`, `B`, `C`), from which you are creating 3 new columns. The value set in each is a boolean value where a &#39;1&#39; is set depending on what the `storeType` was and `0` for the other 2 columns.

![](./images/walkthrough/storeType.png)

La `storeType` colonne active est supprimée.

#### Conversion d’isHoliday en type numérique

La modification suivante consiste à remplacer la valeur booléenne `isHoliday` par une représentation numérique.

![](./images/walkthrough/isHoliday.png)

#### Prévision des ventes hebdomadaires de la semaine prochaine

Vous souhaitez maintenant ajouter des ventes hebdomadaires précédentes et futures à chacun de vos jeux de données. Vous pouvez le faire en compensant votre `weeklySales`comportement. En outre, la `weeklySales` différence est calculée. Pour cela, il faut soustraire les `weeklySales` aux `weeklySales` de la semaine précédente.

![](./images/walkthrough/weekly_past_future.png)

Since you are offsetting the `weeklySales` data 45 datasets forwards and 45 datasets backwards to create new columns, the first and last 45 data points have NaN values. You can remove these points from your dataset by using the `df.dropna()` function which removes all rows that have NaN values.

![](./images/walkthrough/dropna.png)

Vous trouverez ci-dessous un résumé du jeu de données après les modifications :

![](./images/walkthrough/df_info_new.png)

### Formation et vérification {#training-and-verification}

Il est maintenant temps de créer quelques modèles de données et de sélectionner le modèle qui sera le plus performant pour prédire les ventes futures. Vous allez évaluer les 5 algorithmes suivants :

- Régression linéaire
- Arborescence de décision
- Forêt aléatoire
- Amplification progressive
- Méthode des k plus proches voisins

#### Scission du jeu de données en sous-ensembles de formation et de test

Vous avez besoin d’un moyen de savoir à quel point votre modèle sera capable de prédire les valeurs. Cette évaluation peut être effectuée en allouant une partie du jeu de données comme données de validation, et le reste comme données de formation. Since `weeklySalesAhead` is the actual future values of `weeklySales`, you can use this to evaluate how accurate the model is at predicting the value. La scission se fait comme suit :

![](./images/walkthrough/split_data.png)

You now have `X_train` and `y_train` for preparing the models and `X_test` and `y_test` for evaluation later.

#### Contrôle des algorithmes

In this section, you declare all the algorithms into an array called `model`. Next, you iterate through this array and for each algorithm, input your training data with `model.fit()` which creates a model `mdl`. Grâce à ce modèle, vous pouvez prédire `weeklySalesAhead` avec vos `X_test` données.

![](./images/walkthrough/training_scoring.png)

For the scoring, you are taking the mean percentage difference between the predicted `weeklySalesAhead` with the actual values in the `y_test` data. Puisque vous souhaitez minimiser la différence entre votre prédiction et le résultat réel, le régresseur d&#39;augmentation du rayonnement est le modèle le plus performant.

#### Visualisation des prédictions

Enfin, vous visualisez votre modèle de prévision avec les valeurs de vente hebdomadaires réelles. La ligne bleue représente les chiffres réels, tandis que la ligne verte représente votre prévision à l’aide de l’augmentation du dégradé. Le code suivant génère 6 tracés qui représentent 6 des 45 magasins de votre jeu de données. Seule la boutique `Store 1` est illustrée ici :

![](./images/walkthrough/visualize_prediction.png)

## Étapes suivantes

Ce document couvrait un processus général de data scientist pour résoudre un problème de vente au détail. Pour résumer :

- Chargez les bibliothèques requises pour votre flux de travail.
- Une fois les bibliothèques chargées, vous pouvez début d’examiner les données à l’aide de résumés statistiques, de visualisations et de graphiques.
- Ensuite, l’ingénierie des fonctionnalités est utilisée pour apporter des modifications à votre jeu de données de vente au détail.
- Enfin, créez des modèles des données et sélectionnez le modèle le plus performant pour prédire les ventes futures.

Une fois que vous êtes prêt, début en lisant le guide [d&#39;utilisation de](./jupyterlab/overview.md) JupyterLab pour un aperçu rapide des ordinateurs portables dans Adobe Experience Platform Data Science Workspace. De plus, si vous souhaitez en savoir plus sur les modèles et les recettes, début en lisant le didacticiel sur le schéma de vente au [détail et le jeu de données](./models-recipes/create-retails-sales-dataset.md) . Ce didacticiel vous prépare à suivre les didacticiels Data Science Workspace qui peuvent être consultés dans la page [des didacticiels Data Science Workspace](../tutorials/data-science-workspace.md).