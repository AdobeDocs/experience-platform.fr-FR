---
title: Calcul des statistiques des jeux de données
description: Ce document décrit comment calculer les statistiques au niveau des colonnes sur les jeux de données Azure Data Lake Storage (ADLS) avec des commandes SQL.
exl-id: 66f11cd4-b115-40b8-ba8a-c4bb3606bbbf
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 100%

---

# Calcul des statistiques des jeux de données

Vous pouvez désormais calculer les statistiques au niveau des colonnes sur les jeux de données [!DNL Azure Data Lake Storage] (ADLS) avec la commande SQL `COMPUTE STATISTICS`. Les commandes SQL qui calculent les statistiques des jeux de données sont une extension de la commande `ANALYZE TABLE`. Vous trouverez des détails complets sur la commande `ANALYZE TABLE` dans la [documentation de référence SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Les statistiques calculées sont stockées dans des tables temporaires dont la persistance est limitée au niveau de la session. Vous pouvez accéder aux résultats des calculs à tout moment au cours de la session en cours. Elles ne sont pas accessibles dans différentes sessions PSQL.

Pour afficher les statistiques qui ont été calculées avec la commande `ANALYZE TABLE COMPUTE STATISTICS`, utilisez une requête SELECT sur le nom d’alias ou l’identifiant de statistiques. Vous pouvez également limiter la portée de l’analyse statistique à l’ensemble du jeu de données, à un sous-ensemble d’un jeu de données, à toutes les colonnes ou à un sous-ensemble de colonnes.

>[!IMPORTANT]
>
>Les commandes `COMPUTE STATISTICS`, `FILTERCONTEXT` et `FOR COLUMNS` ne sont pas prises en charge sur les tables du magasin accéléré. Ces extensions pour la commande `ANALYZE TABLE` ne sont actuellement prises en charge que pour les tables ADLS. Pour plus d’informations, voir la [section TABLE D’ANALYSE](../sql/syntax.md#analyze-table) du guide de syntaxe SQL.

Ce guide vous aide à structurer vos requêtes afin que vous puissiez calculer les statistiques de colonnes d’un jeu de données ADLS. À l’aide de ces commandes, vous pouvez afficher les statistiques générées dans votre session via un client PSQL à l’aide d’une requête SQL.

## Calcul des statistiques {#compute-statistics}

D’autres éléments ont été ajoutés à la commande `ANALYZE TABLE` qui vous permettent de **calculer les statistiques pour un sous-ensemble d’un jeu de données et pour certaines colonnes**. Pour calculer les statistiques d’un jeu de données, vous devez utiliser le format `ANALYZE TABLE <tableName> COMPUTE STATISTICS`.

>[!IMPORTANT]
>
>Le comportement par défaut calcule les statistiques pour le **jeu de données complet** et pour **toutes les colonnes**. Pour calculer les statistiques sur toutes les colonnes, vous devez utiliser le format de requête `ANALYZE TABLE COMPUTE STATISTICS`. Nous vous recommandons de ne **pas** utiliser la commande `COMPUTE STATISTICS` sur un jeu de données ADLS, car la taille du jeu de données peut être très importante (potentiellement des pétaoctets de données). Vous devez toujours envisager d’exécuter la commande d’analyse à l’aide de `FILTERCONTEXT` et d’une liste de colonnes spécifiée. Reportez-vous aux sections sur la [limitation des colonnes analysées](#limit-included-columns) et l’[ajout d’une condition de filtre](#filter-condition) pour plus d’informations.

L’exemple illustré ci-dessous calcule les statistiques pour le jeu de données `adc_geometric` et pour **toutes** les colonnes du jeu de données.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>La commande `COMPUTE STATISTICS` ne prend pas en charge les types de données de tableau ou de mappage. Vous pouvez définir un indicateur `skip_stats_for_complex_datatypes` pour envoyer une notification ou un message d’erreur si le cadre de données d’entrée comporte des colonnes avec des types de données de tableau et de mappage. Par défaut, l’indicateur est défini sur « true ». Pour activer les notifications ou les erreurs, utilisez la commande suivante : `SET skip_stats_for_complex_datatypes = false`.

## Créer un nom d’alias {#alias-name}

Comme les résultats des calculs peuvent être très volumineux, il n’est pas raisonnable de renvoyer les données calculées directement dans la sortie de console. Bien que les noms d’alias soient facultatifs, il est recommandé de les utiliser lors du calcul des statistiques. Indiquez un nom d’alias dans l’instruction pour référencer de manière descriptive les résultats dans vos requêtes SQL. Un `Statistics ID` peut également être généré automatiquement pour stocker les informations calculées.

L’exemple ci-dessous stocke les statistiques calculées de sortie dans le fichier `alias_name` à titre de référence ultérieure. Le nom d’alias utilisé dans la requête est disponible à titre de référence dès l’exécution de la commande `ANALYZE TABLE`.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

La sortie de l’exemple ci-dessus est `SUCCESSFULLY COMPLETED, alias_name`. La sortie de console n’affiche pas les statistiques dans la réponse à la commande de calcul de statistiques de la table d’analyse. Pour afficher les résultats détaillés, vous devez envoyer une requête SELECT au nom d’alias ou à l’identifiant de statistiques.

## Afficher la sortie des statistiques calculées {#view-output-of-computed-statistics}

Si vous n’indiquez pas de nom d’alias à l’avance, Query Service génère automatiquement un nom pour `Statistics ID` qui suit le format `<tableName_stats_{incremental_number}>`. Si un nom d’alias est fourni, il apparaît dans la colonne `Statistics ID`.

Consultez l’exemple de sortie d’une requête `COMPUTE STATISTICS` suivant :

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

Vous pouvez alors **interroger directement les statistiques calculées** en référençant l’`Statistics ID`. L’exemple d’instruction ci-dessous permet d’afficher la sortie complète lorsque vous l’utilisez avec l’`Statistics ID` ou le nom d’alias.

```sql
SELECT * FROM adc_geometric_stats_1; 
```

Le résultat des statistiques calculées peut ressembler à l’exemple ci-dessous.

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
|------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(12 rows)
```

## Afficher les métadonnées d’analyse statistique {#show-statistics}

La commande `SHOW STATISTICS` permet d’afficher les métadonnées de toutes les statistiques temporaires générées dans la session. Vous pouvez ainsi affiner la portée de votre analyse statistique.

Consultez un exemple de sortie pour `SHOW STATISTICS` ci-dessous.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
|----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Voici une description des noms des colonnes de métadonnées.

| Nom de la colonne | Description |
|---|---|
| `statsId` | Cet ID fait référence à la table temporaire des statistiques générée par la commande `COMPUTE STATISTICS`. |
| `tableName` | Table d’origine utilisée pour l’analyse. |
| `columnSet` | Liste de toutes les colonnes sélectionnées spécifiquement pour l’analyse. Une valeur vide indique que toutes les colonnes ont été analysées. Voir la section sur la [limitation des colonnes](#limit-included-columns) pour plus d’informations. |
| `filterContext` | Liste de tous les filtres appliqués à l’analyse. |
| `timestamp` | Tout filtre chronologique appliqué à votre analyse de données permettant de cibler une période spécifique. Voir la [section sur les conditions de filtre date et heure](#filter-condition) pour plus d’informations. |

Vous pouvez utiliser l’ID de statistiques ou le nom d’alias pour rechercher les statistiques calculées avec une instruction SELECT à tout moment au cours de la session actuelle. L’identifiant de statistiques et les statistiques générées ne sont valides que pour cette session particulière et ne sont pas accessibles dans différentes sessions PSQL. Les statistiques calculées ne sont actuellement pas persistantes. Consultez la section sur la façon d’[afficher la sortie de vos statistiques calculées](#view-output-of-computed-statistics) pour plus d’informations.

## Limiter les colonnes incluses {#limit-included-columns}

Pour cibler votre analyse, vous pouvez calculer des statistiques pour des colonnes de jeux de données spécifiques en les classant par nom. Utilisez la syntaxe `FOR COLUMNS (<col1>, <col2>)` pour cibler des colonnes spécifiques. L’exemple ci-dessous calcule les statistiques pour les colonnes `commerce`, `id`, et `timestamp` pour le jeu de données `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Vous pouvez calculer les statistiques pour n’importe quel niveau racine ou colonne imbriquée. L’exemple suivant illustre ces références.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Ajouter une condition de filtre date et heure {#filter-condition}

Pour cibler l’analyse de vos colonnes en fonction de la chronologie, vous pouvez ajouter une condition de filtre date et heure. Cette condition peut être utilisée pour filtrer les données historiques ou cibler votre analyse des données sur une période spécifique. La commande `FILTERCONTEXT` calcule les statistiques sur un sous-ensemble du jeu de données en fonction de la condition de filtre que vous fournissez.

Dans l’exemple ci-dessous, les statistiques sont calculées sur toutes les colonnes du jeu de données. `tableName`, où la date/heure de la colonne contient des valeurs comprises entre la plage spécifiée de `2023-04-01 00:00:00` et `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Vous pouvez combiner la limite des colonnes et le filtre pour créer des requêtes de calcul hautement spécifiques pour vos colonnes de jeux de données. Par exemple, la requête suivante calcule les statistiques sur les colonnes `commerce`, `id`, et `timestamp` pour le jeu de données `tableName`, où la colonne de date et d’heure contient des valeurs comprises entre la plage spécifiée de `2023-04-01 00:00:00` et `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous comprenez mieux comment générer des statistiques au niveau des colonnes à partir d’un jeu de données ADLS à l’aide d’une requête SQL. Il est recommandé de lire le [guide de syntaxe SQl](../sql/syntax.md) pour découvrir d’autres fonctionnalités d’Adobe Experience Platform Query Service.
