---
title: Extension SQL d’ingénierie des fonctionnalités
description: Découvrez l’extension SQL d’ingénierie des fonctionnalités de Data Distiller pour prétraiter les données en vue d’une modélisation statistique avancée. Il couvre les techniques disponibles d’extraction, de transformation et de sélection des fonctionnalités.
role: Developer
exl-id: 622c8ef3-9651-46b3-ad22-021a93190149
source-git-commit: e4ee4accdb28dafda7e37625eb84062bb6e53644
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# Extension SQL d’ingénierie de fonctionnalités

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Distiller de données. Pour plus d’informations, contactez votre représentant ou représentante Adobe.

Pour répondre à vos besoins d’ingénierie des fonctionnalités, utilisez l’extension de transformateur SQL afin de simplifier et d’automatiser le prétraitement de vos données. Utilisez cette extension pour créer des fonctionnalités et profiter d’une expérimentation transparente avec différentes techniques d’ingénierie des fonctionnalités, y compris en les associant à des modèles. Conçu pour l’informatique distribuée, vous pouvez réaliser l’ingénierie de fonctionnalités sur de grands jeux de données de manière parallèle et évolutive, ce qui réduit considérablement le temps nécessaire au prétraitement des données avec l’extension SQL d’ingénierie de fonctionnalités de Distiller de données.

## Présentation de la technique {#technique-overview}

Les fonctionnalités d’ingénierie des fonctionnalités couvrent trois domaines principaux : extraction de fonctionnalités, transformation de fonctionnalités et sélection de fonctionnalités. Chaque zone comprend des fonctions spécifiques conçues pour extraire, convertir, cibler et améliorer votre prétraitement des données.

### Extraction des fonctionnalités {#feature-extraction}

Extrayez des informations pertinentes à partir de vos données, en particulier des données textuelles, et convertissez-les dans un format numérique que les modèles pris en charge peuvent utiliser ou transformer et dériver des jeux de données. Utilisez les fonctions suivantes pour effectuer l’extraction de fonctionnalités :

- **[Transformateur textuel](./feature-transformation.md#textual-transformations)** : permet de convertir des données textuelles en fonctions numériques.
- **[Vectoriseur de nombre](./feature-transformation.md#countvectorizer)** : transforme une collection de documents texte en vecteurs de nombre de jetons.
- **[N-gramme](./feature-transformation.md#ngram)** : Génère des séquences de n-grammes à partir de données texte.
- **[Suppression de mots vides](./feature-transformation.md#stopwordsremover)** : filtrez les mots courants qui n’ont pas de signification significative.
- **[TF-IDF](./feature-transformation.md#tf-idf)** : mesure l&#39;importance des mots dans un document par rapport à un corpus.
- **[Tokenizer](./feature-transformation.md#tokenizer)** : ventiler le texte en termes individuels (mots).
- **[Word2Vec](./feature-transformation.md#word2vec)** : mappez des mots à des vecteurs de taille fixe et créez des incorporations de mots.

### Transformation de caractéristiques {#feature-transformation}

En plus d’extraire des fonctionnalités, utilisez les transformateurs généraux suivants pour préparer vos fonctionnalités aux modèles statistiques avancés et aux jeux de données dérivés. Appliquez une mise à l’échelle, une normalisation ou un codage pour vous assurer que vos fonctionnalités sont à la même échelle et ont une distribution similaire.

#### Transformateurs généraux

Vous trouverez ci-dessous une liste d’outils permettant de traiter un large éventail de types de données afin d’améliorer votre workflow de prétraitement des données.

- **[Imputation numérique](./feature-transformation.md#numeric-imputer)** : remplissez les valeurs manquantes dans les colonnes numériques avec une valeur spécifiée, telle que la moyenne ou la médiane.
- **[Imputeur de chaîne](./feature-transformation.md#string-imputer)** : remplacez les valeurs de chaîne manquantes par une valeur spécifiée, par exemple la chaîne la plus fréquente dans la colonne .
- **[Vector Assembler](./feature-transformation.md#vector-assembler)** : combinez plusieurs colonnes en une seule colonne vectorielle pour préparer les données pour les modèles de machine learning.
- **[Ordinateur booléen](./feature-transformation.md#boolean-imputer)** : remplissez les valeurs booléennes manquantes avec une valeur spécifiée, par exemple `true` ou `false`.

#### Transformateurs numériques

Appliquez ces techniques pour traiter et mettre à l’échelle efficacement les données numériques afin d’améliorer les performances du modèle.

- **[Binarizer](./feature-transformation.md#binarizer)** : permet de convertir des fonctions continues en valeurs binaires en fonction d’un seuil.
- **[Compartimenteur](./feature-transformation.md#bucketizer)** : mappez les fonctionnalités continues dans des compartiments discrets.
- **[Min-Max Scaler](./feature-transformation.md#minmaxscaler)** : redimensionnez les fonctionnalités dans une plage spécifiée, généralement [0, 1].
- **[Max Abs Scaler](./feature-transformation.md#maxabsscaler)** : redimensionnez les fonctions dans la plage [-1, 1] sans modifier la dispersion.
- **[Normaliseur](./feature-transformation.md#normalizer)** : permet de normaliser les vecteurs pour obtenir une norme unitaire.
- **[Quantile Discretizer](./feature-transformation.md#quantilediscretizer)** : convertissez les fonctions continues en fonctions catégorielles en les classant en quantités.
- **[Standard Scaler](./feature-transformation.md#standardscaler)** : normalisez les caractéristiques pour avoir un écart type unitaire et/ou une moyenne nulle.

#### Transformateurs catégoriels

Utilisez ces transformateurs pour convertir et coder des données catégorielles dans des formats adaptés aux modèles de machine learning.

- **[Indexeur de chaîne](./feature-transformation.md#stringindexer)** : convertissez des données de chaîne catégorielles en index numériques.
- **[Un encodeur à chaud](./feature-transformation.md#onehotencoder)** : mappe les données catégorielles en vecteurs binaires.

### Sélection de fonctionnalités {#feature-selection}

Ensuite, concentrez-vous sur la sélection d’un sous-ensemble des fonctionnalités les plus importantes de la visionneuse d’origine. Ce processus permet de réduire les dimensions de vos données, ce qui facilite le traitement de vos modèles et améliore les performances globales du modèle.

<!-- 
Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. 
-->

## Mise en œuvre de la clause OPTIONS {#options-clause}

Lorsque vous définissez votre modèle, utilisez la clause `OPTIONS` pour spécifier l’algorithme et ses paramètres. Commencez par définir le paramètre `type` pour indiquer l’algorithme que vous utilisez, par exemple `K-Means`. Définissez ensuite les paramètres pertinents de la clause `OPTIONS` en tant que paires clé-valeur pour affiner votre modèle. Si vous choisissez de ne pas personnaliser certains paramètres, le système applique les paramètres par défaut. Reportez-vous à la documentation pertinente pour comprendre la fonction et les valeurs par défaut de chaque paramètre.

### Étapes suivantes

Après avoir appris les techniques d’ingénierie des fonctionnalités décrites dans ce document, passez au document [Modèles](./models.md). Il vous guide tout au long du processus de création, de formation et de gestion de modèles approuvés à l’aide des fonctionnalités que vous avez conçues. Une fois vos modèles créés, passez au document [ Implémenter des modèles statistiques avancés .](./implement-models/implement-models.md). Ce document offre un aperçu et fournit des liens vers des guides détaillés relatifs à différentes techniques de modélisation, notamment la mise en grappe, la classification et la régression. En suivant ces documents, vous apprendrez à configurer et à implémenter divers modèles approuvés dans vos workflows SQL et à optimiser vos modèles pour une analyse de données avancée.
