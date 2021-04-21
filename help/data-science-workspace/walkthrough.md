---
keywords: Experience Platform ; présentation ; Espace de travail des sciences de données ; sujets populaires
solution: Experience Platform
title: Présentation de l'espace de travail Data Science
topic-legacy: Walkthrough
description: Ce document fournit une présentation détaillée d’Adobe Experience Platform Data Science Workspace. Plus précisément, le processus général par lequel un chercheur de données doit résoudre un problème à l’aide de l’apprentissage automatique.
exl-id: d814846e-52a9-46c6-831a-3399241959f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 33%

---

# [!DNL Data Science Workspace] parcours

Ce document fournit une procédure pas à pas pour Adobe Experience Platform [!DNL Data Science Workspace]. Ce didacticiel présente un flux de travail général des chercheurs en données et explique comment ils peuvent aborder et résoudre un problème à l’aide de l’apprentissage automatique.

## Conditions préalables

- Compte Adobe ID enregistré
   - Le compte Adobe ID doit avoir été ajouté à une organisation ayant accès à Adobe Experience Platform et [!DNL Data Science Workspace].

## Cas d’utilisation au détail

Un détaillant doit faire face à de nombreux défis pour rester compétitif sur le marché actuel. L&#39;une des principales préoccupations du détaillant est de décider du prix optimal d&#39;un produit et de prévoir les tendances de vente. Grâce à un modèle de prévision précis, un détaillant serait en mesure de trouver la relation entre les politiques de demande et de tarification et de prendre des décisions de prix optimisées pour maximiser les ventes et les recettes.

## Solution du spécialiste des données

La solution d&#39;un chercheur en données consiste à exploiter la richesse des informations historiques fournies par un détaillant, à prédire les tendances futures et à optimiser les décisions de prix. Cette procédure pas à pas utilise les données des ventes passées pour former un modèle d&#39;apprentissage automatique et utilise ce modèle pour prédire les tendances futures des ventes. Ainsi, vous pouvez générer des informations pour vous aider à apporter des modifications de tarification optimales.

Cet aperçu reflète les étapes qu&#39;un chercheur de données suivrait pour créer un jeu de données et un modèle pour prédire les ventes hebdomadaires. Ce didacticiel couvre les sections suivantes de l&#39;exemple de carnet de vente au détail sur Adobe Experience Platform [!DNL Data Science Workspace] :

- [Configuration](#setup)
- [Exploration des données](#exploring-data)
- [Conception des fonctionnalités](#feature-engineering)
- [Formation et vérification](#training-and-verification)

### Ordinateurs portables dans [!DNL Data Science Workspace]

Dans l’interface utilisateur de Adobe Experience Platform, sélectionnez **[!UICONTROL Ordinateurs portables]** dans l’onglet **[!UICONTROL Data Science]** pour accéder à la page de présentation [!UICONTROL Notebooks]. Dans cette page, sélectionnez l&#39;onglet [!DNL JupyterLab] pour lancer votre environnement [!DNL JupyterLab]. Le landing page par défaut de [!DNL JupyterLab] est **[!UICONTROL Launcher]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

Ce didacticiel utilise [!DNL Python] 3 in [!DNL JupyterLab Notebooks] pour montrer comment accéder aux données et les explorer. Sur la page du lanceur, vous trouverez des notebooks d’exemple. L&#39;exemple de carnet de notes **[!UICONTROL Ventes au détail]** est utilisé dans les exemples fournis ci-dessous.

### Configuration {#setup}

Avec le bloc-notes Ventes au détail ouvert, la première chose à faire est de charger les bibliothèques requises pour votre flux de travail. La liste suivante décrit brièvement chacune des bibliothèques utilisées dans les exemples dans les étapes suivantes.

- **insensible** : Bibliothèque informatique scientifique qui ajoute la prise en charge de grandes matrices et matrices multidimensionnelles
- **pandas** : Bibliothèque qui offre les structures de données et les opérations utilisées pour la manipulation et l’analyse des données
- **matplotlib.pyplot** : Chargement d’une bibliothèque fournissant une expérience de type MATLAB lors du mappage
- **seaborn**  : Bibliothèque de visualisation de données d’interface de haut niveau basée sur matplotlib
- **sklearn** : Bibliothèque d’apprentissage automatique qui comprend des algorithmes de classification, de régression, de vecteur de prise en charge et de cluster
- **avertissements** : Bibliothèque qui contrôle les messages d’avertissement

### Exploration des données {#exploring-data}

#### Chargement des données

Une fois les bibliothèques chargées, vous pouvez début d’examiner les données. Le code [!DNL Python] suivant utilise la structure de données `DataFrame` des pandas et la fonction [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) pour lire le fichier CSV hébergé sur [!DNL Github] dans le DataFrame des pandas :

![](./images/walkthrough/read_csv.png)

La structure de données du DataFrame de pandas est une structure de données étiquetées en deux dimensions. Pour voir rapidement les dimensions de vos données, vous pouvez utiliser `df.shape`. Cette opération renvoie un tuple qui représente les dimensions du DataFrame :

![](./images/walkthrough/df_shape.png)

Enfin, vous pouvez prévisualisation à quoi ressemblent vos données. Vous pouvez utiliser `df.head(n)` pour vue des premières lignes `n` du DataFrame :

![](./images/walkthrough/df_head.png)

#### Résumé statistique

Nous pouvons exploiter la bibliothèque [!DNL Python's] pandas pour obtenir le type de données de chaque attribut. La sortie de l’appel suivant nous donnera des informations sur le nombre d’entrées et le type de données pour chacune des colonnes :

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

En examinant les valeurs minimale et maximale pour `store`, vous pouvez constater qu’il existe 45 magasins uniques que les données représentent. Les `storeTypes` permettent également de différencier les boutiques. vous pouvez voir la distribution de `storeTypes` en procédant comme suit :

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

Le format actuel de la date (`2010-02-05`) peut rendre difficile la différenciation des données pour chaque semaine. Pour cette raison, vous devez convertir la date en semaine et année.

![](./images/walkthrough/date_to_week_year.png)

À présent, la semaine et la date s’affichent comme suit :

![](./images/walkthrough/date_week_year.png)

#### Conversion de storeType en variable indicatrice

Ensuite, vous souhaitez convertir la colonne storeType en colonnes représentant chacune des colonnes `storeType`. Il existe 3 types de magasin (`A`, `B`, `C`), à partir desquels vous créez 3 nouvelles colonnes. La valeur définie dans chacun est une valeur booléenne où &quot;1&quot; est défini selon ce que `storeType` était et `0` pour les 2 autres colonnes.

![](./images/walkthrough/storeType.png)

La colonne `storeType` actuelle est supprimée.

#### Conversion d’isHoliday en type numérique

La modification suivante consiste à remplacer la valeur booléenne `isHoliday` par une représentation numérique.

![](./images/walkthrough/isHoliday.png)

#### Prévision des ventes hebdomadaires de la semaine prochaine

Vous souhaitez maintenant ajouter des ventes hebdomadaires précédentes et futures à chacun de vos jeux de données. Vous pouvez le faire en compensant votre `weeklySales`. De plus, la différence `weeklySales` est calculée. Pour cela, il faut soustraire les `weeklySales` aux `weeklySales` de la semaine précédente.

![](./images/walkthrough/weekly_past_future.png)

Puisque vous compliquez les jeux de données `weeklySales` 45 à l’avant et les jeux de données 45 à l’arrière pour créer de nouvelles colonnes, les 45 premiers et derniers points de données ont des valeurs NaN. Vous pouvez supprimer ces points de votre jeu de données en utilisant la fonction `df.dropna()` qui supprime toutes les lignes qui ont des valeurs NaN.

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

Vous avez besoin d’un moyen de savoir à quel point votre modèle sera capable de prédire les valeurs. Cette évaluation peut être effectuée en allouant une partie du jeu de données comme données de validation, et le reste comme données de formation. Puisque `weeklySalesAhead` correspond aux valeurs futures réelles de `weeklySales`, vous pouvez l&#39;utiliser pour évaluer la précision du modèle dans la prévision de la valeur. La scission se fait comme suit :

![](./images/walkthrough/split_data.png)

Vous avez maintenant `X_train` et `y_train` pour préparer les modèles et `X_test` et `y_test` pour évaluation ultérieure.

#### Contrôle des algorithmes

Dans cette section, vous déclarez tous les algorithmes dans un tableau appelé `model`. Ensuite, vous effectuez une itération dans ce tableau et, pour chaque algorithme, vous devez saisir vos données d&#39;identification avec `model.fit()` qui crée un modèle `mdl`. Grâce à ce modèle, vous pouvez prédire `weeklySalesAhead` avec vos données `X_test`.

![](./images/walkthrough/training_scoring.png)

Pour le score, vous prenez la différence moyenne en pourcentage entre les `weeklySalesAhead` prédites et les valeurs réelles dans les données `y_test`. Puisque vous souhaitez minimiser la différence entre votre prévision et le résultat réel, le régresseur d’augmentation du rayonnement est le modèle le plus performant.

#### Visualisation des prédictions

Enfin, vous visualisez votre modèle de prévision avec les valeurs de vente hebdomadaires réelles. La ligne bleue représente les chiffres réels, tandis que la ligne verte représente votre prévision à l’aide de l’augmentation du dégradé. Le code suivant génère 6 tracés qui représentent 6 des 45 magasins de votre jeu de données. Seule la boutique `Store 1` est illustrée ici :

![](./images/walkthrough/visualize_prediction.png)

## Étapes suivantes

Ce document couvrait un processus général de data scientist pour résoudre un problème de vente au détail. Pour résumer :

- Chargez les bibliothèques requises pour votre flux de travail.
- Une fois les bibliothèques chargées, vous pouvez début d’examiner les données à l’aide de résumés statistiques, de visualisations et de graphiques.
- Ensuite, l’ingénierie des fonctionnalités est utilisée pour apporter des modifications à votre jeu de données de vente au détail.
- Enfin, créez des modèles des données et sélectionnez le modèle le plus performant pour prédire les ventes futures.

Une fois que vous êtes prêt, début en lisant le [Guide d&#39;utilisation de JupyterLab](./jupyterlab/overview.md) pour un aperçu rapide des blocs-notes dans Adobe Experience Platform Data Science Workspace. De plus, si vous souhaitez en savoir plus sur les modèles et les recettes, début en lisant le [tutoriel sur le schéma de vente au détail et le jeu de données](./models-recipes/create-retails-sales-dataset.md). Ce didacticiel vous prépare à suivre les didacticiels Data Science Workspace qui peuvent être consultés dans la [page des didacticiels Data Science Workspace](../tutorials/data-science-workspace.md).
