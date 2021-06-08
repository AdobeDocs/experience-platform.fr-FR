---
keywords: Experience Platform;présentation;Data Science Workspace;rubriques les plus consultées
solution: Experience Platform
title: Présentation de Data Science Workspace
topic-legacy: Walkthrough
description: Ce document fournit une présentation détaillée d’Adobe Experience Platform Data Science Workspace. Plus précisément, le workflow général qu’un spécialiste des données doit suivre pour résoudre un problème à l’aide de l’apprentissage automatique.
exl-id: d814846e-52a9-46c6-831a-3399241959f2
source-git-commit: 7d98340e7949aadc744513415c4fc7469efd2403
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 33%

---

# [!DNL Data Science Workspace] walkthrough

Ce document fournit une présentation détaillée de Adobe Experience Platform [!DNL Data Science Workspace]. Ce tutoriel décrit un workflow général du spécialiste des données et la manière dont il peut aborder et résoudre un problème à l’aide de l’apprentissage automatique.

## Conditions préalables

- Compte Adobe ID enregistré
   - Le compte Adobe ID doit avoir été ajouté à une organisation ayant accès à Adobe Experience Platform et [!DNL Data Science Workspace].

## Cas pratique de vente au détail

Un détaillant doit faire face à de nombreux défis pour rester compétitif sur le marché actuel. L’une des principales préoccupations du détaillant est de décider du prix optimal d’un produit et de prédire les tendances de vente. Grâce à un modèle de prédiction précis, un détaillant serait en mesure de trouver la relation entre les politiques de demande et de prix et de prendre des décisions de tarification optimisées pour maximiser les ventes et les recettes.

## Solution du spécialiste des données

La solution d’un spécialiste des données consiste à exploiter la richesse des informations historiques fournies par un détaillant, à prédire les tendances futures et à optimiser les décisions de tarification. Cette présentation utilise les données de ventes antérieures pour former un modèle d’apprentissage automatique et utilise le modèle pour prédire les tendances de vente futures. Vous pouvez ainsi générer des informations pour vous aider à apporter des modifications optimales aux prix.

Cet aperçu reflète les étapes qu’un spécialiste des données doit suivre pour créer un jeu de données et un modèle pour prédire les ventes hebdomadaires. Ce tutoriel couvre les sections suivantes du notebook Exemple de vente au détail sur Adobe Experience Platform [!DNL Data Science Workspace] :

- [Configuration](#setup)
- [Exploration des données](#exploring-data)
- [Conception des fonctionnalités](#feature-engineering)
- [Formation et vérification](#training-and-verification)

### Notebooks dans [!DNL Data Science Workspace]

Dans l’interface utilisateur de Adobe Experience Platform, sélectionnez **[!UICONTROL Notebooks]** dans l’onglet **[!UICONTROL Data Science]** pour accéder à la page d’aperçu [!UICONTROL Notebooks]. Sur cette page, sélectionnez l’onglet [!DNL JupyterLab] pour lancer votre environnement [!DNL JupyterLab]. La page d’entrée par défaut pour [!DNL JupyterLab] est le **[!UICONTROL lanceur]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

Ce tutoriel utilise [!DNL Python] 3 dans [!DNL JupyterLab Notebooks] pour montrer comment accéder aux données et les explorer. Sur la page du lanceur, vous trouverez des notebooks d’exemple. L’exemple de notebook **[!UICONTROL Ventes au détail]** est utilisé dans les exemples fournis ci-dessous.

### Configuration {#setup}

Une fois le notebook Ventes au détail ouvert, la première chose à faire est de charger les bibliothèques requises pour votre workflow. La liste suivante décrit brièvement chacune des bibliothèques utilisées dans les exemples dans les étapes suivantes.

- **numpy** : Bibliothèque de calcul scientifique qui ajoute la prise en charge de tableaux et de matrices multidimensionnels volumineux
- **pandas** : Bibliothèque proposant des structures et des opérations de données utilisées pour la manipulation et l’analyse des données
- **matplotlib.pyplot** : Bibliothèque de mappage qui fournit une expérience de type MATLAB lors du mappage
- **seaborn**  : Bibliothèque de visualisation des données d’interface de haut niveau basée sur matplotlib
- **sklearn** : Bibliothèque d’apprentissage automatique qui comprend la classification, la régression, les vecteurs de prise en charge et les algorithmes de cluster
- **avertissement** : Bibliothèque qui contrôle les messages d’avertissement

### Exploration des données {#exploring-data}

#### Chargement des données

Une fois les bibliothèques chargées, vous pouvez commencer à consulter les données. Le code [!DNL Python] suivant utilise la structure de données `DataFrame` de pandas et la fonction [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) pour lire le fichier CSV hébergé sur [!DNL Github] dans le DataFrame de pandas :

![](./images/walkthrough/read_csv.png)

La structure de données du DataFrame de pandas est une structure de données étiquetées en deux dimensions. Pour voir rapidement les dimensions de vos données, vous pouvez utiliser `df.shape`. Cette opération renvoie un tuple qui représente les dimensions du DataFrame :

![](./images/walkthrough/df_shape.png)

Enfin, vous pouvez prévisualiser vos données. Vous pouvez utiliser `df.head(n)` pour afficher les premières lignes `n` du DataFrame :

![](./images/walkthrough/df_head.png)

#### Résumé statistique

Nous pouvons tirer parti de la bibliothèque [!DNL Python's] pandas pour obtenir le type de données de chaque attribut. La sortie de l’appel suivant nous donnera des informations sur le nombre d’entrées et le type de données pour chacune des colonnes :

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

Vous pouvez ainsi constater qu’il existe 6 435 instances pour chaque caractéristique. Nous obtenons également des informations statistiques, telles que la moyenne, l’écart type, le minimum, le maximum et les plages interquartiles. Cela nous permet d’identifier les variations de données. Dans la section suivante, vous allez passer en revue la visualisation qui accompagne ces informations pour nous donner une compréhension complète de vos données.

En examinant les valeurs minimale et maximale pour `store`, vous pouvez voir qu’il existe 45 boutiques uniques que les données représentent. Les `storeTypes` permettent également de différencier les boutiques. vous pouvez voir la distribution de `storeTypes` en procédant comme suit :

![](./images/walkthrough/df_groupby.png)

Ici, nous avons 22 boutiques `storeType A`, 17 boutiques `storeType B` et 6 boutiques `storeType C`.

#### Visualisation des données

Maintenant que vous connaissez les valeurs de votre cadre de données, vous souhaitez les compléter par des visualisations afin de rendre les choses plus claires et d’identifier plus facilement les motifs. Ces graphiques servent également à transmettre les résultats à une audience.

#### Graphiques unidimensionnels

Les graphiques unidimensionnels sont des tracés représentant une seule variable. La boîte à moustaches est un graphique unidimensionnel couramment utilisé pour visualiser les données.

En utilisant votre jeu de données de vente au détail d’avant, vous pouvez générer le graphique de boîte et de whisky pour chacun des 45 magasins et leurs ventes hebdomadaires. Le graphique est généré à l’aide de la fonction `seaborn.boxplot`.

![](./images/walkthrough/box_whisker.png)

Un graphique de boîte à moustaches sert à illustrer la distribution des données. Les lignes extérieures du graphique représentent les quartiles supérieur et inférieur, tandis que la boîte s’étend sur la plage interquartile. La ligne dans la zone indique la médiane. Tout point de données plus de 1,5 fois supérieur ou inférieur au quartile est marqué sous forme de cercle. Ces points sont considérés comme des valeurs aberrantes.

Vous pouvez ensuite tracer les ventes hebdomadaires avec le temps. Vous n’afficherez que la sortie de la première boutique. Le code du notebook génère 6 tracés correspondant à 6 des 45 boutiques de notre jeu de données.

![](./images/walkthrough/weekly_sales.png)

Ce diagramme permet de comparer les ventes hebdomadaires sur une période de 2 ans. Nous pouvons facilement repérer les motifs des pics et des creux de ventes au fil du temps.

#### Graphiques multidimensionnels

Les graphiques multidimensionnels servent à visualiser les interactions entre les variables. Grâce à cette visualisation, les spécialistes des données peuvent vérifier s’il existe des corrélations ou des motifs entre les variables. La matrice de corrélation est un graphique multidimensionnel couramment utilisé. Avec une matrice de corrélation, les dépendances entre les différentes variables sont quantifiées à l’aide d’un coefficient de corrélation.

En utilisant le même jeu de données relatif aux ventes, vous pouvez générer la matrice de corrélation.

![](./images/walkthrough/correlation_1.png)

Notez la diagonale de 1 au centre. Elle indique que lorsqu’une variable est comparée à elle-même, elle présente une corrélation positive entière. Une corrélation positive élevée aura une magnitude proche de 1, tandis que les corrélations faibles seront plus proches de 0. Une corrélation négative s’affiche sous la forme d’un coefficient négatif, indiquant une tendance inverse.

### Conception des fonctionnalités {#feature-engineering}

Dans cette section, la conception des fonctionnalités est utilisée pour apporter des modifications à votre jeu de données de vente au détail en effectuant les opérations suivantes :

- Ajout de colonnes pour la semaine et l’année
- Conversion de storeType en variable indicatrice
- Convertir isHoliday en variable numérique
- Prévision des ventes hebdomadaires de la semaine prochaine

#### Ajout de colonnes pour la semaine et l’année

Le format actuel de la date (`2010-02-05`) peut rendre difficile la différenciation des données pour chaque semaine. Pour cette raison, vous devez convertir la date en semaine et en année.

![](./images/walkthrough/date_to_week_year.png)

À présent, la semaine et la date s’affichent comme suit :

![](./images/walkthrough/date_week_year.png)

#### Conversion de storeType en variable indicatrice

Ensuite, vous souhaitez convertir la colonne storeType en colonnes représentant chaque `storeType`. Il existe trois types de magasin (`A`, `B`, `C`), à partir desquels vous créez 3 nouvelles colonnes. La valeur définie dans chaque colonne est une valeur booléenne où &quot;1&quot; est défini en fonction de ce que sont `storeType` et `0` pour les 2 autres colonnes.

![](./images/walkthrough/storeType.png)

La colonne `storeType` actuelle est supprimée.

#### Conversion d’isHoliday en type numérique

La modification suivante consiste à remplacer la valeur booléenne `isHoliday` par une représentation numérique.

![](./images/walkthrough/isHoliday.png)

#### Prévision des ventes hebdomadaires de la semaine prochaine

Vous souhaitez maintenant ajouter les ventes hebdomadaires précédentes et futures à chacun de vos jeux de données. Vous pouvez le faire en décalant votre `weeklySales`. En outre, la différence `weeklySales` est calculée. Pour cela, il faut soustraire les `weeklySales` aux `weeklySales` de la semaine précédente.

![](./images/walkthrough/weekly_past_future.png)

Puisque vous décalez les `weeklySales` données de 45 jeux de données vers l’avant et de 45 jeux de données vers l’arrière pour créer de nouvelles colonnes, les 45 premiers et derniers points de données ont des valeurs NaN. Vous pouvez supprimer ces points de votre jeu de données à l’aide de la fonction `df.dropna()` qui supprime toutes les lignes comportant des valeurs NaN.

![](./images/walkthrough/dropna.png)

Vous trouverez ci-dessous un résumé du jeu de données après vos modifications :

![](./images/walkthrough/df_info_new.png)

### Formation et vérification {#training-and-verification}

Il est maintenant temps de créer quelques modèles de données et de sélectionner le modèle qui sera le plus performant pour prédire les ventes futures. Vous allez évaluer les 5 algorithmes suivants :

- Régression linéaire
- Arborescence de décision
- Forêt aléatoire
- Amplification progressive
- Méthode des k plus proches voisins

#### Scission du jeu de données en sous-ensembles de formation et de test

Vous avez besoin d’un moyen de savoir à quel point votre modèle sera capable de prédire les valeurs. Cette évaluation peut être effectuée en allouant une partie du jeu de données comme données de validation, et le reste comme données de formation. Comme `weeklySalesAhead` correspond aux valeurs futures réelles de `weeklySales`, vous pouvez l’utiliser pour évaluer la précision du modèle dans la prédiction de la valeur. La scission se fait comme suit :

![](./images/walkthrough/split_data.png)

Vous disposez désormais de `X_train` et `y_train` pour la préparation des modèles et de `X_test` et `y_test` pour l’évaluation ultérieure.

#### Contrôle des algorithmes

Dans cette section, vous déclarez tous les algorithmes dans un tableau appelé `model`. Ensuite, vous effectuez une itération sur ce tableau et, pour chaque algorithme, saisissez vos données d’apprentissage avec `model.fit()` qui crée un modèle `mdl`. Grâce à ce modèle, vous pouvez prédire `weeklySalesAhead` avec vos données `X_test`.

![](./images/walkthrough/training_scoring.png)

Pour la notation, vous prenez la différence moyenne en pourcentage entre la valeur `weeklySalesAhead` prédite et les valeurs réelles dans les données `y_test`. Puisque vous souhaitez minimiser la différence entre votre prédiction et le résultat réel, le dégradé de amplification est le modèle le plus performant.

#### Visualisation des prédictions

Enfin, vous visualisez votre modèle de prédiction avec les valeurs réelles des ventes hebdomadaires. La ligne bleue représente les chiffres réels, tandis que la ligne verte représente votre prévision à l’aide de l’amplification progressive. Le code suivant génère 6 tracés qui représentent 6 des 45 boutiques de votre jeu de données. Seule la boutique `Store 1` est illustrée ici :

![](./images/walkthrough/visualize_prediction.png)

## Étapes suivantes

Ce document couvrait un processus de spécialiste des données général pour résoudre un problème de vente au détail. Pour résumer :

- Chargez les bibliothèques requises pour votre workflow.
- Une fois les bibliothèques chargées, vous pouvez commencer à consulter les données à l’aide de résumés statistiques, de visualisations et de graphiques.
- Ensuite, la conception des fonctionnalités est utilisée pour apporter des modifications à votre jeu de données relatif aux ventes.
- Enfin, créez des modèles de données et sélectionnez le modèle le plus performant pour prédire les ventes futures.

Une fois que vous êtes prêt, commencez par lire le [guide d’utilisation de JupyterLab](./jupyterlab/overview.md) pour un aperçu rapide des notebooks dans Adobe Experience Platform Data Science Workspace. De plus, si vous souhaitez en savoir plus sur les modèles et les recettes, commencez par lire le tutoriel [Schéma de ventes au détail et jeu de données](./models-recipes/create-retails-sales-dataset.md) .
