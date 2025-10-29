---
title: Filtrage des robots à l’aide des statistiques et du machine learning
description: Découvrez comment utiliser les statistiques Data Distiller et le machine learning pour identifier et filtrer l’activité des robots afin d’assurer des analyses précises et une intégrité des données améliorée.
exl-id: 30d98281-7d15-47a6-b365-3baa07356010
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# Filtrage des robots à l’aide des statistiques et du machine learning

Les applications pratiques du filtrage des robots s&#39;étendent sur plusieurs secteurs d&#39;activité. Dans le commerce électronique, il améliore la fiabilité des mesures de taux de conversion, les sites Web d&#39;actualités peuvent bénéficier de l&#39;atténuation des faux indicateurs d&#39;engagement et les réseaux publicitaires peuvent assurer une facturation équitable. Pour conserver des analyses précises et assurer l’intégrité des données dans les données de parcours de navigation ou de trafic web, vous devez gérer l’activité des robots. Vous pouvez garantir des données d’analyse de haute qualité en utilisant Data Distiller afin d’implémenter un filtrage de robots efficace et d’éliminer le trafic indésirable.

Ce document fournit un guide complet pour identifier et filtrer l’activité des robots à l’aide de SQL et des techniques de machine learning. Il présente une progression d’approches complémentaires, en commençant par le filtrage de base et en passant à la détection et à l’évaluation basées sur le machine learning. Adoptez ce cadre robuste pour améliorer la détection des robots et maintenir l’intégrité de vos données.

## Comprendre l’activité des robots {#understand-bot-activity}

L’activité des robots peut être identifiée en détectant les pics d’actions des utilisateurs dans des intervalles de temps spécifiques. Par exemple, des clics excessifs effectués par un seul utilisateur sur une courte période peuvent indiquer un comportement de robot. Les deux attributs clés utilisés dans le filtrage des robots sont les suivants :

- **ECID (identifiant visiteur Experience Cloud) :** identifiant universel et persistant qui identifie les visiteurs et visiteuses.
- **Horodatage :** l’heure et la date auxquelles une activité se produit sur le site web.

Les exemples ci-dessous montrent comment utiliser le langage SQL et les techniques de machine learning pour identifier, affiner et prédire l’activité des robots. Utilisez ces méthodes pour améliorer l’intégrité de vos données et garantir des analyses exploitables.

## Filtrage des robots basé sur SQL {#sql-based-bot-filtering}

Cet exemple de filtrage de robots basé sur SQL montre comment utiliser des requêtes SQL pour définir des seuils et détecter une activité de robot en fonction de règles prédéfinies. Cette approche fondamentale permet d’identifier les anomalies du trafic web en supprimant les activités inhabituelles. En personnalisant les règles de détection avec des seuils et des intervalles définis, vous pouvez adapter efficacement le filtrage des robots à vos modèles de trafic spécifiques.

### Définir des seuils pour l’activité des robots {#define-thresholds}

Commencez par analyser votre jeu de données pour identifier et catégoriser le comportement des utilisateurs. Concentrez-vous sur des attributs tels que l’ECID, l’horodatage et `webPageDetails.name` (nom de la page web visitée) pour regrouper les actions des utilisateurs et utilisatrices et détecter les modèles indiquant une activité de robots.

La requête SQL ci-dessous montre comment appliquer le seuil de plus de 60 clics en une minute pour identifier une activité suspecte :

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### Étendre à plusieurs intervalles {#expand-to-multiple-intervals}

Définissez ensuite différents intervalles de temps pour les seuils. Ces intervalles peuvent inclure :

- Intervalle de **minutes :** jusqu’à 60 clics.
- Intervalle de **minutes :** jusqu’à 300 clics.
- **Intervalle de 30 minutes :** jusqu’à 1 800 clics.

La requête SQL suivante crée une vue nommée `analytics_events_clicks_count_criteria` pour gérer les seuils sur plusieurs intervalles. L’instruction consolide le nombre de clics pour des intervalles d’une minute, de 5 minutes et de 30 minutes dans un jeu de données structuré et signale l’activité potentielle des robots en fonction de seuils prédéfinis.

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

L’instruction joint les données de `table_count_1_min`, `table_count_5_mins` et `table_count_30_mins` à l’aide de la valeur `mcid` et de la page web. Il consolide ensuite les nombres de clics de chaque utilisateur sur plusieurs intervalles de temps afin de fournir une vue complète de l’activité des utilisateurs. Enfin, la logique de marquage identifie ensuite les utilisateurs et utilisatrices qui dépassent 50 clics en une minute et les marque comme des robots (`isBot = 1`).

### Structure du jeu de données de sortie

Le jeu de données de sortie est structuré avec des champs plats et imbriqués. Cette structure offre une certaine flexibilité lors de la détection du trafic anormal et prend en charge des stratégies de filtrage avancées qui utilisent SQL et le machine learning. Les champs imbriqués incluent des `count` et des `web` qui encapsulent des détails granulaires sur les seuils d’activité et les pages web. La capture de ces mesures signifie que les fonctionnalités peuvent être facilement extraites pour les tâches d’entraînement et de prévision.

Le diagramme de schéma suivant décrit la structure du jeu de données généré et met en évidence la manière dont les champs imbriqués et plats peuvent être utilisés pour un traitement et une détection des robots efficaces.

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### Jeu de données de sortie à utiliser pour l’apprentissage

Le résultat de cette expression peut ressembler au tableau fourni ci-dessous. Dans le tableau, la colonne `isBot` sert de libellé pour faire la distinction entre les activités robots et non robots.

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## Fonctions statistiques avancées pour le filtrage des robots {#statistical-functions-for-bot-filtering}

Ce deuxième exemple s’appuie sur le filtrage SQL de base en incorporant des techniques de machine learning pour affiner les seuils et améliorer la précision du filtrage. En utilisant des fonctions statistiques avancées, telles que l’analyse de régression ou les algorithmes de mise en grappe, cette approche introduit des fonctionnalités prédictives que vous pouvez utiliser pour développer des modèles permettant de gérer des jeux de données complexes avec une plus grande précision.

### Créer un jeu de données de formation {#build-a-training-dataset}

Tout d’abord, préparez un jeu de données avec des structures plates et imbriquées que le modèle de machine learning peut utiliser (comme décrit ci-dessus). Vous trouverez plus d’informations sur la façon de procéder dans la [documentation relative à l’utilisation de structures de données imbriquées](../../key-concepts/nested-data-structures.md). Regroupez les données par date et heure, ID utilisateur et nom de page web pour identifier les modèles dans les activités de robots.

### Utilisation des clauses TRANSFORM et OPTIONS pour la création de modèles {#transform-and-preprocess}

Pour transformer votre jeu de données et configurer votre modèle de machine learning efficacement, procédez comme suit. Les étapes détaillent comment gérer les valeurs nulles, préparer les fonctions et définir les paramètres du modèle pour des performances optimales.

>[!TIP]
>
>Pour en savoir plus sur l’utilisation des transformations et le prétraitement des données, consultez la documentation [Techniques de transformation des fonctions](../feature-transformation.md).

1. Pour remplir des valeurs nulles dans des colonnes numériques, de chaîne et booléennes, utilisez respectivement des fonctions `numeric_imputer`, `string_imputer` et `boolean_imputer`. Cette étape permet à l’algorithme de machine learning de traiter les données sans erreurs.
2. Appliquez des transformations de fonction pour préparer les données pour la modélisation. Appliquez des `binarized`, des `quantile_discretizer` ou des `string_indexer` pour classer ou normaliser les colonnes. Ensuite, alimentez la sortie des imputeurs (`numeric_imputer` et `string_imputer`) dans des transformateurs ultérieurs tels que `string_indexer` ou `quantile_discretizer` pour créer des caractéristiques significatives.
3. Utilisez la fonction `vector_assembler` pour combiner les colonnes transformées en une seule colonne de fonction. Mettez ensuite à l’échelle les fonctions à l’aide de `min_max_scaler` pour normaliser les valeurs afin d’améliorer les performances du modèle. Remarque : dans l’exemple SQL, la dernière transformation mentionnée dans la clause TRANSFORM devient la colonne de fonction utilisée par le modèle de machine learning.
4. Spécifiez le type de modèle et tout autre hyperparamètre de la clause OPTIONS. Par exemple, `decision_tree_classifier` a été choisi ici, car il s’agit d’un problème de classification. D’autres paramètres tels que `max_depth` ont été ajustés (`MAX_DEPTH=4`) pour ajuster le modèle afin d’obtenir de meilleures performances.
5. Combinez les fonctionnalités et libellez les données de sortie. Utilisez la clause SELECT pour spécifier le jeu de données pour l’entraînement. Cette clause doit inclure les colonnes de fonction (`count_per_id`, `web`, `id`) et la colonne de libellé (`isBot`), qui indique si une action est susceptible d’être un robot.

Votre instruction peut ressembler à l’exemple ci-dessous.

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**Résultat**

Dans les résultats affichés ci-dessous, le modèle `bot_filtering_model` est créé avec succès avec un identifiant, un nom et une version uniques. Cette sortie sert de référence pour le suivi et la gestion des modèles. Utilisez ces références pour identifier la configuration et la version exactes requises pour les prédictions ou les évaluations.

```console
           Created Model ID           |       Created Model       | Version
|--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### Évaluation du modèle formé {#evaluate-trained-model}

Après avoir créé le modèle, utilisez la commande `MODEL_EVALUATE` pour évaluer ses performances. Cette étape permet de s’assurer que le modèle répond aux exigences de précision et de performance pour détecter l’activité des robots.

Utilisez les arguments suivants dans votre commande SQL pour évaluer le modèle :

1. Spécifiez le nom du modèle (`bot_filtering_model`) pour indiquer le modèle à évaluer. Ce nom doit correspondre à celui que vous avez créé précédemment avec la commande `CREATE MODEL`.
2. Indiquez la version du modèle (`1`) dans le deuxième argument pour spécifier la version du modèle que vous souhaitez évaluer. S’il existe plusieurs versions, cela permet de s’assurer que la version correcte est utilisée.
3. Incluez le jeu de données d’évaluation pour définir le jeu de données à évaluer. Assurez-vous que le jeu de données inclut les mêmes colonnes de fonctionnalités (`count_per_id`, `web`, `id`) et la même colonne de libellés (`isBot`) que celles utilisées pendant l’entraînement.

>[!NOTE]
>
>Les transformations appliquées lors de l’entraînement des modèles sont automatiquement appliquées lors de l’évaluation.

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**Résultat**

La réponse inclut des mesures telles que la précision, la précision, le rappel et l’AUC-ROC. Les résultats confirment si le modèle fonctionne bien ou non.

>[!NOTE]
>
>Les valeurs comprises entre 0 et 1 représentent des proportions ou des probabilités, 1,0 indiquant une performance parfaite.

```console
auc_roc | accuracy | precision | recall
|---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **Mesure** | **Description** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | Cette mesure indique l’efficacité avec laquelle votre modèle peut classer les robots et les non-robots. Il est largement utilisé pour évaluer les modèles de classification. |
| `accuracy` | Pourcentage de prédictions correctes faites par le modèle. |
| `precision` | La proportion de vraies prédictions de robots parmi tous les robots prédits. |
| `recall` | Proportion de vrais robots détectés sur tous les robots réels. |

>[!TIP]
>
>Pour une utilisation sur les sandbox de production, pensez à évaluer le modèle sur des jeux de données de test pour vous assurer qu’il se généralise efficacement.

### Prédire l’activité des robots {#predict-bot-activity}

Utilisez la commande `MODEL_PREDICT` avec le modèle formé pour identifier les utilisateurs (`id`) qui sont des robots. Pour générer des prédictions permettant d’identifier l’activité des robots, procédez comme suit :

1. Utilisez le nom du modèle (`bot_filtering_model`) dans le premier argument pour spécifier le modèle à utiliser pour les prédictions.
2. Spécifiez la version du modèle (`1`) dans le deuxième argument pour vous assurer que la version correcte du modèle est utilisée.
3. Pour fournir les données correctes pour les prédictions, utilisez une instruction SELECT pour spécifier les colonnes de caractéristiques (`count_per_id`, `web`, `id`). N’incluez pas la colonne de libellé (`isBot`), car le modèle générera des prédictions pour ce champ.

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**Résultat**

La réponse inclut des prédictions pour chaque utilisateur (`id`), ainsi que des détails sur son activité et le résultat de classification du modèle. Cette sortie permet un examen détaillé du comportement des utilisateurs et de la classification de l’activité des robots par le modèle.

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
|---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

Le tableau ci-dessous explique chaque mesure :

| Nom de la colonne | Description |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | Identifiant unique de chaque utilisateur. |
| `count.one_minute` | Le nombre de clics agrégés est calculé pour des intervalles d’une minute. |
| `count.five_minute` | Le nombre de clics agrégés est calculé pour des intervalles de 5 minutes. |
| `count.thirty_minute` | Les clics agrégés sont comptabilisés pendant des intervalles de 30 minutes. |
| `web.webpagedetails.name` | Nom de la page web visitée. Cela fournit un contexte pour l’activité des utilisateurs et utilisatrices. |
| `prediction` | La prédiction du modèle. Un résultat `1.0` indique que l’utilisateur est marqué comme un robot en fonction de ses modèles d’activité. |

## Gestion des modèles {#manage-models}

Pour gérer vos modèles de machine learning, utilisez les mots-clés SQL répertoriés dans la section ci-dessous.

### Liste des modèles disponibles {#list-available-models}

Gérez et examinez efficacement les modèles à l’aide de la commande `SHOW MODELS;`. Cette commande répertorie tous les modèles de machine learning qui ont été créés dans l’espace de travail actuel. La sortie fournit un aperçu des modèles disponibles et inclut leurs noms, versions et autres métadonnées.

```sql
SHOW MODELS;
```

### Suppression de modèles {#delete-models}

Pour libérer des ressources et s’assurer que seuls les modèles appropriés sont conservés, utilisez la commande `DROP MODEL` pour supprimer les modèles obsolètes ou inutiles. Cette commande supprime tout modèle de machine learning spécifié après les mots clés. Dans l’exemple ci-dessous, le `bot_filtering_model` est supprimé du système.

```sql
DROP MODEL bot_filtering_model;
```

## Étapes suivantes

En lisant ce document, vous avez appris à identifier et à filtrer l’activité des robots à l’aide de SQL et des techniques de machine learning à l’aide des méthodes Data Distiller. Ensuite, appliquez ces concepts à vos jeux de données et automatisez le recyclage des modèles pour une amélioration continue.
