---
title: Techniques de transformation des fonctionnalités
description: Découvrez les techniques de prétraitement essentielles telles que la transformation des données, le codage et la mise à l’échelle des fonctionnalités, qui préparent les données pour l’entraînement des modèles statistiques. Elle traite de l’importance de la gestion des valeurs manquantes et de la conversion des données catégorielles pour améliorer les performances et la précision du modèle.
role: Developer
exl-id: ed7fa9b7-f74e-481b-afba-8690ce50c777
TQID: https://experienceleague.adobe.com/4FfVYgpCXTwYmHb-wiFQQGLPupHQJ7JKfU-elHayugU
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 3447
ht-degree: 10%

---

# Techniques de transformation des caractéristiques

Les transformations sont des étapes de prétraitement cruciales qui convertissent ou mettent à l’échelle des données dans un format adapté à l’entraînement et à l’analyse des modèles, assurant des performances et une précision optimales. Ce document sert de ressource syntaxique supplémentaire et fournit des détails détaillés sur les principales techniques de transformation des fonctionnalités pour le prétraitement des données.

Les modèles de machine learning ne peuvent pas traiter directement les valeurs de chaîne ou les valeurs nulles, ce qui rend le prétraitement des données essentiel. Ce guide explique comment utiliser diverses transformations pour imputer les valeurs manquantes, convertir des données catégorielles en formats numériques et appliquer des techniques de mise à l’échelle des fonctionnalités telles que l’encodage à chaud et la vectorisation. Ces méthodes permettent aux modèles d’interpréter et d’apprendre efficacement des données, ce qui améliore finalement leurs performances.

## Transformation automatique des caractéristiques {#automatic-transformations}

Si vous choisissez d&#39;ignorer la clause `TRANSFORM` dans votre commande `CREATE MODEL`, la transformation de fonction se produit automatiquement. Le prétraitement automatique des données inclut le remplacement des valeurs nulles et les transformations de caractéristiques standard (en fonction du type de données). Les colonnes numériques et de texte sont automatiquement imputées, puis des transformations de caractéristiques sont effectuées pour s’assurer que les données sont dans un format approprié pour l’entraînement de modèles de machine learning. Ce processus inclut l’imputation de données manquante et les transformations catégorielles, numériques et booléennes.

>[!IMPORTANT]
>
>La transformation de fonction utilisée au moment de la formation sera également utilisée pour la transformation de fonction au moment de la prédiction et de l’évaluation.

Les tableaux suivants expliquent comment différents types de données sont gérés lorsque la clause `TRANSFORM` est omise lors de la commande `CREATE MODEL`.

### Remplacement nul {#automatic-null-replacement}

| Type de données | Remplacement nul |
|-----------------|-----------------------------------------------------|
| Numérique | Les valeurs NULL sont remplacées par la valeur moyenne de la colonne. |
| Catégorique | Les valeurs nulles sont remplacées par le mot-clé `ml_unknown`. |
| Booléen | Les valeurs nulles sont remplacées par une valeur `FALSE`. |
| Date et heure | Ce champ devrait être continu. |
| Imbriqué/STRUCT | Le remplacement dépend du type de données du nœud feuille. |

### Transformation de caractéristiques {#automatic-feature-transformation}

| Type de données | Transformation de fonctionnalités |
|-----------------|-----------------------------------------------------|
| Numérique | NON REQUIS - Ce type de données est compris par les algorithmes de machine learning de . |
| Chaîne | L’indexation des chaînes se produit. |
| Booléen | L’indexation des chaînes se produit. |
| Date et heure | Aucune opération ne se produit. |
| STRUCT | La valeur est développée jusqu’à son nœud feuille. La transformation se produit en fonction du type de données du nœud feuille. |

**exemple**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Transformations manuelles des caractéristiques {#manual-transformations}

Pour définir un prétraitement des données personnalisé dans votre instruction `CREATE MODEL`, utilisez la clause `TRANSFORM` en combinaison avec un certain nombre de fonctions de transformation disponibles. Ces fonctions de prétraitement manuel peuvent également être utilisées en dehors de la clause `TRANSFORM`. Toutes les transformations décrites dans la section [transformateur ci-dessous](#available-transformations) peuvent être utilisées pour prétraiter les données manuellement.

### Principales caractéristiques {#key-characteristics}

Voici les principales caractéristiques de la transformation des fonctions à prendre en compte lorsque vous définissez vos fonctions de prétraitement :

- **Syntaxe** : `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - Le nom d’alias est obligatoire dans la syntaxe. Vous devez fournir un nom d’alias pour que la requête échoue.

- **Parameters** : les paramètres sont des arguments positionnels. Cela signifie que chaque paramètre ne peut prendre que certaines valeurs et nécessite que tous les paramètres précédents soient spécifiés si des valeurs personnalisées sont fournies. Reportez-vous à la documentation pertinente pour plus d’informations sur la fonction qui accepte tel argument.

- **Transformateurs à chaîne** : la sortie d&#39;un transformateur peut devenir l&#39;entrée d&#39;un autre transformateur.

- **Utilisation des fonctionnalités** : la dernière transformation de fonctionnalité est utilisée en tant que fonctionnalité du modèle de machine learning.

**Exemple**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## Transformations disponibles {#available-transformations}

Il existe 19 transformations disponibles. Ces transformations sont divisées en [Transformations générales](#general-transformations), [Transformations numériques](#numeric-transformations), [Transformations catégorielles](#categorical-transformations) et [Transformations textuelles](#textual-transformations).

### Transformations générales {#general-transformations}

Lisez cette section pour plus de détails sur les transformateurs utilisés pour un large éventail de types de données. Ces informations sont essentielles si vous devez appliquer des transformations non spécifiques aux données catégorielles ou textuelles.

>[!NOTE]
>
>Le type de données d’entrée fait référence à la colonne sur laquelle l’imputation est appliquée. Le type de données de sortie fait référence à la colonne qui est générée en tant que sortie une fois que la transformation a pris effet.

#### Imprimante numérique {#numeric-imputer}

Le transformateur **Imprimante numérique** complète les valeurs manquantes dans un jeu de données. Cette méthode utilise la moyenne, la médiane ou le mode des colonnes dans lesquelles se trouvent les valeurs manquantes. Les colonnes d’entrée doivent être `DoubleType` ou `FloatType`. Vous trouverez plus d’informations et d’exemples dans la documentation sur l’algorithme [ Spark](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer).

>[!NOTE]
>
>Toutes les valeurs nulles dans les colonnes d’entrée sont traitées comme manquantes et donc également imputées.

**Types des données**

- Type de données d’entrée : numérique
- Type de données de sortie : numérique

**Définition**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | Une stratégie d&#39;imputation. Les valeurs disponibles sont les suivantes : [`mean`, `median` et `mode`]. | chaîne | mean | facultatif |

{style="table-layout:auto"}

**Exemple avant imputation**

| identifiant | hour |
|---|---|
| 0 | 18,0 |
| 1 | null |
| 2 | 8,0 |

**Exemple après imputation (en utilisant la stratégie moyenne)**

| identifiant | hour |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Imprimante de chaînes {#string-imputer}

Le transformateur **Imputeur de chaîne** complète les valeurs manquantes dans un jeu de données à l’aide d’une chaîne fournie par l’utilisateur comme argument de fonction. Les colonnes d’entrée et de sortie doivent être du type de données `string`.

>[!NOTE]
>
>Toutes les valeurs nulles des colonnes d’entrée sont traitées comme manquantes et sont remplacées par la chaîne spécifiée.

**Types des données**

- Type de données d’entrée : chaîne
- Type de données de sortie : chaîne

**Définition**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Valeur qui remplace les valeurs nulles. | chaîne | ml_unknown | facultatif |

{style="table-layout:auto"}

**Exemple avant imputation**

| identifiant | nom |
|---|---|
| 0 | John |
| 1 | null |
| 2 | Alice |

**Exemple après imputation (en utilisant &#39;ml_unknown&#39; comme remplacement)**

| identifiant | nom |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Imprimante booléenne {#boolean-imputer}

Le transformateur **imputeur booléen** complète les valeurs manquantes dans un jeu de données pour une colonne booléenne. Les colonnes d’entrée et de sortie doivent être de type `Boolean`.

>[!NOTE]
>
>Toutes les valeurs nulles des colonnes d’entrée sont traitées comme manquantes et sont remplacées par la valeur booléenne spécifiée.

**Types des données**

- Type de données d’entrée : booléen
- Type de données de sortie : booléen

**Définition**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Imprimante booléenne. Valeurs autorisées : [`true`, `false`]. | booléen | False | facultatif |

**Exemple avant imputation**

| identifiant | drapeau |
|---|---|
| 0 | vrai |
| 1 | null |
| 2 | False |

**Exemple après imputation (en utilisant &#39;true&#39; comme remplacement)**

| identifiant | drapeau |
|---|---|
| 0 | vrai |
| 1 | vrai |
| 2 | False |

#### Assembleur vectoriel {#vector-assembler}

Le transformateur `VectorAssembler` combine une liste spécifiée de colonnes d’entrée en une seule colonne vectorielle, ce qui facilite la gestion de plusieurs fonctionnalités dans les modèles de machine learning. Ceci est particulièrement utile pour fusionner des fonctions brutes et celles générées par différents transformateurs de fonctions en un seul vecteur de fonctions unifié. `VectorAssembler` accepte les colonnes d’entrée de types numérique, booléen et vectoriel. Dans chaque ligne, les valeurs des colonnes d&#39;entrée sont concaténées dans un vecteur dans l&#39;ordre spécifié.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Types des données**

- Type de données d’entrée : `array[string]` (noms de colonne avec valeurs numériques/tableaux[numériques])
- Type de données de sortie : `Vector[double]`

**Définition**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
| -------- | ------------ | ----- | -------- | -------- |
| Non applicable | Aucun paramètre supplémentaire n&#39;est requis pour ce transformateur. | Non applicable | Non applicable | Non applicable |

{style="table-layout:auto"}

**Exemple avant transformation**

| identifiant | hour | mobile | userFeatures | cliqué |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1.0 | [0.0, 10.0, 0.5] | 1.0 |

{style="table-layout:auto"}

**Exemple après transformation**

| identifiant | hour | mobile | userFeatures | cliqué | fonctionnalités |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1.0 | [0.0, 10.0, 0.5] | 1.0 | [18.0, 1.0, 0.0, 10.0, 0.5] |

{style="table-layout:auto"}

### Transformations numériques {#numeric-transformations}

Lisez cette section pour en savoir plus sur les transformateurs disponibles pour le traitement et la mise à l’échelle des données numériques. Ces transformateurs sont nécessaires pour gérer et optimiser les fonctionnalités numériques de vos jeux de données.

#### Binarizer {#binarizer}

Le transformateur `Binarizer` convertit les caractéristiques numériques en caractéristiques binaires (0/1) par un processus appelé binarisation. Les valeurs de caractéristique supérieures au seuil spécifié sont converties en 1,0, tandis que les valeurs égales ou inférieures au seuil sont converties en 0,0. Le `Binarizer` prend en charge les types `Vector` et `Double` pour la colonne d’entrée.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**Types des données**

- Type de données d’entrée : colonne numérique
- Type de données de sortie : numérique

**Définition**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | Paramètre du seuil utilisé pour binariser les fonctions continues. Les fonctions supérieures au seuil sont binarisées sur 1.0, tandis que les fonctions égales ou inférieures au seuil sont binarisées sur 0.0. | int/double | 0,0 | facultatif |

{style="table-layout:auto"}

**Exemple d’entrée avant la binarisation**

| identifiant | évaluation |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**Exemple de sortie après binarisation (seuil par défaut de 0,0)**

| identifiant | évaluation |
|---|---------|
| 0 | 0,0 |
| 1 | 1.0 |
| 2 | 1.0 |

**Définition avec seuil personnalisé**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**Exemple de sortie après binarisation (avec un seuil de 14,0)**

| identifiant | age |
|---|-------|
| 0 | 0,0 |
| 1 | 0,0 |
| 2 | 1.0 |

#### Compartimenteur {#bucketizer}

Le transformateur `Bucketizer` convertit une colonne de fonctions continues en une colonne d&#39;intervalles de fonctions, en fonction de seuils spécifiés par l&#39;utilisateur. Ce processus est utile pour segmenter les données continues en compartiments ou compartiments discrets. Le `Bucketizer` nécessite un paramètre `splits`, qui définit les limites des intervalles.

**Types des données**

- Type de données d’entrée : colonne numérique
- Type de données de sortie : numérique (valeurs en classe)

**Définition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | Paramètre permettant de mapper des fonctions continues dans des regroupements. Avec les divisions `n+1`, il existe `n` compartiments. Les divisions doivent être dans un ordre strictement croissant et la plage (x,y) est utilisée pour chaque compartiment, à l’exception du dernier, qui inclut y. | array(double) | S.O. | facultatif |

{style="table-layout:auto"}

**Exemples de divisions**

- Tableau(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Tableau(0.0, 1.0, 2.0)

Les divisions doivent couvrir l’ensemble de la plage de valeurs Double ; sinon, les valeurs en dehors des divisions spécifiées seront traitées comme des erreurs.

**Exemple de transformation**

Cet exemple prend une colonne de fonctions continues (`course_duration`), la classe selon le `splits` fourni, puis assemble les compartiments résultants avec d&#39;autres fonctions.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

Le transformateur `MinMaxScaler` redimensionne chaque fonction d’un jeu de données de lignes de vecteurs à une plage spécifiée, généralement [0, 1]. Cela permet de s’assurer que toutes les fonctionnalités contribuent de manière égale au modèle. Elle est particulièrement utile pour les modèles sensibles à la mise à l’échelle des caractéristiques, tels que les algorithmes basés sur la descente de gradient. Le `MinMaxScaler` fonctionne sur les paramètres suivants :

- **min** : limite inférieure de la transformation, partagée par toutes les fonctionnalités. La valeur par défaut est `0.0`.
- **max** : limite supérieure de la transformation, partagée par toutes les fonctionnalités. La valeur par défaut est `1.0`.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**Types des données**

- Type de données d’entrée : `Array[Double]`
- Type de données de sortie : `Array[Double]`

**Définition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | Limite inférieure après transformation, partagée par toutes les fonctionnalités. | double | 0,0 | facultatif |
| `max` | Limite supérieure après transformation, partagée par toutes les fonctionnalités. | double | 1.0 | facultatif |

**Exemple de transformation**

Cet exemple transforme un ensemble de fonctions, en les redimensionnant à la plage spécifiée à l&#39;aide de MinMaxScaler après avoir appliqué plusieurs autres transformations.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

Le transformateur `MaxAbsScaler` redimensionne chaque caractéristique d&#39;un jeu de données de lignes de vecteurs à la plage [-1, 1] en divisant par la valeur absolue maximale de chaque caractéristique. Cette transformation est idéale pour préserver la dispersion dans les jeux de données avec des valeurs positives et négatives, car elle ne déplace ni ne centre les données. Cela rend le `MaxAbsScaler` particulièrement adapté aux modèles sensibles à l&#39;échelle des caractéristiques d&#39;entrée, telles que celles impliquant des calculs de distance.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**Types des données**

- Type de données d’entrée : `Array[Double]`
- Type de données de sortie : `Array[Double]`

**Définition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| Non applicable | MaxAbsScaler ne nécessite aucun paramètre supplémentaire pour son fonctionnement. | Non applicable | Non applicable | Non applicable |

**Exemple de transformation**

Cet exemple montre comment appliquer plusieurs transformations, y compris `MaxAbsScaler`, pour redimensionner des fonctions dans la plage [-1, 1].

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normaliseur {#normalizer}

Le `Normalizer` est un transformateur qui normalise chaque vecteur dans un jeu de données de lignes de vecteurs pour avoir une norme d&#39;unité. Ce procédé assure une échelle cohérente sans altérer la direction des vecteurs. Cette transformation est particulièrement utile dans les modèles de machine learning qui reposent sur des mesures de distance ou d’autres calculs vectoriels, en particulier lorsque l’amplitude des vecteurs varie considérablement.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**Types des données**

- Type de données d’entrée : `array[double]` / `vector[double]`
- Type de données de sortie : `vector[double]`

**Définition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | Spécifie le `p-norm` utilisé pour la normalisation (par exemple, `1-norm`, `2-norm`, etc.). | entier | 2 | facultatif |

**Exemple de transformation**

Cet exemple montre comment appliquer plusieurs transformations, y compris le `Normalizer`, pour normaliser un ensemble de fonctions à l&#39;aide de la `p-norm` spécifiée.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

Le `QuantileDiscretizer` est un transformateur qui convertit une colonne avec des fonctions continues en fonctions catégorielles compartimentées, avec le nombre de compartiments déterminé par le paramètre `numBuckets`. Dans certains cas, le nombre réel d’intervalles peut être inférieur à ce nombre spécifié s’il y a trop peu de valeurs distinctes pour créer suffisamment de quantités.

Cette transformation est particulièrement utile pour simplifier la représentation des données continues ou pour la préparer à des algorithmes qui fonctionnent mieux avec une entrée catégorielle.

**Types des données**

- Type de données d’entrée : colonne numérique
- Type de données de sortie : colonne numérique (catégorielle)

**Définition**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | Nombre d’intervalles (quantiles ou catégories) dans lesquels les points de données sont regroupés. Ce nombre doit être supérieur ou égal à deux. | entier | 2 | facultatif |

**Exemple de transformation**

Cet exemple montre comment le `QuantileDiscretizer` regroupe une colonne de fonctions continues (`hour`) en trois compartiments catégoriels.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Exemple avant et après discrétisation**

| identifiant | hour | résultat |
|---|------|--------|
| 0 | 18,0 | 2.0 |
| 1 | 19,0 | 2.0 |
| 2 | 8,0 | 1.0 |
| 3 | 5.0 | 1.0 |
| 4 | 2,2 | 0,0 |

#### StandardScaler {#standardscaler}

Le `StandardScaler` est un transformateur qui normalise chaque caractéristique dans un jeu de données de lignes vectorielles pour avoir un écart-type unitaire et/ou une moyenne nulle. Ce processus rend les données plus adaptées aux algorithmes qui supposent que les fonctionnalités sont centrées autour de zéro avec une échelle cohérente. Cette transformation est particulièrement importante pour les modèles d’apprentissage automatique tels que la MVS, la régression logistique et les réseaux de neurones, où des données non normalisées pourraient entraîner des problèmes de convergence ou une précision réduite.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**Types des données**

- Type de données d’entrée : Vecteur
- Type de données de sortie : Vecteur

**Définition**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | Met à l’échelle les données pour avoir un écart type d’unité. | booléen | True | facultatif |
| `withMean` | Centre les données avec la moyenne avant la mise à l’échelle. Cette option génère une sortie dense. Faites donc preuve de prudence lorsque les entrées sont éparses. | booléen | False | facultatif |

**Exemple de transformation**

Cet exemple montre comment appliquer le StandardScaler à un ensemble de fonctionnalités, en les normalisant avec un écart-type unitaire et une moyenne nulle.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Transformations catégorielles {#categorical-transformations}

Lisez cette section pour obtenir un aperçu des transformateurs disponibles conçus pour convertir et prétraiter des données catégorielles pour les modèles de machine learning. Ces transformations sont conçues pour les points de données qui représentent des catégories ou des libellés distincts, plutôt que des valeurs numériques.

#### StringIndexer {#stringindexer}

Le `StringIndexer` est un transformateur qui code une colonne de chaînes d&#39;étiquettes en une colonne d&#39;indices numériques. Les indices vont de 0 à `numLabels` et sont ordonnés par fréquence de libellé (le libellé le plus fréquent reçoit un index de 0). Si la colonne d’entrée est numérique, elle est convertie en chaîne avant l’indexation. Les libellés non affichés peuvent être affectés au `numLabels` d’index s’ils sont spécifiés par l’utilisateur.

Cette transformation est particulièrement utile pour convertir des données de chaîne catégorielles en forme numérique, ce qui les rend adaptées aux modèles de machine learning qui nécessitent une entrée numérique.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**Types des données**

- Type de données d’entrée : chaîne
- Type de données de sortie : numérique

**Définition**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|-------------|------|---------|----------|
| Non applicable | `StringIndexer` ne nécessite aucun paramètre supplémentaire pour son fonctionnement. | Non applicable | Non applicable | Non applicable |

**Exemple de transformation**

Cet exemple montre comment appliquer le `StringIndexer` à une fonction catégorielle, en la convertissant en index numérique.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

Le `OneHotEncoder` est un transformateur qui convertit une colonne d&#39;indices d&#39;étiquettes en une colonne de vecteurs binaires épars, chaque vecteur ayant au plus une seule valeur. Ce codage est particulièrement utile pour permettre aux algorithmes qui nécessitent une entrée numérique, comme la régression logistique, d&#39;incorporer efficacement des données catégorielles.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**Types des données**

- Type de données d’entrée : numérique
- Type de données de sortie : Vector[Int]

**Définition**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|-------------|------|---------|----------|
| Non applicable | OneHotEncoder ne nécessite aucun paramètre supplémentaire pour son fonctionnement. | Non applicable | Non applicable | Non applicable |

**Exemple de transformation**

Cet exemple montre comment d’abord appliquer le `StringIndexer` à une fonction catégorielle, puis utiliser le `OneHotEncoder` pour convertir les valeurs indexées en vecteur binaire.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Transformations textuelles {#textual-transformations}

Cette section fournit des détails sur les transformateurs disponibles pour le traitement et la conversion de données de texte en formats utilisables par les modèles de machine learning. Cette section est essentielle pour les développeurs qui travaillent avec des données en langage naturel et l’analyse de texte.

#### CountVectorizer {#countvectorizer}

Le `CountVectorizer` est un transformateur qui convertit une collection de documents texte en vecteurs de nombres de jetons, produisant des représentations éparses basées sur le vocabulaire extrait du corpus. Cette transformation est essentielle pour convertir des données textuelles en format numérique qui peut être utilisé par des algorithmes de machine learning, tels que LDA (Latent Dirichlet Allocation), en représentant la fréquence des jetons dans chaque document.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Types des données**

- Type de données d’entrée : Array[String]
- Type de données de sortie : Vecteur dense

**Définition**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Taille max du vocabulaire. CountVectorizer crée un vocabulaire qui ne prend en compte que les `vocabSize` termes les plus fréquents classés par fréquence de terme dans le corpus. | Int | 218 | facultatif |
| `MIN_DOC_FREQ` | Indique le nombre minimum de documents différents dans lesquels un terme doit apparaître pour être inclus dans le vocabulaire. Il peut s’agir d’un nombre absolu ou d’une fraction de documents (s’il s’agit d’un double). | Double | 1.0 | facultatif |
| `MAX_DOC_FREQ` | Indique le nombre maximal de documents différents dans lesquels un terme peut apparaître pour être inclus dans le vocabulaire. Il peut s’agir d’un nombre absolu ou d’une fraction de documents (s’il s’agit d’un double). | Double | (263)-1 | facultatif |
| `MIN_TERM_FREQ` | Filtre les mots rares dans un document. Les termes dont la fréquence/le nombre est inférieur au seuil donné sont ignorés. Il peut s’agir d’un nombre absolu ou d’une fraction du nombre de jetons du document. | Double | 1.0 | facultatif |

{style="table-layout:auto"}

**Exemple de transformation**

Cet exemple montre comment CountVectorizer convertit une collection de tableaux de texte en vecteurs de nombres de jetons, produisant ainsi une représentation éparse.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Exemple avant et après vectorisation**

| identifiant | SMS | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(« a », « b », « c ») | (3,[0,1,2],[1.0,1.0,1.0]) |
| 1 | Tableau(« a », « b », « b », « c », « a ») | (3,[0,1,2],[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

Le `NGram` est un transformateur qui génère une séquence de n-grammes, où un n-gramme est une séquence de (&#39;𝑛&#39;) jetons (typiquement des mots) pour un entier (`𝑛`). La sortie se compose de chaînes délimitées par des espaces de mots consécutifs « 𝑛 », qui peuvent être utilisées comme fonctionnalités dans les modèles de machine learning, en particulier ceux axés sur le traitement du langage naturel.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Types des données**

- Type de données d’entrée : Array[String]
- Type de données de sortie : Array[String]

**Définition**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | La longueur minimale de n grammes doit être supérieure ou égale à 1. | entier | 2 (fonctionnalités bigram) | facultatif |

{style="table-layout:auto"}

**Exemple de transformation**

Cet exemple montre comment le transformateur NGram crée une séquence de 3 grammes à partir d’une liste de jetons dérivés de données texte.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Exemple avant et après la transformation n-gram**

| identifiant | SMS | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [ « ceci », « était », « un », « divertissant », « film »] | [ « c&#39;était un », « c&#39;était un divertissement », « un film divertissant »] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

Le `StopWordsRemover` est un transformateur qui supprime les mots vides d&#39;une séquence de chaînes, en filtrant les mots communs qui n&#39;ont pas de signification significative. Elle prend en entrée une séquence de chaînes (comme la sortie d’un jeton) et supprime tous les mots vides spécifiés par le paramètre `stopWords`.

Cette transformation est utile pour le prétraitement des données textuelles, ce qui améliore l’efficacité des modèles de machine learning en aval en éliminant les mots qui ne contribuent pas beaucoup à la signification globale.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Types des données**

- Type de données d’entrée : Array[String]
- Type de données de sortie : Array[String]

**Définition**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | Mots à filtrer. | tableau [chaîne] | Valeur par défaut : mots vides anglais | facultatif |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**Exemple de transformation**

Cet exemple montre comment le `StopWordsRemover` filtre les mots vides courants en anglais d’une liste de jetons.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Exemple avant et après la suppression des mots vides**

| identifiant | brut | filtré |
|----|------------------------------|--------------------------|
| 0 | [J&#39;ai vu, le, rouge, ballon] | [scie, rouge, ballon] |
| 1 | [Mary, a eu, un, petit, agneau] | [Marie, petit, agneau] |

**Exemple avec des mots vides personnalisés**

Cet exemple montre comment utiliser une liste personnalisée de mots vides pour filtrer des mots spécifiques des séquences d’entrée.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Exemple avant et après la suppression de mots vides personnalisés**

| identifiant | brut | filtré |
|----|------------------------------|--------------------------|
| 0 | [J&#39;ai vu, le, rouge, ballon] | [scie, le, ballon] |
| 1 | [Mary, a eu, un, petit, agneau] | [Marie, un, petit, agneau] |

#### TF-IDF {#tf-idf}

Le `TF-IDF` (Terme Fréquence-Inverse de Document Frequency) est un transformateur utilisé pour mesurer l&#39;importance d&#39;un mot dans un document par rapport à un corpus. La fréquence des termes (TF) fait référence au nombre de fois qu&#39;un terme \(t\) apparaît dans un document \(d\), tandis que la fréquence des documents (DF) mesure le nombre de documents dans le corpus \(D\) contenant le terme \(t\). Cette méthode est largement utilisée dans l’exploration de texte pour réduire l’influence de mots courants, tels que « a », « le » et « de », qui contiennent peu d’informations uniques.

Cette transformation est particulièrement utile pour l’exploration de texte et le traitement du langage naturel, car elle attribue une valeur numérique à l’importance de chaque mot dans un document et dans l’ensemble du corpus.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**Types des données**

- Type de données d’entrée : Array[String]
- Type de données de sortie : Vector[Int]

**Définition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | Nombre de fonctionnalités à générer. Doit être supérieur à 0. | Int | 262144 | facultatif |
| `MIN_DOC_FREQ` | Nombre minimal de documents dans lesquels un terme doit apparaître comme inclus dans le modèle. | Int | 0 | facultatif |

{style="table-layout:auto"}

**Exemple de transformation**

Cet exemple montre comment utiliser TF-IDF pour transformer des phrases segmentées en un vecteur de caractéristiques qui représente l’importance de chaque terme dans le contexte du corpus entier.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

Le `Tokenizer` est un transformateur qui décompose le texte, tel qu’une phrase, en termes individuels, généralement des mots. Il convertit les phrases en tableaux de jetons, fournissant ainsi une étape fondamentale dans le prétraitement de texte qui prépare les données pour d’autres processus d’analyse de texte ou de modélisation.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Types des données**

- Type de données d’entrée : Phrase textuelle
- Type de données de sortie : Array[String]

**Définition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|-------------|------|---------|----------|
| Non applicable | Le `Tokenizer` ne nécessite aucun paramètre supplémentaire pour son fonctionnement. | Non applicable | Non applicable | Non applicable |

**Exemple de transformation**

Cet exemple montre comment le `Tokenizer` répartit les phrases en mots individuels (jetons) dans le cadre d’un pipeline de traitement de texte.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

Le `Word2Vec` est un estimateur qui traite des séquences de mots représentant des documents et entraîne un `Word2VecModel`. Ce modèle mappe chaque mot à un vecteur de taille fixe unique et transforme chaque document en un vecteur en faisant la moyenne des vecteurs de tous les mots du document. Largement utilisé dans les tâches de traitement du langage naturel, `Word2Vec` crée des incorporations de mots qui capturent une signification sémantique, convertissant des données textuelles en vecteurs numériques qui représentent les relations entre les mots et permettant une analyse de texte plus efficace et des modèles de machine learning.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**Types des données**

- Type de données d’entrée : Array[String]
- Type de données de sortie : Vector[Double]

**Définition**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | La dimension du vecteur dans lequel chaque mot est transformé. | Entier | 100 | facultatif |
| `MIN_COUNT` | Nombre minimal de fois où un jeton doit sembler inclus dans le vocabulaire du modèle de `Word2Vec`. | Entier | 5 | facultatif |

{style="table-layout:auto"}

**Exemple de transformation**

Cet exemple montre comment `Word2Vec` convertit une révision segmentée en unités lexicales en un vecteur de taille fixe représentant la moyenne des vecteurs de mot dans le document.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Exemple avant et après la transformation Word2Vec**

| revue | tokenisé | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| c&#39;était un film divertissant | [c&#39;était, un film divertissant] | [-0,025713888928294182,0,00818799751577899,0,0092235435731709,-0,01515385233797133,0,012175946310162545,3,1129065901041035E-4,0,0025145105042611252,0,005757019785232843,-0,021328244300093502,0,009335877187550069] |

{style="table-layout:auto"}
