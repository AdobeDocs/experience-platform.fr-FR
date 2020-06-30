---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Présentation de Data Science Workspace
topic: Walkthrough
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 0%

---


# [!DNL Data Science Workspace] parcours

Ce document fournit une passerelle pour l&#39;Adobe Experience Platform [!DNL Data Science Workspace]. Plus précisément, nous allons passer en revue le processus général qu&#39;un chercheur en données doit suivre pour résoudre un problème à l&#39;aide de l&#39;apprentissage automatique.

## Conditions préalables

- Un compte d&#39;Adobe ID enregistré
   - Le compte d&#39;Adobe ID doit avoir été ajouté à une organisation ayant accès à l&#39;Adobe Experience Platform et au [!DNL Data Science Workspace]

## Motivation du chercheur en données

Un détaillant doit faire face à de nombreux défis pour rester compétitif sur le marché actuel. L&#39;une des principales préoccupations du détaillant est de décider du prix optimal de ses produits et de prédire les tendances de vente. Grâce à un modèle de prévision précis, le détaillant serait en mesure de trouver la relation entre les politiques de demande et de tarification et de prendre des décisions de prix optimisées pour maximiser les ventes et les recettes.

## Solution du chercheur en données

La solution d&#39;un chercheur en données consiste à exploiter la richesse des données historiques auxquelles un détaillant a accès, à prédire les tendances futures et à optimiser les décisions de tarification. Nous utiliserons les données des ventes passées pour former notre modèle d&#39;apprentissage automatique et nous utiliserons le modèle pour prédire les tendances futures des ventes. Ainsi, le détaillant pourra avoir des informations pour les aider à modifier les prix.

Dans cet aperçu, nous allons passer en revue les étapes qu&#39;un scientifique spécialiste des données doit franchir pour créer un ensemble de données et un modèle pour prédire les ventes hebdomadaires. Nous passerons en revue les sections suivantes de l&#39;exemple de carnet de vente au détail sur l&#39;Adobe Experience Platform [!DNL Data Science Workspace]:

- [Configuration](#setup)
- [Exploration des données](#exploring-data)
- [Ingénierie des fonctionnalités](#feature-engineering)
- [Formation et vérification](#training-and-verification)

### Ordinateurs portables dans [!DNL Data Science Workspace]

Tout d&#39;abord, nous voulons créer un [!DNL JupyterLab] bloc-notes pour ouvrir l&#39;exemple de bloc-notes &quot;Ventes au détail&quot;. Suivez les étapes effectuées par le data scientist dans le bloc-notes pour mieux comprendre un processus typique.

Dans l’interface utilisateur de l’Adobe Experience Platform, cliquez sur l’onglet Data Science dans le menu supérieur pour accéder au [!DNL Data Science Workspace]. A partir de cette page, cliquez sur l&#39; [!DNL JupyterLab] onglet qui va ouvrir le [!DNL JupyterLab] lanceur. Vous devriez voir une page similaire à celle-ci.

![](./images/walkthrough/jupyterlab_launcher.png)

Dans notre tutoriel, nous utiliserons [!DNL Python] 3 dans le [!DNL Jupyter Notebook] pour montrer comment accéder aux données et les explorer. Dans la page Lanceur, des exemples de cahiers sont fournis. Nous utiliserons l&#39;échantillon &quot;Ventes au détail&quot; pour [!DNL Python] 3.

![](./images/walkthrough/retail_sales.png)

### Configuration {#setup}

Avec le bloc-notes Ventes au détail ouvert, la première chose que nous faisons est de charger les bibliothèques nécessaires à notre flux de travail. La liste suivante présente brièvement les utilisations de chacun d&#39;eux :
- **numpy** - bibliothèque de calcul scientifique qui ajoute la prise en charge de grandes matrices et matrices multidimensionnelles
- **pandas** - bibliothèque qui offre les structures de données et les opérations utilisées pour la manipulation et l&#39;analyse des données
- **matplotlib.pyplot** - bibliothèque de mappage qui fournit une expérience de type MATLAB lors du mappage
- **seaborn** - bibliothèque de visualisation de données d’interface de haut niveau basée sur matplotlib
- **sklearn** - bibliothèque d’apprentissage automatique qui comprend les algorithmes de classification, de régression, de support vectoriel et de cluster
- **avertissements** - bibliothèque qui contrôle les messages d’avertissement

### Explorer les données {#exploring-data}

#### Charger les données

Une fois les bibliothèques chargées, nous pouvons début de regarder les données. Le [!DNL Python] code suivant utilise la structure de `DataFrame` données des pandas et la fonction [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) pour lire le fichier CSV hébergé sur [!DNL Github] dans le DataFrame des pandas :

![](./images/walkthrough/read_csv.png)

La structure de données DataFrame de Pandas est une structure de données à deux dimensions étiquetées. Pour voir rapidement les dimensions de nos données, nous pouvons utiliser `df.shape`. Ceci renvoie un tuple qui représente la dimension du DataFrame :

![](./images/walkthrough/df_shape.png)

Enfin, nous pouvons jeter un oeil à ce à quoi ressemblent nos données. Nous pouvons utiliser `df.head(n)` pour vue les premières `n` lignes du DataFrame :

![](./images/walkthrough/df_head.png)

#### Résumé statistique

Nous pouvons exploiter la bibliothèque [!DNL Python's] pandas pour obtenir le type de données de chaque attribut. La sortie de l&#39;appel suivant nous donnera des informations sur le nombre d&#39;entrées et le type de données pour chacune des colonnes :

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Ces informations sont utiles car connaître le type de données de chaque colonne nous permettra de savoir comment traiter les données.

Maintenant regardons le résumé statistique. Seuls les types de données numériques s’affichent de sorte que `date`, `storeType`et `isHoliday` ne soient pas générés :

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Avec cela, nous pouvons voir qu&#39;il y a 6435 instances pour chaque caractéristique. De plus, des informations statistiques telles que moyenne, écart type (std), min, max et interquartiles sont fournies. Ceci nous donne des informations sur l&#39;écart pour les données. Dans la section suivante, nous allons passer en revue la visualisation qui fonctionne avec ces informations pour nous donner une compréhension complète de nos données.

En examinant les valeurs minimale et maximale pour `store`, nous voyons qu&#39;il existe 45 magasins uniques que les données représentent. Il y a aussi `storeTypes` qui différencient ce qu&#39;est un magasin. Nous pouvons voir la distribution de `storeTypes` en procédant comme suit :

![](./images/walkthrough/df_groupby.png)

Cela signifie que 22 magasins sont de `storeType A` , 17 `storeType B`et 6 `storeType C`.

#### Visualiser les données

Maintenant que nous connaissons les valeurs de nos blocs de données, nous voulons compléter cela par des visualisations pour rendre les choses plus claires et plus faciles à identifier les schémas. Ces graphiques sont également utiles pour transmettre des résultats à une audience.

#### Graphiques univariés

Les graphiques univariés sont des tracés d’une variable individuelle. Les graphiques univariés courants utilisés pour visualiser vos données sont les tracés de boîtes et de muraille.

En utilisant notre jeu de données de vente au détail d&#39;avant, nous pouvons générer la boîte et le tracé de chuchotement pour chacun des 45 magasins et leurs ventes hebdomadaires. Le graphique est généré à l’aide de la `seaborn.boxplot` fonction.

![](./images/walkthrough/box_whisker.png)

Un tracé de boîte et de muraille est utilisé pour montrer la distribution des données. Les lignes extérieures du graphique montrent les quartiles supérieur et inférieur tandis que la boîte s&#39;étend sur la plage interquartile. La ligne dans la zone marque la médiane. Les points de données plus de 1,5 fois le quartile supérieur ou inférieur sont marqués comme un cercle. Ces points sont considérés comme des valeurs aberrantes.

Ensuite, nous pouvons tracer les ventes hebdomadaires avec le temps. Nous n&#39;afficherons que la sortie du premier magasin. Le code du bloc-notes génère 6 tracés correspondant à 6 des 45 magasins de notre jeu de données.

![](./images/walkthrough/weekly_sales.png)

Ce diagramme permet de comparer les ventes hebdomadaires sur une période de 2 ans. Il est facile de voir les pics de ventes et les schémas de creux au fil du temps.

#### Graphiques multivariés

Les tracés multivariés permettent de visualiser l’interaction entre les variables. Avec la visualisation, les chercheurs de données peuvent voir s&#39;il y a des corrélations ou des modèles entre les variables. Un graphique multivarié commun utilisé est une matrice de corrélation. Avec une matrice de corrélation, les dépendances entre plusieurs variables sont quantifiées avec le coefficient de corrélation.

En utilisant le même jeu de données de vente au détail, nous pouvons générer la matrice de corrélation.

![](./images/walkthrough/correlation_1.png)

Remarquez la diagonale de ceux qui sont au centre. Cela montre que lorsqu’une variable est comparée à elle-même, elle présente une corrélation positive complète. Une forte corrélation positive aura une magnitude proche de 1 tandis que des corrélations faibles seront plus proches de 0. Une corrélation négative est montrée avec un coefficient négatif montrant une tendance inverse.

### Ingénierie des fonctionnalités {#feature-engineering}

Dans cette section, nous apporterons des modifications à notre jeu de données de vente au détail. Nous effectuerons les opérations suivantes :

- ajouter des colonnes semaine et année
- convertir storeType en variable indicateur
- convertir isHoliday en variable numérique
- prévoir les ventes hebdomadaires de la semaine prochaine

#### Ajouter les colonnes semaine et année

Le format actuel de la date (`2010-02-05`) est difficile à différencier si les données sont pour chaque semaine. C’est pourquoi nous allons convertir la date en semaine et en année.

![](./images/walkthrough/date_to_week_year.png)

La semaine et la date sont désormais les suivantes :

![](./images/walkthrough/date_week_year.png)

#### Convertir storeType en variable indicateur

Ensuite, nous voulons convertir la colonne storeType en colonnes représentant chacune des `storeType`colonnes. Il existe 3 types de magasins (`A`, `B`, `C`), à partir desquels nous créons 3 nouvelles colonnes. La valeur définie dans chacun sera une valeur booléenne où &quot;1&quot; sera défini selon ce que `storeType` était et `0` pour les 2 autres colonnes.

![](./images/walkthrough/storeType.png)

La `storeType` colonne active sera supprimée.

#### Convertir isHoliday en type numérique

La prochaine modification consiste à remplacer la valeur booléenne par une représentation numérique. `isHoliday`

![](./images/walkthrough/isHoliday.png)


#### Prévoir les ventes hebdomadaires de la semaine prochaine

Maintenant, nous voulons ajouter les ventes hebdomadaires précédentes et futures à chacun de nos ensembles de données. Nous le faisons en compensant notre `weeklySales`action. De plus, nous calculons la `weeklySales` différence. Pour ce faire, on soustrait `weeklySales` les données de la semaine précédente `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

Puisque nous compensons les `weeklySales` données 45 jeux de données à l’avant et 45 jeux de données à l’arrière pour créer de nouvelles colonnes, les 45 premiers et derniers points de données auront des valeurs NaN. Nous pouvons supprimer ces points de notre jeu de données en utilisant la `df.dropna()` fonction qui supprime toutes les lignes qui ont des valeurs NaN.

![](./images/walkthrough/dropna.png)

Vous trouverez ci-dessous un résumé du jeu de données après les modifications :

![](./images/walkthrough/df_info_new.png)

### Formation et vérification {#training-and-verification}

Il est maintenant temps de créer des modèles de données et de sélectionner le modèle le plus performant pour prédire les ventes futures. Nous évaluerons les 5 algorithmes suivants :

- Régression linéaire
- Arborescence de décision
- Forêt aléatoire
- Augmentation du dégradé
- K Voisins

#### Diviser le jeu de données en sous-ensembles de formation et de test

Nous avons besoin d&#39;un moyen de savoir à quel point notre modèle sera capable de prédire les valeurs. Cette évaluation peut être effectuée en allouant une partie du jeu de données à utiliser comme validation et le reste comme données de formation. Puisque `weeklySalesAhead` sont les valeurs futures réelles de `weeklySales`, nous pouvons utiliser ceci pour évaluer la précision du modèle dans la prédiction de la valeur. Le fractionnement se fait comme suit :

![](./images/walkthrough/split_data.png)

Nous avons maintenant `X_train` et `y_train` pour préparer les modèles et `X_test` et `y_test` pour l&#39;évaluation ultérieure.

#### Algorithmes de contrôle des points

Dans cette section, nous déclarerons tous les algorithmes dans un tableau appelé `model`. Ensuite, nous itérons à travers ce tableau et pour chaque algorithme, nous saisissons nos données d&#39;entraînement avec `model.fit()` lesquelles crée un modèle `mdl`. En utilisant ce modèle, nous prédirons `weeklySalesAhead` avec nos `X_test` données.

![](./images/walkthrough/training_scoring.png)

Pour la notation, nous prenons la différence moyenne en pourcentage entre les valeurs prédites `weeklySalesAhead` et les valeurs réelles dans les `y_test` données. Puisque nous voulons minimiser la différence entre notre prédiction et la réalité, le régresseur d&#39;augmentation du rayonnement est le modèle le plus performant.

#### Visualiser les prédictions

Enfin, nous visualiserons notre modèle de prévision avec les valeurs de vente hebdomadaires réelles. La ligne bleue représente les chiffres réels, tandis que la ligne verte représente notre prédiction à l&#39;aide de l&#39;augmentation du dégradé. Le code suivant génère 6 tracés qui représentent 6 des 45 magasins de notre jeu de données. Seul `Store 1` :

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## Conclusion

Avec cet aperçu, nous avons passé en revue le flux de travail qu&#39;un informaticien suivrait pour résoudre un problème de vente au détail. Plus précisément, nous avons suivi les étapes suivantes pour parvenir à une solution qui prévoit des ventes hebdomadaires futures.

- [Configuration](#setup)
- [Exploration des données](#exploring-data)
- [Ingénierie des fonctionnalités](#feature-engineering)
- [Formation et vérification](#training-and-verification)