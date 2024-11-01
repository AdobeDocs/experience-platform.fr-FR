---
title: Modèles
description: Gestion du cycle de vie du modèle avec l’extension SQL de Data Distiller. Découvrez comment créer, former et gérer des modèles statistiques avancés à l’aide de SQL, y compris des processus clés tels que le contrôle de version, l’évaluation et la prédiction des modèles, afin d’obtenir des informations exploitables de vos données.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 1%

---

# Modèles

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Data Distiller. Pour en savoir plus, contactez votre représentant ou représentante Adobe.

Query Service prend désormais en charge les processus principaux de création et de déploiement d’un modèle. Vous pouvez utiliser SQL pour entraîner le modèle à l’aide de vos données, évaluer sa précision, puis appliquer le modèle de formation pour faire des prédictions sur de nouvelles données. Vous pouvez ensuite utiliser le modèle pour généraliser à partir de vos données antérieures afin de prendre des décisions éclairées sur les scénarios du monde réel.

Les trois étapes du cycle de vie du modèle pour générer des informations exploitables sont les suivantes :

1. **Formation** : le modèle apprend des modèles à partir du jeu de données fourni. (créer ou remplacer un modèle)
2. **Tests/évaluation** : les performances du modèle sont évaluées à l’aide d’un jeu de données distinct. (`model_evaluate`)
3. **Prédiction** : le modèle formé est utilisé pour faire des prédictions sur de nouvelles données invisibles.

Utilisez l’extension SQL de modèle, ajoutée à la grammaire SQL existante, pour gérer le cycle de vie du modèle en fonction des besoins de votre entreprise. Ce document couvre le langage SQL nécessaire pour créer ou remplacer un modèle, entraîner, évaluer, reformer si nécessaire et prédire les insights.

## Création et formation de modèles {#create-and-train}

Découvrez comment définir, configurer et entraîner un modèle d’apprentissage automatique à l’aide de commandes SQL. Le code SQL ci-dessous indique comment créer un modèle, appliquer des transformations d’ingénierie de fonctionnalités et lancer le processus de formation pour s’assurer que le modèle est correctement configuré pour une utilisation ultérieure. Les commandes SQL suivantes détaillent les différentes options de création et de gestion de modèles :

- **CREATE MODEL** : crée et forme un nouveau modèle sur un jeu de données spécifié. Si un modèle portant le même nom existe déjà, cette commande renvoie une erreur.
- **CRÉER UN MODÈLE SI NON EXISTE** : crée et entraîne un nouveau modèle uniquement si un modèle portant le même nom n’existe pas déjà sur le jeu de données spécifié.
- **CRÉER OU REMPLACER LE MODÈLE** : crée et entraîne un modèle, en remplaçant la dernière version d’un modèle existant par le même nom sur le jeu de données spécifié.

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

Pour vous aider à comprendre les composants et configurations clés dans le processus de création et d’entraînement de modèle, les notes suivantes expliquent l’objectif et la fonction de chaque élément dans l’exemple SQL ci-dessus.

- `<model_alias>` : l’alias du modèle est un nom réutilisable attribué au modèle, qui peut être référencé ultérieurement. Il est nécessaire de donner un nom à votre modèle.
- `transform` : la clause de transformation est utilisée pour appliquer des transformations d’ingénierie de fonctionnalités (par exemple, un encodage à chaud et l’indexation de chaîne) au jeu de données avant de former le modèle. La dernière clause de l’instruction `TRANSFORM` doit être soit une `vector_assembler` avec une liste de colonnes qui composerait les fonctionnalités pour la formation de modèle, soit un type dérivé de `vector_assembler` (par exemple `max_abs_scaler(feature)`, `standard_scaler(feature)`, etc.). Seules les colonnes mentionnées dans la dernière clause seront utilisées pour la formation ; toutes les autres colonnes, même si elles sont incluses dans la requête `SELECT`, seront exclues.
- `label = <label-COLUMN>` : colonne d’étiquette du jeu de données d’entraînement qui spécifie la cible ou le résultat que le modèle vise à prédire.
- `training-dataset` : cette syntaxe sélectionne les données utilisées pour former le modèle.
- `type = 'LogisticRegression'` : cette syntaxe spécifie le type d’algorithme d’apprentissage automatique à utiliser. Les options incluent `LinearRegression`, `LogisticRegression` et `KMeans`.
- `options` : ce mot-clé fournit un ensemble flexible de paires clé-valeur pour configurer le modèle.
   - `Key model_type` : `model_type = '<supported algorithm>'` : spécifie le type d’algorithme d’apprentissage automatique à utiliser. Les options prises en charge sont `LinearRegression`, `LogisticRegression` et `KMeans`.
   - `Key label` : `label = <label_COLUMN>` : définit la colonne d’étiquette dans le jeu de données d’entraînement, qui indique la cible ou le résultat que le modèle vise à prédire.

Utilisez SQL pour référencer le jeu de données utilisé pour l’entraînement.

## Mettre à jour un modèle {#update}

Découvrez comment mettre à jour un modèle d’apprentissage automatique existant en appliquant de nouvelles transformations d’ingénierie de fonctionnalités et en configurant des options telles que le type d’algorithme et la colonne d’étiquettes. Le code SQL ci-dessous indique comment augmenter le numéro de version du modèle avec chaque mise à jour et s’assurer que les modifications sont suivies afin que le modèle puisse être réutilisé dans les étapes d’évaluation ou de prédiction futures.

```sql
UPDATE model <model_alias> transform( one_hot_encoder(NAME) ohe_name, string_indexer(gender) gendersi) options ( type = 'LogisticRegression', label = <label-COLUMN>, ) ASSELECT col1,
       col2,
       col3
FROM   training-dataset.
```

Pour vous aider à comprendre comment gérer efficacement les versions de modèle et appliquer des transformations, les notes suivantes expliquent les composants et options clés du processus de mise à jour du modèle.

- `UPDATE model <model_alias>` : la commande update gère le contrôle de version et augmente le numéro de version du modèle avec chaque mise à jour.
- `version` : mot-clé facultatif utilisé uniquement lors des mises à jour pour créer une version du modèle.

## Évaluation des modèles {#evaluate-model}

Pour garantir des résultats fiables, évaluez la précision et l’efficacité du modèle avant de le déployer pour des prédictions avec le mot-clé `model_evaluate`. L’instruction SQL ci-dessous spécifie un jeu de données de test, des colonnes spécifiques et la version du modèle pour tester le modèle en évaluant ses performances.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

La fonction `model_evaluate` prend `model-alias` comme premier argument et une instruction `SELECT` flexible comme second argument. Query Service exécute d’abord l’instruction `SELECT` et mappe les résultats à la fonction définie par l’Adobe `model_evaluate` (ADF). Le système attend des noms de colonne et des types de données dans le résultat de l’instruction `SELECT` qu’ils correspondent à ceux utilisés à l’étape de formation. Ces noms de colonne et types de données sont traités comme des données de test et des données d’étiquette à des fins d’évaluation.

>[!IMPORTANT]
>
>Lors de l’évaluation (`model_evaluate`) et de la prédiction (`model_predict`), la ou les transformations effectuées au moment de l’entraînement sont utilisées.

## Prédiction {#predict}

Ensuite, utilisez le mot-clé `model_predict` pour appliquer le modèle et la version spécifiés à un jeu de données et générer des prédictions pour les colonnes sélectionnées. Le code SQL ci-dessous illustre ce processus, indiquant comment prévoir les résultats à l’aide de l’alias et de la version du modèle.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict` accepte l’alias de modèle comme premier argument et une instruction `SELECT` flexible comme second argument. Query Service exécute d’abord l’instruction `SELECT` et mappe les résultats à l’ADF `model_predict`. Le système s’attend à ce que les noms de colonne et les types de données dans le résultat de l’instruction `SELECT` correspondent à ceux de l’étape de formation. Ces données sont ensuite utilisées pour la notation et la génération de prédictions.

>[!IMPORTANT]
>
>Lors de l’évaluation (`model_evaluate`) et de la prédiction (`model_predict`), la ou les transformations effectuées au moment de l’entraînement sont utilisées.

## Évaluation et gestion de vos modèles

Utilisez la commande `SHOW MODELS` pour répertorier tous les modèles disponibles que vous avez créés. Utilisez-le pour afficher les modèles qui ont été formés et qui sont disponibles pour l’évaluation ou la prédiction. Lorsqu’elles sont interrogées, les informations sont récupérées à partir du référentiel de modèles qui est mis à jour lors de la création du modèle. Les détails renvoyés sont les suivants : ID de modèle, nom du modèle, version, jeu de données source, détails de l’algorithme, options/paramètres, heure de création/mise à jour et l’utilisateur qui a créé le modèle.

```sql
SHOW MODELS;
```

Les résultats apparaissent dans un tableau similaire à celui illustré ci-dessous :

| model-id | model-name | version | source-dataset | type | options | transform | fields | created | mis à jour | created BY |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1.0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[&quot;name&quot;, &quot;gender&quot;\] | 2024-08-14 10h30 | 2024-08-14 11 h | `JohnSnow@adobe.com` |

## Nettoyer et gérer vos modèles

Utilisez la commande `DROP MODELS` pour supprimer les modèles que vous avez créés du registre des modèles. Vous pouvez l’utiliser pour supprimer des modèles obsolètes, inutilisés ou indésirables. Cela libère des ressources et garantit que seuls les modèles pertinents sont conservés. Vous pouvez également inclure un nom de modèle facultatif pour une plus grande précision. Cela supprime uniquement le modèle avec la version de modèle fournie.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Étapes suivantes

Après avoir lu ce document, vous comprenez désormais la syntaxe SQL de base requise pour créer, former et gérer des modèles approuvés à l’aide de Data Distiller. Explorez ensuite le [document Mise en oeuvre de modèles statistiques avancés](./implement-models/implement-models.md) pour en savoir plus sur les différents modèles de confiance disponibles et sur la manière de les mettre en oeuvre efficacement dans vos workflows SQL. Si vous ne l’avez pas déjà fait, veillez à consulter le document [Feature Engineering](./feature-engineering.md) pour vous assurer que vos données sont parfaitement préparées pour la formation de modèles.
