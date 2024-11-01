---
title: Techniques de transformation des fonctionnalités
description: Découvrez les techniques essentielles de prétraitement telles que la transformation, le codage et la mise à l’échelle des fonctionnalités des données, qui préparent les données à la formation aux modèles statistiques. Il couvre l’importance de gérer les valeurs manquantes et de convertir les données catégorielles afin d’améliorer les performances et la précision du modèle.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '3437'
ht-degree: 9%

---

# Techniques de transformation des fonctionnalités

Les transformations sont des étapes essentielles de prétraitement qui convertissent ou dimensionnent les données dans un format adapté à la formation et à l’analyse des modèles, assurant ainsi des performances optimales et une précision optimale. Ce document sert de ressource de syntaxe complémentaire, fournissant des détails détaillés sur les principales techniques de transformation des fonctionnalités pour le prétraitement des données.

Les modèles d’apprentissage automatique ne peuvent pas traiter directement des valeurs de chaîne ou des valeurs nulles, ce qui rend le prétraitement des données essentiel. Ce guide explique comment utiliser diverses transformations pour imputer les valeurs manquantes, convertir les données catégoriques en formats numériques et appliquer des techniques de mise à l’échelle des fonctionnalités telles que le codage à chaud et la vectorisation. Ces méthodes permettent aux modèles d’interpréter et d’apprendre efficacement des données, ce qui améliore finalement leurs performances.

## Transformation automatique des fonctionnalités {#automatic-transformations}

Si vous choisissez d’ignorer la clause `TRANSFORM` dans votre commande `CREATE MODEL`, la transformation des fonctionnalités se produit automatiquement. Le prétraitement automatique des données comprend des transformations de fonctions standard et de remplacement nulles (basées sur le type de données). Les colonnes numériques et de texte sont automatiquement imputées, puis des transformations de fonctionnalités sont effectuées afin de s’assurer que les données sont dans un format approprié pour la formation des modèles d’apprentissage automatique. Ce processus comprend l’imputation des données manquante et des transformations catégoriques, numériques et booléennes.

>[!IMPORTANT]
>
>La transformation des fonctionnalités utilisée au moment de la formation sera également utilisée pour la transformation des fonctionnalités au moment de la prédiction et de l’évaluation.

Les tableaux suivants expliquent comment différents types de données sont traités lorsque la clause `TRANSFORM` est omise lors de la commande `CREATE MODEL`.

### Remplacement nul {#automatic-null-replacement}

| Type de données | Remplacement nul |
|-----------------|-----------------------------------------------------|
| Numérique | Les valeurs nulles sont remplacées par la valeur moyenne de la colonne. |
| Catégorielle | Les valeurs nulles sont remplacées par le mot-clé `ml_unknown`. |
| Booléen | Les valeurs null sont remplacées par une valeur `FALSE`. |
| Date et heure | Il s’agit d’un champ continu. |
| Imbriqué/STRUCT | Le remplacement dépend du type de données du noeud terminal. |

### Transformation des fonctionnalités {#automatic-feature-transformation}

| Type de données | Transformation des fonctionnalités |
|-----------------|-----------------------------------------------------|
| Numérique | NOT REQUIRED : car ce type de données est compris par les algorithmes d’apprentissage automatique. |
| Chaîne | L’indexation des chaînes se produit. |
| Booléen | L’indexation des chaînes se produit. |
| Date et heure | Aucune opération ne se produit. |
| STRUCTION | La valeur est étendue à son noeud terminal. La transformation se produit en fonction du type de données du noeud terminal. |

**exemple**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Conversion manuelle des fonctionnalités {#manual-transformations}

Pour définir le prétraitement des données personnalisé dans votre instruction `CREATE MODEL`, utilisez la clause `TRANSFORM` en combinaison avec n’importe quel nombre de fonctions de transformation disponibles. Ces fonctions de prétraitement manuel peuvent également être utilisées en dehors de la clause `TRANSFORM`. Toutes les transformations mentionnées dans la section [transformateur ci-dessous](#available-transformations) peuvent être utilisées pour prétraiter les données manuellement.

### Caractéristiques clés

Voici les principales caractéristiques de la transformation des fonctionnalités à prendre en compte lorsque vous définissez vos fonctions de prétraitement :

- **Syntaxe** : `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - Le nom de l&#39;alias est obligatoire dans la syntaxe. Vous devez indiquer un nom d’alias pour que la requête échoue.

- **Parameters** : les paramètres sont des arguments de positionnement. Cela signifie que chaque paramètre ne peut prendre que certaines valeurs. Pour plus d’informations sur la fonction qui utilise cet argument, reportez-vous à la documentation appropriée.

- **Chaînage des transformateurs** : la sortie d’un transformateur peut devenir l’entrée d’un autre transformateur.

- **Utilisation des fonctionnalités** : la dernière transformation des fonctionnalités est utilisée comme une fonctionnalité du modèle d’apprentissage automatique.

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

Il existe 19 transformations disponibles. Ces transformations sont divisées en [transformations générales](#general-transformations), [transformations numériques](#numeric-transformations), [transformations catégorielles](#categorical-transformations) et [transformations textuelles](#textual-transformations).

### Transformations générales {#general-transformations}

Lisez cette section pour plus de détails sur les transformateurs utilisés pour un large éventail de types de données. Ces informations sont essentielles si vous devez appliquer des transformations qui ne sont pas spécifiques aux données catégorielles ou textuelles.

>[!NOTE]
>
>Le type de données d’entrée fait référence à la colonne sur laquelle l’imputation est appliquée. Le type de données de sortie fait référence à la colonne qui est produite en tant que sortie une fois la transformation prise en compte.

#### Imprimeur numérique {#numeric-imputer}

Le transformateur **Numeric imputer** complète les valeurs manquantes dans un jeu de données. Cette option utilise la moyenne, la médiane ou le mode des colonnes dans lesquelles se trouvent les valeurs manquantes. Les colonnes d’entrée doivent être `DoubleType` ou `FloatType`. Vous trouverez plus d’informations et d’exemples dans la [documentation de l’algorithme Spark](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer).

>[!NOTE]
>
>Toutes les valeurs null dans les colonnes d’entrée sont traitées comme manquantes, et donc également imputées.

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
| `STRATEGY` | Une stratégie d&#39;imputation. Les valeurs disponibles sont : [`mean`, `median`, `mode`]. | Chaîne | mean | facultatif |

{style="table-layout:auto"}

**Exemple avant imputation**

| identifiant | hour |
|---|---|
| 0 | 18,0 |
| 1 | null |
| 2 | 8,0 |

**Exemple après imputation (avec stratégie moyenne)**

| identifiant | hour |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Entier de chaîne {#string-imputer}

Le transformateur **chaîne imputer** complète les valeurs manquantes dans un jeu de données à l’aide d’une chaîne fournie par l’utilisateur en tant qu’argument de fonction. Les colonnes d’entrée et de sortie doivent être de type de données `string`.

>[!NOTE]
>
>Toutes les valeurs null dans les colonnes d’entrée sont traitées comme manquantes et sont remplacées par la chaîne spécifiée.

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
| `NULL_REPLACEMENT` | La valeur qui remplace null. | Chaîne | ml_unknown | facultatif |

{style="table-layout:auto"}

**Exemple avant imputation**

| identifiant | nom |
|---|---|
| 0 | John |
| 1 | null |
| 2 | Alice |

**Exemple après imputation (utilisation de &#39;ml_unknown&#39; comme remplacement)**

| identifiant | nom |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Indice booléen {#imputer}

Le transformateur **** de l’attribut booléen complète les valeurs manquantes dans un jeu de données pour une colonne booléenne. Les colonnes d’entrée et de sortie doivent être de type `Boolean`.

>[!NOTE]
>
>Toutes les valeurs null dans les colonnes d’entrée sont traitées comme manquantes et sont remplacées par la valeur booléenne spécifiée.

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
| `NULL_REPLACEMENT` | Indice booléen. Valeurs autorisées : [`true`, `false`]. | Booléen | False | facultatif |

**Exemple avant imputation**

| identifiant | indicateur |
|---|---|
| 0 | vrai |
| 1 | null |
| 2 | False |

**Exemple après imputation (utilisation de &#39;true&#39; comme remplacement)**

| identifiant | indicateur |
|---|---|
| 0 | vrai |
| 1 | vrai |
| 2 | False |

#### Assembleur vectoriel {#vector-assembler}

Le transformateur `VectorAssembler` combine une liste spécifiée de colonnes d’entrée dans une seule colonne vectorielle, ce qui facilite la gestion de plusieurs fonctionnalités dans les modèles d’apprentissage automatique. Cela s’avère particulièrement utile pour fusionner des fonctionnalités brutes et celles générées par différents transformateurs de fonctionnalités en un seul vecteur de fonctionnalités unifié. `VectorAssembler` accepte les colonnes d’entrée de types numérique, booléen et vectoriel. Dans chaque ligne, les valeurs des colonnes de saisie sont concaténées dans un vecteur dans l’ordre indiqué.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Types des données**

- Type de données d’entrée : `array[string]` (noms de colonne avec des valeurs numériques/de tableau [numériques])
- Type de données de sortie : `Vector[double]`

**Définition**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
| -------- | ------------ | ----- | -------- | -------- |
| NA | Aucun paramètre supplémentaire n’est requis pour ce transformateur. | NA | NA | NA |

{style="table-layout:auto"}

**Exemple avant transformation**

| identifiant | hour | mobile | userFeatures | clicked |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1.0 | [0.0, 10.0, 0.5] | 1.0 |

{style="table-layout:auto"}

**Exemple après transformation**

| identifiant | hour | mobile | userFeatures | clicked | fonctionnalités |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1.0 | [0.0, 10.0, 0.5] | 1.0 | [18.0, 1.0, 0.0, 10.0, 0.5] |

{style="table-layout:auto"}

### Transformations numériques {#numeric-transformations}

Lisez cette section pour en savoir plus sur les transformateurs disponibles pour le traitement et la mise à l’échelle des données numériques. Ces transformateurs sont nécessaires pour gérer et optimiser les fonctionnalités numériques de vos jeux de données.

#### Binarizer {#binarizer}

Le transformateur `Binarizer` convertit les fonctions numériques en fonctions binaires (0/1) par le biais d’un processus appelé binarisation. Les valeurs de fonction supérieures au seuil spécifié sont converties en 1.0, tandis que les valeurs égales ou inférieures au seuil sont converties en 0.0. `Binarizer` prend en charge les types `Vector` et `Double` pour la colonne d’entrée.

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
| `THRESHOLD` | Param pour le seuil utilisé pour binariser les fonctionnalités continues. Les fonctionnalités supérieures au seuil sont binaires à 1.0, tandis que les fonctionnalités égales ou inférieures au seuil sont binaires à 0.0. | int/double | 0,0 | facultatif |

{style="table-layout:auto"}

**Exemple d’entrée avant la binarisation**

| identifiant | note |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**Exemple de sortie après la binarisation (seuil par défaut de 0.0)**

| identifiant | note |
|---|---------|
| 0 | 0,0 |
| 1 | 1.0 |
| 2 | 1.0 |

**Définition avec seuil personnalisé**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**Exemple de sortie après la binarisation (avec un seuil de 14.0)**

| identifiant | age |
|---|-------|
| 0 | 0,0 |
| 1 | 0,0 |
| 2 | 1.0 |

#### Bucketizer {#bucketizer}

Le transformateur `Bucketizer` convertit une colonne de fonctionnalités continues en une colonne de compartiments de fonctionnalités, en fonction des seuils spécifiés par l’utilisateur. Ce processus est utile pour segmenter les données continues en classes ou compartiments discrets. `Bucketizer` nécessite un paramètre `splits` qui définit les limites des compartiments.

**Types des données**

- Type de données d’entrée : colonne numérique
- Type de données de sortie : numérique (valeurs binaires)

**Définition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | Paramètre permettant de mapper les fonctionnalités continues en compartiments. Avec `n+1` divisions, il existe `n` compartiments. Les séparations doivent être dans un ordre strictement croissant et la plage (x,y) est utilisée pour chaque compartiment, à l’exception de la dernière, qui inclut y. | array(double) | S/O | facultatif |

{style="table-layout:auto"}

**Exemples de divisions**

- Tableau(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Tableau(0.0, 1.0, 2.0)

Les séparations doivent couvrir toute la gamme des valeurs Double ; dans le cas contraire, les valeurs en dehors des séparations spécifiées seront traitées comme des erreurs.

**Exemple de transformation**

Cet exemple utilise une colonne de fonctionnalités continues (`course_duration`), les classe en fonction du `splits` fourni, puis assemble les compartiments résultants avec d’autres fonctionnalités.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

Le transformateur `MinMaxScaler` redimensionne chaque fonctionnalité d’un jeu de données de lignes vectorielles sur une plage spécifiée, généralement [0, 1]. Cela garantit que toutes les fonctionnalités contribuent de manière égale au modèle. Elle est particulièrement utile pour les modèles sensibles à la mise à l’échelle des fonctionnalités, tels que les algorithmes basés sur la descente en dégradé. Le `MinMaxScaler` fonctionne sur les paramètres suivants :

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

Cet exemple transforme un ensemble de fonctionnalités, les redimensionnant à la plage spécifiée à l’aide de MinMaxScaler après avoir appliqué plusieurs autres transformations.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

Le transformateur `MaxAbsScaler` redimensionne chaque fonctionnalité d’un jeu de données de lignes vectorielles sur la plage [-1, 1] en la divisant par la valeur absolue maximale de chaque fonctionnalité. Cette transformation est idéale pour préserver la dispersion des jeux de données avec des valeurs positives et négatives, car elle ne déplace ni ne centre les données. Cela rend le `MaxAbsScaler` particulièrement adapté aux modèles qui sont sensibles à l’échelle des fonctionnalités d’entrée, comme ceux qui impliquent des calculs de distance.

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
| NA | MaxAbsScaler ne nécessite aucun paramètre supplémentaire pour son fonctionnement. | NA | NA | NA |

**Exemple de transformation**

Cet exemple applique plusieurs transformations, y compris `MaxAbsScaler`, pour redimensionner les fonctionnalités dans la plage [-1, 1].

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normaliseur {#normalizer}

`Normalizer` est un transformateur qui normalise chaque vecteur dans un jeu de données de lignes vectorielles pour avoir une norme unitaire. Ce processus assure une échelle cohérente sans modifier la direction des vecteurs. Cette transformation est particulièrement utile dans les modèles d&#39;apprentissage automatique qui reposent sur des mesures à distance ou d&#39;autres calculs vectoriels, surtout lorsque l&#39;ampleur des vecteurs varie considérablement.

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
| `p` | Spécifie le `p-norm` utilisé pour la normalisation (par exemple, `1-norm`, `2-norm`, etc.). | Entier | 2 | facultatif |

**Exemple de transformation**

Cet exemple montre comment appliquer plusieurs transformations, y compris `Normalizer`, pour normaliser un ensemble de fonctionnalités à l’aide du `p-norm` spécifié.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

`QuantileDiscretizer` est un transformateur qui convertit une colonne avec des fonctions continues en fonctions catégoriques binaires, avec le nombre de classes déterminé par le paramètre `numBuckets` . Dans certains cas, le nombre réel de compartiments peut être inférieur à ce nombre spécifié s’il existe trop peu de valeurs distinctes pour créer suffisamment de quantiles.

Cette transformation est particulièrement utile pour simplifier la représentation des données continues ou pour les préparer aux algorithmes qui fonctionnent mieux avec l’entrée catégorique.

**Types des données**

- Type de données d’entrée : colonne numérique
- Type de données de sortie : colonne numérique (catégorie)

**Définition**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | Nombre de compartiments (quantiles ou catégories) dans lesquels les points de données sont regroupés. Ce nombre doit être supérieur ou égal à deux. | Entier | 2 | facultatif |

**Exemple de transformation**

Cet exemple montre comment `QuantileDiscretizer` classe une colonne de fonctionnalités continues (`hour`) en trois compartiments catégoriques.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Exemple avant et après la discrétisation**

| identifiant | hour | result |
|---|------|--------|
| 0 | 18,0 | 2.0 |
| 1 | 19,0 | 2.0 |
| 2 | 8,0 | 1.0 |
| 3 | 5.0 | 1.0 |
| 4 | 2,2 | 0,0 |

#### StandardScaler {#standardscaler}

`StandardScaler` est un transformateur qui normalise chaque fonctionnalité d’un jeu de données de lignes vectorielles pour obtenir une écart-type unitaire et/ou une moyenne nulle. Ce processus rend les données plus adaptées aux algorithmes qui supposent que les fonctionnalités sont centrées autour de zéro avec une échelle cohérente. Cette transformation est particulièrement importante pour les modèles d&#39;apprentissage automatique tels que SVM, la régression logistique et les réseaux neuronaux, où des données non normalisées pourraient entraîner des problèmes de convergence ou une précision réduite.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**Types des données**

- Type de données d’entrée : vector
- Type de données de sortie : Vector

**Définition**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | Met à l’échelle les données pour obtenir l’écart type unitaire. | Booléen | True | facultatif |
| `withMean` | Centre les données avec la moyenne avant la mise à l’échelle. Cette option produit une sortie dense, il faut donc être prudent avec une entrée clairsemée. | Booléen | False | facultatif |

**Exemple de transformation**

Cet exemple montre comment appliquer StandardScaler à un ensemble de fonctionnalités, en les normalisant avec l’écart-type unitaire et la moyenne nulle.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Conversions catégorielles {#categorical-transformations}

Lisez cette section pour un aperçu des transformateurs disponibles conçus pour convertir et prétraiter des données catégoriques pour les modèles d’apprentissage automatique. Ces transformations sont conçues pour des points de données qui représentent des catégories ou des étiquettes distinctes, plutôt que des valeurs numériques.

#### StringIndexer {#stringindexer}

`StringIndexer` est un transformateur qui code une colonne de chaîne d’étiquettes dans une colonne d’index numériques. Les index sont compris entre 0 et `numLabels` et sont classés par fréquence d’étiquette (le libellé le plus courant reçoit un index de 0). Si la colonne d’entrée est numérique, elle est convertie en chaîne avant indexation. Des libellés non visibles peuvent être affectés à l’index `numLabels` s’ils sont spécifiés par l’utilisateur.

Cette transformation est particulièrement utile pour convertir des données de chaîne catégorielles sous forme numérique, ce qui la rend adaptée aux modèles d’apprentissage automatique qui nécessitent une entrée numérique.

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
| NA | `StringIndexer` ne nécessite aucun paramètre supplémentaire pour son fonctionnement. | NA | NA | NA |

**Exemple de transformation**

Cet exemple montre comment appliquer le `StringIndexer` à une fonction catégorique, en le convertissant en index numérique.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

`OneHotEncoder` est un transformateur qui convertit une colonne d’index de libellé en une colonne de vecteurs binaires épars, où chaque vecteur possède au plus une seule valeur. Cet encodage est particulièrement utile pour permettre aux algorithmes qui nécessitent une entrée numérique, comme la Régression logistique, d’incorporer efficacement les données catégorielles.

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
| NA | OneHotEncoder ne nécessite aucun paramètre supplémentaire pour son fonctionnement. | NA | NA | NA |

**Exemple de transformation**

Cet exemple montre comment appliquer d’abord le `StringIndexer` à une fonction catégorique, puis utiliser le `OneHotEncoder` pour convertir les valeurs indexées en vecteur binaire.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Transformations textuelles {#textual-transformations}

Cette section fournit des détails sur les transformateurs disponibles pour le traitement et la conversion de données texte en formats pouvant être utilisés par les modèles d’apprentissage automatique. Cette section est essentielle pour les développeurs qui travaillent sur les données de langage naturel et l’analyse de texte.

#### CountVectorizer {#countvectorizer}

`CountVectorizer` est un transformateur qui convertit une collection de documents texte en vecteurs de nombre de jetons, produisant des représentations éparses basées sur le vocabulaire extrait du corpus. Cette transformation est essentielle pour convertir des données texte dans un format numérique utilisable par des algorithmes d’apprentissage automatique, tels que LDA (Latent Dirichlet Attribution), en représentant la fréquence des jetons dans chaque document.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Types des données**

- Type de données d’entrée : Array[String]
- Type de données de sortie : Vecteur Dense

**Définition**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Taille maximale du vocabulaire. CountVectorizer crée un vocabulaire qui ne prend en compte que les `vocabSize` principaux termes ordonnés par fréquence de terme dans le corpus. | Int | 218 | facultatif |
| `MIN_DOC_FREQ` | Indique le nombre minimum de documents dans lesquels un terme doit apparaître pour être inclus dans le vocabulaire. Il peut s’agir d’un nombre absolu ou d’une fraction de documents (si le nombre est double). | Double | 1.0 | facultatif |
| `MAX_DOC_FREQ` | Indique le nombre maximal de documents dans lesquels un terme peut apparaître pour être inclus dans le vocabulaire. Il peut s’agir d’un nombre absolu ou d’une fraction de documents (si le nombre est double). | Double | (263)-1 | facultatif |
| `MIN_TERM_FREQ` | Filtre les mots rares d’un document. Les termes dont la fréquence/le nombre est inférieur au seuil donné sont ignorés. Il peut s’agir d’un nombre absolu ou d’une fraction du nombre de jetons du document. | Double | 1.0 | facultatif |

{style="table-layout:auto"}

**Exemple de transformation**

Cet exemple illustre la manière dont CountVectorizer convertit une collection de tableaux de texte en vecteurs de nombres de jetons, produisant ainsi une représentation éparse.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Exemple avant et après la vectorisation**

| identifiant | text | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;) | (3,[0,1,2],[1.0,1.0,1.0]) |
| 1 | Array(&quot;a&quot;, &quot;b&quot;, &quot;b&quot;, &quot;c&quot;, &quot;a&quot;) | (3,[0,1,2],[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

`NGram` est un transformateur qui génère une séquence d’n-grammes, où un n-gramme est une séquence de jetons (&#39;??&#39;) (généralement des mots) pour certains entiers (`𝑛`). La sortie est composée de chaînes &quot;??&quot; délimitées par des espaces, qui peuvent être utilisées comme fonctionnalités dans les modèles d’apprentissage automatique, en particulier celles axées sur le traitement du langage naturel.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Types des données**

- Type de données d’entrée : Array[String]
- Type de données de sortie : Tableau[Chaîne]

**Définition**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | La longueur minimale de n-gramme doit être supérieure ou égale à 1. | Entier | 2 (fonctions de bigramme) | facultatif |

{style="table-layout:auto"}

**Exemple de transformation**

Cet exemple montre comment le transformateur NGram crée une séquence de 3 grammes à partir d&#39;une liste de jetons dérivés de données textuelles.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Exemple avant et après la transformation n-gramme**

| identifiant | text | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;this&quot;, &quot;was&quot;, &quot;an&quot;, &quot;amusant&quot;, &quot;movie&quot;] | [&quot;c&#39;était un&quot;, &quot;c&#39;était un film divertissant&quot;, &quot;un film divertissant&quot;] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

`StopWordsRemover` est un transformateur qui supprime les mots d’arrêt d’une séquence de chaînes, en éliminant les mots courants qui n’ont pas de signification significative. Elle prend en entrée une séquence de chaînes (comme la sortie d’un jeton) et supprime tous les mots-clés spécifiés par le paramètre `stopWords`.

Cette transformation est utile pour le prétraitement des données texte, ce qui améliore l’efficacité des modèles d’apprentissage automatique en aval en éliminant les mots qui ne contribuent pas beaucoup à la signification globale.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Types des données**

- Type de données d’entrée : Array[String]
- Type de données de sortie : Tableau[Chaîne]

**Définition**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | Les mots à filtrer. | array [string] | Valeur par défaut : mots-clés anglais | facultatif |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**Exemple de transformation**

Cet exemple montre comment le `StopWordsRemover` filtre les mots-clés anglais courants d’une liste de jetons.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Exemple avant et après la suppression de mots vides**

| identifiant | raw | filtré |
|----|------------------------------|--------------------------|
| 0 | [J&#39;ai vu, vu, rouge, ballon] | [scie, rouge, ballon] |
| 1 | [Mary, had, a, small, agneau] | [Marie, petite, agneau] |

**Exemple avec mots d’arrêt personnalisés**

Cet exemple illustre l’utilisation d’une liste personnalisée de mots d’arrêt pour filtrer des mots spécifiques des séquences d’entrée.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Exemple avant et après suppression de mots d’arrêt personnalisés**

| identifiant | raw | filtré |
|----|------------------------------|--------------------------|
| 0 | [J&#39;ai vu, vu, rouge, ballon] | [vu, le, le ballon] |
| 1 | [Mary, had, a, small, agneau] | [Mary, a, small, agneau] |

#### TF-IDF {#tf-idf}

`TF-IDF` (Term Frequency-Inverse Document Frequency) est un transformateur utilisé pour mesurer l’importance d’un mot dans un document par rapport à un corpus. Fréquence des termes (TF) fait référence au nombre de fois où un terme \(t\) apparaît dans un document \(d\), tandis que la fréquence des documents (DF) mesure le nombre de documents dans le corpus \(D\) contenant le terme \(t\). Cette méthode est largement utilisée dans l’extraction de texte pour réduire l’influence des mots courants, tels que &quot;a&quot;, &quot;the&quot; et &quot;of&quot;, qui contiennent peu d’informations uniques.

Cette transformation s’avère particulièrement utile dans les tâches d’extraction de texte et de traitement du langage naturel, dans la mesure où elle attribue une valeur numérique à l’importance de chaque mot dans un document et dans l’ensemble du corpus.

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
| `MIN_DOC_FREQ` | Nombre minimum de documents dans lesquels un terme doit apparaître inclus dans le modèle. | Int | 0 | facultatif |

{style="table-layout:auto"}

**Exemple de transformation**

Cet exemple montre comment utiliser TF-IDF pour transformer des phrases en jetons en un vecteur de fonctionnalités qui représente l’importance de chaque terme dans le contexte du corpus entier.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

`Tokenizer` est un transformateur qui ventile le texte, tel qu’une phrase, en termes individuels, généralement en mots. Il convertit les phrases en tableaux de jetons, ce qui fournit une étape fondamentale du prétraitement de texte qui prépare les données pour d’autres processus d’analyse de texte ou de modélisation.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Types des données**

- Type de données d’entrée : phrase textuelle
- Type de données de sortie : Tableau[Chaîne]

**Définition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Paramètres**

| Paramètre | Description | Type | Par défaut | Facultatif |
|-----------|-------------|------|---------|----------|
| NA | `Tokenizer` ne nécessite aucun paramètre supplémentaire pour son fonctionnement. | NA | NA | NA |

**Exemple de transformation**

Cet exemple montre comment `Tokenizer` ventile des phrases en mots individuels (jetons) dans le cadre d’un pipeline de traitement de texte.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

`Word2Vec` est un estimateur qui traite des séquences de mots représentant des documents et forme un `Word2VecModel`. Ce modèle associe chaque mot à un vecteur de taille fixe unique et convertit chaque document en vecteur en calculant la moyenne des vecteurs de tous les mots du document. Largement utilisée dans les tâches de traitement de langage naturel, `Word2Vec` crée des intégrations de mots qui capturent la signification sémantique, convertissant les données de texte en vecteurs numériques qui représentent les relations entre les mots et permettant une analyse de texte plus efficace et des modèles d’apprentissage automatique.

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
| `VECTOR_SIZE` | Dimension du vecteur dans lequel chaque mot est transformé. | Nombre entier | 100 | facultatif |
| `MIN_COUNT` | Nombre minimum de fois où un jeton doit apparaître inclus dans le vocabulaire du modèle `Word2Vec`. | Nombre entier | 5 | facultatif |

{style="table-layout:auto"}

**Exemple de transformation**

Cet exemple montre comment `Word2Vec` convertit une révision en unités lexicales en vecteur de taille fixe représentant la moyenne des vecteurs de mots dans le document.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Exemple avant et après la transformation Word2Vec**

| review | tokenized | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| c&#39;était un film divertissant. | [ceci, était, un, divertissant, film] | [-0.025713888928294182,0.00818799751577899,0.0092235435731709,-0.01515385233797133,0.012175946310162545,3.1129065901041035E-4,0.0025145105042611252,0.005757019785232843,-0.021328244300093502,0.009335877187550069{1] |

{style="table-layout:auto"}
