---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Présentation détaillée de Data Science Workspace
topic: Walkthrough
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 93%

---


# [!DNL Data Science Workspace] parcours

This document provides a walkthrough for Adobe Experience Platform [!DNL Data Science Workspace]. Plus précisément, nous allons passer en revue le processus général suivi par un spécialiste des données pour résoudre un problème à l’aide de l’apprentissage automatique.

## Conditions préalables

- Compte Adobe ID enregistré
   - Le compte Adobe ID doit avoir été ajouté à une organisation ayant accès à Adobe Experience Platform et à [!DNL Data Science Workspace]

## Motivation du spécialiste des données

Un détaillant doit faire face à de nombreux défis pour rester compétitif sur le marché actuel. L’une des principales préoccupations du détaillant concerne le prix optimal de ses produits et la prédiction des tendances de vente. Avec un modèle de prévision précis, le détaillant serait en mesure d’identifier la relation entre les politiques de demande et de prix, mais aussi de prendre des décisions optimisées concernant le prix afin de maximiser les ventes et le chiffre d’affaires.

## Solution du spécialiste des données

La solution du spécialiste des données consiste à exploiter la richesse des données historiques auxquelles le détaillant a accès, à prédire les tendances futures et à optimiser les décisions relatives aux prix. Nous allons utiliser des données relatives aux ventes passées pour former notre modèle d’apprentissage automatique, puis nous utiliserons le modèle pour prédire les tendances futures en matière de ventes. Ces informations utiles aideront le détaillant à modifier les prix.

Dans cette présentation, nous allons passer en revue les étapes suivies par un spécialiste des données pour utiliser un jeu de données et créer un modèle afin de prédire les ventes hebdomadaires. Nous passerons en revue les sections suivantes du notebook d’exemple « Ventes au détail » dans Adobe Experience Platform [!DNL Data Science Workspace]:

- [Configuration](#setup)
- [Exploration des données](#exploring-data)
- [Conception des fonctionnalités](#feature-engineering)
- [Formation et vérification](#training-and-verification)

### Ordinateurs portables dans [!DNL Data Science Workspace]

Firstly, we want to create a [!DNL JupyterLab] notebook to open the &quot;Retail Sales&quot; sample notebook. Suivez les étapes effectuées par le spécialiste des données dans le notebook pour mieux comprendre ce processus type.

Dans l’interface utilisateur d’Adobe Experience Platform, cliquez sur l’onglet Data Science du menu supérieur pour accéder à [!DNL Data Science Workspace]. From this page, click on the [!DNL JupyterLab] tab which will open the [!DNL JupyterLab] launcher. Vous devriez voir une page similaire à celle-ci.

![](./images/walkthrough/jupyterlab_launcher.png)

In our tutorial, we will be using [!DNL Python] 3 in the [!DNL Jupyter Notebook] to show how to access and explore the data. Sur la page du lanceur, vous trouverez des notebooks d’exemple. We will be using the &quot;Retail Sales&quot; sample for [!DNL Python] 3.

![](./images/walkthrough/retail_sales.png)

### Configuration {#setup}

Une fois le notebook « Ventes au détail » ouvert, la première chose à faire est de charger les bibliothèques requises pour notre processus. La liste suivante fournit une brève description de la fonction de chacune :
- **numpy** - Bibliothèque de calcul scientifique qui ajoute la prise en charge de tableaux et de matrices multidimensionnels volumineux
- **pandas** - Bibliothèque qui offre les structures et opérations de données utilisées dans le cadre de la manipulation et de l’analyse de données
- **matplotlib.pyplot** - Bibliothèque de représentation graphique qui fournit une expérience de type MATLAB
- **seaborn** - Bibliothèque de visualisation des données d’interface générales basée sur matplotlib
- **sklearn** - Bibliothèque d’apprentissage automatique qui comprend la classification, la régression, les vecteurs de support et les algorithmes de cluster
- **warnings** - Bibliothèque qui contrôle les messages d’avertissement

### Exploration des données {#exploring-data}

#### Chargement des données

Une fois les bibliothèques chargées, nous pouvons nous intéresser aux données. The following [!DNL Python] code uses pandas&#39; `DataFrame` data structure and the [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) function to read the CSV hosted on [!DNL Github] into the pandas DataFrame:

![](./images/walkthrough/read_csv.png)

La structure de données du DataFrame de pandas est une structure de données étiquetées en deux dimensions. Pour voir rapidement les dimensions de nos données, nous pouvons utiliser `df.shape`. Cette opération renvoie un tuple qui représente les dimensions du DataFrame :

![](./images/walkthrough/df_shape.png)

Enfin, nous pouvons avoir un aperçu de l’apparence de nos données. Nous pouvons utiliser `df.head(n)` pour voir les `n` premières lignes du DataFrame :

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

Grâce à cela, nous pouvons voir qu’il existe 6 435 instances pour chaque caractéristique. Nous obtenons également des informations statistiques, telles que la moyenne, l’écart type, le minimum, le maximum et les plages interquartiles. Cela nous permet d’identifier les variations de données. Dans la section suivante, nous allons passer en revue la visualisation qui accompagne ces informations, afin d’avoir une compréhension complète de nos données.

En examinant les valeurs minimale et maximale pour `store`, nous voyons que les données représentent 45 boutiques uniques. Les `storeTypes` permettent également de différencier les boutiques. Nous pouvons voir la distribution des `storeTypes` en procédant comme suit :

![](./images/walkthrough/df_groupby.png)

Ici, nous avons 22 boutiques `storeType A`, 17 boutiques `storeType B` et 6 boutiques `storeType C`.

#### Visualisation des données

Maintenant que nous connaissons les valeurs de notre DataFrame, nous voulons les compléter par des visualisations, afin de rendre les choses plus claires et d’identifier plus facilement les motifs. Ces graphiques servent également à transmettre les résultats à une audience.

#### Graphiques unidimensionnels

Les graphiques unidimensionnels sont des tracés représentant une seule variable. La boîte à moustaches est un graphique unidimensionnel couramment utilisé pour visualiser les données.

En utilisant le même jeu de données relatif aux ventes, nous pouvons générer un graphique de boîte à moustaches pour chacune des 45 boutiques et leurs ventes hebdomadaires. Le graphique est généré à l’aide de la fonction `seaborn.boxplot`.

![](./images/walkthrough/box_whisker.png)

Un graphique de boîte à moustaches sert à illustrer la distribution des données. Les lignes extérieures du graphique représentent les quartiles supérieur et inférieur, tandis que la boîte s’étend sur la plage interquartile. La ligne dans la zone indique la médiane. Tout point de données plus de 1,5 fois supérieur ou inférieur au quartile est marqué sous forme de cercle. Ces points sont considérés comme des valeurs aberrantes.

Ensuite, nous pouvons tracer les ventes hebdomadaires dans le temps. Nous n’afficherons que la sortie de la première boutique. Le code du notebook génère 6 tracés correspondant à 6 des 45 boutiques de notre jeu de données.

![](./images/walkthrough/weekly_sales.png)

Ce diagramme permet de comparer les ventes hebdomadaires sur une période de 2 ans. Nous pouvons facilement repérer les motifs des pics et des creux de ventes au fil du temps.

#### Graphiques multidimensionnels

Les graphiques multidimensionnels servent à visualiser les interactions entre les variables. Grâce à cette visualisation, les spécialistes des données peuvent vérifier s’il existe des corrélations ou des motifs entre les variables. La matrice de corrélation est un graphique multidimensionnel couramment utilisé. Avec une matrice de corrélation, les dépendances entre les différentes variables sont quantifiées à l’aide d’un coefficient de corrélation.

En utilisant le même jeu de données relatif aux ventes, nous pouvons générer la matrice de corrélation.

![](./images/walkthrough/correlation_1.png)

Notez la diagonale de 1 au centre. Elle indique que lorsqu’une variable est comparée à elle-même, elle présente une corrélation positive entière. Une corrélation positive élevée aura une magnitude proche de 1, tandis que les corrélations faibles seront plus proches de 0. Une corrélation négative s’affiche sous la forme d’un coefficient négatif, indiquant une tendance inverse.

### Conception des fonctionnalités {#feature-engineering}

Dans cette section, nous allons apporter des modifications à notre jeu de données relatif aux ventes. Nous allons effectuer les opérations suivantes :

- Ajout de colonnes pour la semaine et l’année
- Conversion de storeType en variable indicatrice
- Conversion d’isHoliday en variable numérique
- Prévision des ventes hebdomadaires de la semaine prochaine

#### Ajout de colonnes pour la semaine et l’année

Avec le format de date actuel (`2010-02-05`), il est difficile d’identifier les semaines. Nous allons convertir la date en semaine et en année.

![](./images/walkthrough/date_to_week_year.png)

À présent, la semaine et la date s’affichent comme suit :

![](./images/walkthrough/date_week_year.png)

#### Conversion de storeType en variable indicatrice

Maintenant, nous voulons convertir la colonne storeType en colonnes représentant chaque `storeType`. Il existe 3 types de boutique (`A`, `B` et `C`), à partir desquels nous allons créer 3 autres colonnes. La valeur de chaque colonne sera une valeur booléenne, à savoir un 1 dans la colonne correspondant au `storeType` et des `0` dans les 2 autres colonnes.

![](./images/walkthrough/storeType.png)

La colonne `storeType` actuelle sera supprimée.

#### Conversion d’isHoliday en type numérique

La modification suivante consiste à remplacer la valeur booléenne `isHoliday` par une représentation numérique.

![](./images/walkthrough/isHoliday.png)


#### Prévision des ventes hebdomadaires de la semaine prochaine

Nous voulons maintenant ajouter les ventes hebdomadaires précédentes et futures à chacun de nos jeux de données. Pour ce faire, nous allons décaler nos `weeklySales`. Nous allons également calculer la différence entre les `weeklySales`. Pour cela, il faut soustraire les `weeklySales` aux `weeklySales` de la semaine précédente.

![](./images/walkthrough/weekly_past_future.png)

Puisque nous décalons les données `weeklySales` de 45 jeux de données vers l’avant et de 45 jeux de données vers l’arrière pour créer des colonnes, les 45 premiers et derniers points de données auront des valeurs NaN. Nous pouvons supprimer ces points de notre jeu de données en utilisant la fonction `df.dropna()` qui supprime toutes les lignes comportant des valeurs NaN.

![](./images/walkthrough/dropna.png)

Vous trouverez ci-dessous un résumé du jeu de données après modification :

![](./images/walkthrough/df_info_new.png)

### Formation et vérification {#training-and-verification}

Il est maintenant temps de créer quelques modèles de données et de sélectionner le modèle qui sera le plus performant pour prédire les ventes futures. Nous allons évaluer les 5 algorithmes suivants :

- Régression linéaire
- Arborescence de décision
- Forêt aléatoire
- Amplification progressive
- Méthode des k plus proches voisins

#### Scission du jeu de données en sous-ensembles de formation et de test

Nous avons besoin de déterminer la précision avec laquelle notre modèle sera capable de prédire les valeurs. Cette évaluation peut être effectuée en allouant une partie du jeu de données comme données de validation, et le reste comme données de formation. Puisque `weeklySalesAhead` représente les futures valeurs réelles des `weeklySales`, nous pouvons l’utiliser pour évaluer la précision du modèle dans la prédiction de la valeur. La scission se fait comme suit :

![](./images/walkthrough/split_data.png)

Nous avons maintenant `X_train` et `y_train` pour préparer les modèles, ainsi que `X_test` et `y_test` pour l’évaluation ultérieure.

#### Contrôle des algorithmes

Dans cette section, nous allons déclarer tous les algorithmes dans un tableau appelé `model`. Ensuite, nous allons itérer par le biais de ce tableau et, pour chaque algorithme, saisir nos données de formation avec `model.fit()`, qui crée un modèle `mdl`. Grâce à ce modèle, nous pourrons prédire `weeklySalesAhead` avec nos données `X_test`.

![](./images/walkthrough/training_scoring.png)

Pour le score, nous prenons la différence moyenne en pourcentage entre les valeurs `weeklySalesAhead` prédites et les valeurs `y_test` réelles. Puisque nous voulons minimiser la différence entre notre prédiction et la réalité, la variable libre d’amplification progressive est le modèle le plus performant.

#### Visualisation des prédictions

Enfin, nous allons visualiser notre modèle de prédiction avec les valeurs réelles des ventes hebdomadaires. La ligne bleue représente les chiffres réels, tandis que la ligne verte représente notre prévision à l’aide de l’amplification progressive. Le code suivant génère 6 tracés qui représentent 6 des 45 boutiques de notre jeu de données. Seule la boutique `Store 1` est illustrée ici :

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## Conclusion

Dans cette présentation, nous avons passé en revue le processus suivi par un spécialiste des données pour résoudre un problème relatif aux ventes au détail. Plus précisément, nous avons suivi ces étapes pour fournir une solution qui prévoit les ventes hebdomadaires futures :

- [Configuration](#setup)
- [Exploration des données](#exploring-data)
- [Conception des fonctionnalités](#feature-engineering)
- [Formation et vérification](#training-and-verification)