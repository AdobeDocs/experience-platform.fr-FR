---
title: Modèles
description: Gestion du cycle de vie des modèles avec l’extension Data Distiller SQL. Découvrez comment créer, entraîner et gérer des modèles statistiques avancés à l’aide de SQL, y compris des processus clés tels que le contrôle de version, l’évaluation et la prédiction des modèles, afin d’obtenir des informations exploitables à partir de vos données.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 09129d9d19816b4d93b4979305f4ad532e5ffde4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 1%

---

# Modèles

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Distiller de données. Pour plus d’informations, contactez votre représentant ou représentante Adobe.

Query Service prend désormais en charge les processus principaux de création et de déploiement d’un modèle. Vous pouvez utiliser SQL pour entraîner le modèle à l’aide de vos données, évaluer sa précision, puis utiliser le modèle entraîné pour faire des prédictions sur de nouvelles données. Vous pouvez ensuite utiliser le modèle pour généraliser à partir de vos données antérieures afin de prendre des décisions éclairées concernant les scénarios du monde réel.

Les trois étapes du cycle de vie du modèle pour générer des informations exploitables sont les suivantes :

1. **Formation** : le modèle apprend des modèles à partir du jeu de données fourni. (créer ou remplacer un modèle)
2. **Test/Évaluation** : les performances du modèle sont évaluées à l’aide d’un jeu de données distinct. (`model_evaluate`)
3. **Prédiction** : le modèle entraîné est utilisé pour effectuer des prédictions sur de nouvelles données non vues.

Utilisez l’extension SQL du modèle, ajoutée à la grammaire SQL existante, pour gérer le cycle de vie du modèle en fonction des besoins de votre entreprise. Ce document couvre le langage SQL requis pour créer ou remplacer un modèle, entraîner, évaluer, recycler si nécessaire et prédire des informations.

## Création de modèles et formation {#create-and-train}

Découvrez comment définir, configurer et entraîner un modèle de machine learning à l’aide de commandes SQL. Le code SQL ci-dessous montre comment créer un modèle, appliquer des transformations d’ingénierie des fonctionnalités et lancer le processus d’entraînement pour s’assurer que le modèle est correctement configuré pour une utilisation ultérieure. Les commandes SQL suivantes détaillent les différentes options de création et de gestion de modèles :

- **CREATE MODEL** : crée et entraîne un nouveau modèle sur un jeu de données spécifié. Si un modèle portant le même nom existe déjà, cette commande renvoie une erreur.
- **CREATE MODEL IF NOT EXISTS** : crée et entraîne un nouveau modèle uniquement si un modèle portant le même nom n’existe pas déjà sur le jeu de données spécifié.
- **CRÉER OU REMPLACER LE MODÈLE** : permet de créer et d’entraîner un modèle, en remplaçant la dernière version d’un modèle existant portant le même nom sur le jeu de données spécifié.

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**Exemple**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

Pour mieux comprendre les composants et les configurations clés du processus de création et d’entraînement de modèle, les notes suivantes expliquent l’objectif et la fonction de chaque élément dans l’exemple SQL ci-dessus.

- `<model_alias>` : l’alias du modèle est un nom réutilisable attribué au modèle, qui peut être référencé ultérieurement. Il est nécessaire de donner un nom à votre modèle.
- `transform` : la clause de transformation est utilisée pour appliquer des transformations d’ingénierie des fonctionnalités (par exemple, un codage à une seule touche et l’indexation des chaînes) au jeu de données avant d’entraîner le modèle. La dernière clause de l&#39;instruction `TRANSFORM` doit être soit une `vector_assembler` avec une liste de colonnes qui composerait les fonctions pour l&#39;entraînement du modèle, soit un type dérivé de la `vector_assembler` (par exemple `max_abs_scaler(feature)`, `standard_scaler(feature)`, etc.). Seules les colonnes mentionnées dans la dernière clause seront utilisées pour la formation ; toutes les autres colonnes, même si elles sont incluses dans la requête `SELECT`, seront exclues.
- `label = <label-COLUMN>` : colonne de libellé du jeu de données d’entraînement qui spécifie la cible ou le résultat que le modèle vise à prédire.
- `training-dataset` : cette syntaxe sélectionne les données utilisées pour entraîner le modèle.
- `type = 'LogisticRegression'` : cette syntaxe spécifie le type d’algorithme de machine learning à utiliser. Les options incluent `LinearRegression`, `LogisticRegression` et `KMeans`.
- `options` : ce mot-clé fournit un ensemble flexible de paires clé-valeur pour configurer le modèle.
   - `Key model_type` : `model_type = '<supported algorithm>'` indique le type d’algorithme de machine learning à utiliser. Les options prises en charge sont les suivantes : `LinearRegression`, `LogisticRegression` et `KMeans`.
   - `Key label` : `label = <label_COLUMN>` : définit la colonne de libellé dans le jeu de données d’entraînement, qui indique la cible ou le résultat que le modèle vise à prédire.

Utilisez SQL pour référencer le jeu de données utilisé pour l’entraînement.

>[!TIP]
>
>Pour plus d’informations sur la clause `TRANSFORM`, y compris sur les fonctions prises en charge et leur utilisation dans les `CREATE MODEL` et les `CREATE TABLE`, consultez la clause [`TRANSFORM` dans la documentation sur la syntaxe SQL](../sql/syntax.md#transform).

## Mise à jour d’un modèle {#update}

Découvrez comment mettre à jour un modèle de machine learning existant en appliquant de nouvelles transformations d’ingénierie des fonctionnalités et en configurant des options telles que le type d’algorithme et la colonne de libellé. Chaque mise à jour crée une nouvelle version du modèle, incrémentée à partir de la dernière version. Cela permet de s’assurer que les modifications sont suivies et que le modèle peut être réutilisé dans les étapes d’évaluation ou de prévision futures.

L’exemple suivant illustre la mise à jour d’un modèle avec de nouvelles transformations et options :

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**Exemple**

Pour mieux comprendre le processus de contrôle de version, utilisez la commande suivante :

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

Une fois cette commande exécutée, le modèle possède une nouvelle version, comme illustré dans le tableau ci-dessous :

| ID de modèle mis à jour | Modèle mis à jour | Nouvelle version |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

Les notes suivantes expliquent les composants et options clés du workflow de mise à jour du modèle.

- `UPDATE model <model_alias>` : la commande de mise à jour gère le contrôle de version et crée une version de modèle incrémentée à partir de la dernière version.
- `version` : mot-clé facultatif utilisé uniquement lors des mises à jour pour spécifier explicitement qu’une nouvelle version doit être créée. En cas d’omission, le système incrémente automatiquement la version.

### Prévisualiser et conserver les fonctions transformées {#preview-transform-output}

Utilisez la clause `TRANSFORM` dans les instructions `CREATE TABLE` et `CREATE TEMP TABLE` pour prévisualiser et conserver la sortie des transformations de fonction avant l&#39;entraînement du modèle. Cette amélioration permet de comprendre comment les fonctions de transformation (telles que le codage, la segmentation en unités lexicales et l’assembleur vectoriel) sont appliquées à votre jeu de données.

En matérialisant les données transformées dans une table autonome, vous pouvez inspecter les fonctions intermédiaires, valider la logique de traitement et garantir la qualité des fonctions avant de créer un modèle. Cela améliore la transparence sur l’ensemble du pipeline de machine learning et permet une prise de décision plus éclairée lors du développement du modèle.

#### Syntaxe {#syntax}

Utilisez la clause `TRANSFORM` dans une instruction `CREATE TABLE` ou `CREATE TEMP TABLE` comme illustré ci-dessous :

```sql
CREATE TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

Ou :

```sql
CREATE TEMP TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

**Exemple**

Créez un tableau à l’aide de transformations de base :

```sql
CREATE TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review;
```

Créez une table temporaire à l&#39;aide d&#39;étapes d&#39;ingénierie de fonctionnalités supplémentaires :

```sql
CREATE TEMP TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

Interrogez ensuite la sortie :

```sql
SELECT * FROM ctas_transform_table LIMIT 1;
```

#### Considérations importantes {#considerations}

Bien que cette fonction améliore la transparence et prenne en charge la validation des fonctionnalités, il existe d’importantes limites à prendre en compte lors de l’utilisation de la clause `TRANSFORM` en dehors de la création du modèle.

- **Sorties vectorielles** : si la transformation génère des sorties de type vecteur, elles sont automatiquement converties en tableaux.
- **Limitation de la réutilisation par lots** : les tables créées avec `TRANSFORM` ne peuvent appliquer des transformations que lors de la création des tables. Les nouveaux lots de données insérés avec `INSERT INTO` ne sont **pas automatiquement transformés**. Pour appliquer la même logique de transformation aux nouvelles données, vous devez recréer la table à l’aide d’une nouvelle instruction `CREATE TABLE AS SELECT` (CTAS).
- **Limitation de la réutilisation des modèles** : les tables créées à l’aide de `TRANSFORM` ne peuvent pas être directement utilisées dans les instructions `CREATE MODEL`. Vous devez redéfinir la logique de `TRANSFORM` lors de la création du modèle. Les transformations qui produisent des sorties de type vecteur ne sont pas prises en charge pendant l&#39;entraînement du modèle. Pour plus d’informations, voir [Types de données de sortie de transformation de fonction](./feature-transformation.md#available-transformations).

>[!NOTE]
>
>Cette fonctionnalité est conçue pour l’inspection et la validation. Il ne remplace pas la logique de pipeline réutilisable. Toutes les transformations destinées à une entrée de modèle doivent être explicitement redéfinies à l’étape de création de modèle.

## Évaluer les modèles {#evaluate-model}

Pour garantir des résultats fiables, évaluez la précision et l’efficacité du modèle avant de le déployer pour les prédictions avec le mot-clé `model_evaluate`. L’instruction SQL ci-dessous spécifie un jeu de données de test, des colonnes spécifiques et la version du modèle pour tester le modèle en évaluant ses performances.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test_dataset)
```

La fonction `model_evaluate` prend `model-alias` comme premier argument et une instruction `SELECT` flexible comme deuxième argument. Query Service exécute d’abord l’instruction `SELECT` et mappe les résultats à la `model_evaluate` fonction définie par Adobe (ADF). Le système s’attend à ce que les noms des colonnes et les types de données dans le résultat de l’instruction `SELECT` correspondent à ceux utilisés dans l’étape d’entraînement. Ces noms de colonne et types de données sont traités comme des données de test et des données d’étiquette pour l’évaluation.

>[!IMPORTANT]
>
>Lors de l’évaluation (`model_evaluate`) et de la prévision (`model_predict`), la ou les transformations effectuées au moment de la formation sont utilisées.

## Prédiction {#predict}

>[!IMPORTANT]
>
>La sélection améliorée des colonnes et le crénelage des `model_predict` sont contrôlés par un indicateur de fonction. Par défaut, les champs intermédiaires tels que `probability` et `rawPrediction` ne sont pas inclus dans la sortie de prédiction.\
>Pour permettre l&#39;accès à ces champs intermédiaires, exécutez la commande suivante avant d&#39;exécuter `model_predict` :
>
>`set advanced_statistics_show_hidden_fields=true;`

Utilisez le mot-clé `model_predict` pour appliquer le modèle et la version spécifiés à un jeu de données et générer des prédictions. Vous pouvez sélectionner toutes les colonnes de sortie, en choisir des spécifiques ou attribuer des alias pour améliorer la clarté de la sortie.

Par défaut, seules les colonnes de base et la prédiction finale sont renvoyées, sauf si l’indicateur de fonctionnalité est activé.

```sql
SELECT * FROM model_predict(model-alias, version-number, SELECT col1, col2 FROM dataset);
```

### Sélectionner des champs de sortie spécifiques {#select-specific-output-fields}

Lorsque l’indicateur de fonctionnalité est activé, vous pouvez récupérer un sous-ensemble de champs à partir de la sortie `model_predict`. Utilisez ceci pour récupérer des résultats intermédiaires, tels que les probabilités de prédiction, les scores de prédiction bruts et les colonnes de base à partir de la requête d’entrée.

**Cas 1 : renvoyer tous les champs de sortie disponibles**

```sql
SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Cas 2 : renvoi des colonnes sélectionnées**

```sql
SELECT a, b, c, probability, predictionCol FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Cas 3 : renvoi des colonnes sélectionnées avec des alias**

```sql
SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

Dans chaque cas, le `SELECT` externe contrôle les champs de résultat renvoyés. Il s’agit notamment des champs de base de la requête d’entrée, ainsi que des sorties de prédiction telles que `probability`, `rawPrediction` et `predictionCol`.

### Conserver les prédictions à l’aide de CREATE TABLE ou INSERT INTO

Vous pouvez conserver des prédictions en utilisant « CREATE TABLE AS SELECT » ou « INSERT INTO SELECT », y compris les sorties de prédiction, le cas échéant.

**Exemple : Créer une table avec tous les champs de sortie de prédiction**

```sql
CREATE TABLE scored_data AS SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Exemple : insérer les champs de sortie sélectionnés avec des alias**

```sql
INSERT INTO scored_data SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

Vous pouvez ainsi sélectionner et conserver uniquement les champs de sortie de prédiction et les colonnes de base appropriés pour les analyses ou les rapports en aval.

## Évaluation et gestion des modèles

Utilisez la commande `SHOW MODELS` pour répertorier tous les modèles disponibles que vous avez créés. Utilisez-le pour afficher les modèles qui ont été entraînés et qui sont disponibles pour évaluation ou prédiction. Lorsqu’elles sont interrogées, les informations sont récupérées à partir du référentiel de modèles qui est mis à jour lors de la création du modèle. Les détails renvoyés sont les suivants : ID de modèle, nom du modèle, version, jeu de données source, détails de l’algorithme, options/paramètres, heure de création/mise à jour et utilisateur ou utilisatrice qui a créé le modèle.

```sql
SHOW MODELS;
```

Les résultats apparaissent dans un tableau similaire à celui ci-dessous :

| model-id | model-name | version | source-jeu de données | type | options | transformer | champs | created | mis à jour | créé PAR |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1.0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[« name », « gender »\] | 14/08/2024 10:30 | 14/08/2024 11:00 | `JohnSnow@adobe.com` |

## Nettoyage et maintenance des modèles

Utilisez la commande `DROP MODELS` pour supprimer les modèles que vous avez créés dans le registre des modèles. Vous pouvez l’utiliser pour supprimer les modèles obsolètes, inutilisés ou indésirables. Cela libère des ressources et garantit que seuls les modèles pertinents sont conservés. Vous pouvez également inclure un nom de modèle facultatif pour améliorer la spécificité. Le modèle est uniquement abandonné avec la version de modèle fournie.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous comprenez la syntaxe SQL de base requise pour créer, entraîner et gérer des modèles approuvés à l’aide de Data Distiller. Explorez ensuite le document [Implémenter des modèles statistiques avancés](./implement-models/implement-models.md) pour en savoir plus sur les différents modèles approuvés disponibles et sur la manière de les implémenter efficacement dans vos workflows SQL. Si ce n’est pas déjà fait, consultez le document [Ingénierie des fonctionnalités](./feature-engineering.md) pour vous assurer que vos données sont préparées de manière optimale pour la formation des modèles.
