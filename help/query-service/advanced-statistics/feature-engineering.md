---
title: Extension SQL d’ingénierie de fonctionnalités
description: Découvrez l’extension SQL de conception des fonctionnalités de Data Distiller pour prétraiter les données pour la modélisation statistique avancée. Il couvre les techniques d’extraction, de transformation et de sélection des fonctionnalités disponibles.
role: Developer
source-git-commit: 1fcfb5c41750e853daaf036ceaae3527b805391c
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Extension SQL d’ingénierie de fonctionnalités

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Data Distiller. Pour en savoir plus, contactez votre représentant ou représentante Adobe.

Pour répondre à vos besoins en matière d’ingénierie de fonctionnalités, utilisez l’extension du transformateur SQL afin de simplifier et d’automatiser le prétraitement des données. Utilisez cette extension pour créer des fonctionnalités et profiter d’une expérience transparente avec différentes techniques d’ingénierie de fonctionnalités, y compris en les associant à des modèles. Conçu pour un calcul distribué, vous pouvez concevoir des fonctionnalités sur des jeux de données volumineux de manière parallèle et évolutive, ce qui réduit considérablement le temps nécessaire au prétraitement des données à l’aide de l’extension SQL de conception des fonctionnalités de Data Distiller.

## Présentation des techniques {#technique-overview}

Les fonctionnalités de conception des fonctionnalités couvrent trois principaux domaines : l’extraction des fonctionnalités, la transformation des fonctionnalités et la sélection des fonctionnalités. Chaque zone comprend des fonctions spécifiques conçues pour extraire, convertir, cibler et améliorer le prétraitement des données.

### Extraction de fonctionnalités {#feature-extraction}

Extrayez des informations pertinentes de vos données, en particulier des données texte, et convertissez-les dans un format numérique que les modèles pris en charge peuvent utiliser ou transformer et dériver des jeux de données. Utilisez les fonctions suivantes pour effectuer l’extraction de fonctionnalités :

- **[Transformateur textuel](./feature-transformation.md#textual-transformations)** : convertissez les données textuelles en fonctions numériques.
- **[Count Vectorizer](./feature-transformation.md#countvectorizer)** : transformez une collection de documents texte en vecteurs de nombre de jetons.
- **[N-gram](./feature-transformation.md#ngram)** : génère des séquences d’n-grammes à partir de données textuelles.
- **[Stop Words Remover](./feature-transformation.md#stopwordsremover)** : permet de filtrer les mots courants qui n’ont pas de signification significative.
- **[TF-IDF](./feature-transformation.md#tf-idf)** : mesurez l&#39;importance des mots dans un document par rapport à un corpus.
- **[Tokenizer](./feature-transformation.md#tokenizer)** : ventilez le texte en termes individuels (mots).
- **[Word2Vec](./feature-transformation.md#word2vec)** : mappez des mots à des vecteurs de taille fixe et créez des incorporations de mots.

### Transformation des fonctionnalités {#feature-transformation}

Outre l’extraction de fonctionnalités, utilisez les transformateurs généraux suivants pour préparer vos fonctionnalités aux modèles statistiques avancés et aux jeux de données dérivés. Appliquez une mise à l’échelle, une normalisation ou un codage pour vous assurer que vos fonctionnalités sont à la même échelle et ont une distribution similaire.

#### Transformateurs généraux

Vous trouverez ci-dessous une liste d’outils permettant de traiter un large éventail de types de données afin d’améliorer votre workflow de prétraitement des données.

- **[Ordinateur numérique](./feature-transformation.md#numeric-imputer)** : renseignez les valeurs manquantes dans les colonnes numériques avec un
- **[String Imputer](./feature-transformation.md#string-imputer)** : remplacez les valeurs de chaîne manquantes par une valeur spécifiée
- **[Assembler vectoriel](./feature-transformation.md#vector-assembler)** : combine plusieurs colonnes en une seule colonne vectorielle.

#### Transformeurs numériques

Appliquez ces techniques pour traiter et mettre à l’échelle efficacement les données numériques afin d’améliorer les performances des modèles.

- **[Binarizer](./feature-transformation.md#binarizer)** : convertissez les fonctionnalités continues en valeurs binaires basées sur un seuil.
- **[Bucketizer](./feature-transformation.md#bucketizer)** : Mappez les fonctionnalités continues dans des compartiments discrets.
- **[Min-Max Scaler](./feature-transformation.md#minmaxscaler)** : redimensionner les fonctionnalités sur une plage spécifiée, généralement [0, 1].
- **[Max Abs Scaler](./feature-transformation.md#maxabsscaler)** : redimensionner les fonctionnalités à la plage [-1, 1] sans modifier la dispersion.
- **[Normalizer](./feature-transformation.md#normalizer)** : normalisez les vecteurs pour qu’ils aient la norme unitaire.
- **[Quantile Discrétizer](./feature-transformation.md#quantilediscretizer)** : convertissez les fonctionnalités continues en fonctionnalités catégoriques en les regroupant en quantiles.
- **[Évolutif standard](./feature-transformation.md#standardscaler)** : normalisez les fonctionnalités pour obtenir une écart-type unitaire et/ou une moyenne nulle.

#### Transformateurs catégoriels

Utilisez ces transformateurs pour convertir et coder des données catégoriques dans des formats adaptés aux modèles d’apprentissage automatique.

- **[Index de chaîne](./feature-transformation.md#stringindexer)** : convertissez les données de chaîne catégorielles en index numériques.
- **[One Hot Encoder](./feature-transformation.md#onehotencoder)** : mappez des données catégoriques en vecteurs binaires.

### Sélection de fonctionnalités {#feature-selection}

Ensuite, concentrez-vous sur la sélection d’un sous-ensemble des fonctionnalités les plus importantes de l’ensemble d’origine. Ce processus permet de réduire les dimensions de vos données, ce qui facilite le traitement de vos modèles et améliore les performances globales du modèle.

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## Mise en oeuvre de la clause OPTIONS {#options-clause}

Lorsque vous définissez votre modèle, utilisez la clause `OPTIONS` pour spécifier l’algorithme et ses paramètres. Commencez par définir le paramètre `type` pour indiquer l’algorithme que vous utilisez, par exemple `K-Means`. Définissez ensuite les paramètres appropriés dans la clause `OPTIONS` en tant que paires clé-valeur pour affiner votre modèle. Notez que certains paramètres peuvent être positionnés et nécessitent que tous les paramètres précédents soient spécifiés si des valeurs personnalisées sont fournies. Si vous choisissez de ne pas personnaliser certains paramètres, le système applique les paramètres par défaut. Reportez-vous à la documentation appropriée pour comprendre la fonction et les valeurs par défaut de chaque paramètre.

### Étapes suivantes

Après avoir appris les techniques d’ingénierie de fonctionnalités décrites dans ce document, accédez au document [Modèles](./models.md). Il vous guide tout au long du processus de création, de formation et de gestion des modèles de confiance à l’aide des fonctionnalités que vous avez conçues. Une fois vos modèles créés, passez au document [Mise en oeuvre de modèles statistiques avancés.](./implement-models/implement-models.md). Ce document sert d’aperçu, en liant à des guides détaillés pour différentes techniques de modélisation, y compris la mise en grappe, la classification et la régression. En suivant ces documents, vous apprenez à configurer et à mettre en oeuvre différents modèles approuvés dans vos workflows SQL et à optimiser vos modèles pour une analyse avancée des données.
