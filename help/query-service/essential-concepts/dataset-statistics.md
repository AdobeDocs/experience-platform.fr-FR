---
title: Calcul des statistiques des jeux de données
description: Ce document décrit comment calculer les statistiques au niveau des colonnes sur les jeux de données Azure Data Lake Storage (ADLS) avec des commandes SQL.
source-git-commit: c7bc395038906e27449c82c518bd33ede05c5691
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 90%

---

# Calcul des statistiques des jeux de données

Vous pouvez désormais calculer les statistiques au niveau des colonnes sur les jeux de données [!DNL Azure Data Lake Storage] (ADLS) avec les commandes SQL `COMPUTE STATISTICS` et `SHOW STATISTICS`. Les commandes SQL qui calculent les statistiques des jeux de données sont une extension de la commande `ANALYZE TABLE`. Vous trouverez des détails complets sur la commande `ANALYZE TABLE` dans la [documentation de référence SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Actuellement, les statistiques générées ne sont valides que pour cette session et ne sont pas persistantes entre chaque session. Elles ne sont pas accessibles dans différentes sessions PSQL.

Avec la commande `SHOW STATISTICS FOR <alias_name>`, vous pouvez voir les statistiques qui ont été calculées avec la commande `ANALYZE TABLE COMPUTE STATISTICS`. Grâce à la combinaison de ces commandes, vous pouvez désormais calculer les statistiques des colonnes sur l’ensemble du jeu de données, un sous-ensemble d’un jeu de données, toutes les colonnes ou un sous-ensemble de colonnes.

>[!IMPORTANT]
>
>Les commandes `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, et `SHOW STATISTICS` ne sont pas prises en charge sur les tables de l’entrepôt de données. Ces extensions pour la commande `ANALYZE TABLE` ne sont actuellement prises en charge que pour les tables ADLS. Pour plus d’informations, voir la [section TABLE D’ANALYSE](../sql/syntax.md#analyze-table) du guide de syntaxe SQL.

Ce guide vous aide à structurer vos requêtes afin que vous puissiez calculer les statistiques de colonnes d’un jeu de données ADLS. À l’aide de ces commandes, vous pouvez afficher les statistiques générées dans votre session via un client PSQL à l’aide d’une requête SQL.

## Calcul des statistiques {#compute-statistics}

D’autres éléments ont été ajoutés à la commande `ANALYZE TABLE` qui vous permettent de **calculer les statistiques pour un sous-ensemble d’un jeu de données et pour certaines colonnes**. Pour ce faire, vous devez utiliser le format `ANALYZE TABLE <tableName> COMPUTE STATISTICS`.

>[!IMPORTANT]
>
>Le comportement par défaut calcule les statistiques pour le **jeu de données complet** et pour **toutes les colonnes**. Pour calculer les statistiques sur toutes les colonnes, vous devez utiliser le format de requête `ANALYZE TABLE COMPUTE STATISTICS`. Nous vous recommandons de ne **pas** l’utiliser sur un jeu de données ADLS, car la taille du jeu de données peut être très importante (potentiellement des pétaoctets de données). Vous devez toujours envisager d’exécuter la commande d’analyse à l’aide de `FILTERCONTEXT` et d’une liste de colonnes spécifiée. Reportez-vous aux sections sur la [limitation des colonnes analysées](#limit-included-columns) et l’[ajout d’une condition de filtre](#filter-condition) pour plus d’informations.

L’exemple illustré ci-dessous calcule les statistiques pour le jeu de données `adc_geometric` et pour **toutes** les colonnes du jeu de données.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` ne prend pas en charge les types de données de tableau ou de mappage. Vous pouvez définir un indicateur `skip_stats_for_complex_datatypes` pour envoyer une notification ou un message d’erreur si le cadre de données d’entrée comporte des colonnes avec des types de données de tableau et de mappage. Par défaut, l’indicateur est défini sur « true ». Pour activer les notifications ou les erreurs, utilisez la commande suivante : `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

La sortie console n’affiche pas les statistiques en réponse à la commande de calcul de statistiques de la table d’analyse. À la place, la console affiche une colonne à une seule ligne de `Statistics ID` avec un identifiant universel unique pour référencer les résultats. Vous pouvez également choisir **directement sur la`Statistics ID`**. Une fois la requête `COMPUTE STATISTICS` terminée, les résultats sont affichés comme suit :

```console
| Statistics ID    | 
| ---------------- |
| adc_geometric_stats_1 |
(1 row)
```

Vous pouvez interroger directement la sortie des statistiques en référençant la variable `Statistics ID` comme illustré ci-dessous :

```sql
SELECT * FROM adc_geometric_stats_1; 
```

Cette instruction vous permet d’afficher la sortie de la même manière que la commande AFFICHER les STATISTIQUES lors de l’utilisation de avec la fonction `Statistics ID`.

Vous pouvez afficher une liste de toutes les statistiques calculées de la session en exécutant la commande AFFICHER LES STATISTIQUES . Vous trouverez ci-dessous un exemple de sortie de la commande AFFICHER LES STATISTIQUES .

```console
statsId | tableName | columnSet | filterContext | timestamp
-----------+---------------+-----------+---------------------------------------+---------------
adc_geometric_stats_1 |adc_geometric | (age) | | 25/06/2023 09:22:26
demo_table_stats_1 | demo_table | (*) | ((age > 25)) | 25/06/2023 12:50:26
```

<!-- Commented out until the <alias_name> feature is released.

To see the output, you must use the `SHOW STATISTICS` command. Instructions on [how to show the statistics](#show-statistics) are provided later in the document. 

-->

## Limiter les colonnes incluses {#limit-included-columns}

Vous pouvez calculer des statistiques pour des colonnes de jeux de données spécifiques en les classant par nom. Utilisez la syntaxe `FOR COLUMNS (<col1>, <col2>)` pour cibler des colonnes spécifiques. L’exemple ci-dessous calcule les statistiques pour les colonnes  `commerce`, `id`, et `timestamp` pour le jeu de données `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Vous pouvez calculer les statistiques pour n’importe quel niveau racine ou colonne imbriquée. L’exemple suivant illustre ces références.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Ajouter une condition de filtre date et heure {#filter-condition}

Vous pouvez ajouter une condition de filtre date et heure pour cibler l’analyse de vos colonnes. Vous pouvez l’utiliser pour filtrer les données historiques ou concentrer votre analyse des données sur une période spécifique. La commande `FILTERCONTEXT` calcule les statistiques sur un sous-ensemble du jeu de données en fonction de la condition de filtre que vous fournissez.

Dans l’exemple ci-dessous, les statistiques sont calculées sur toutes les colonnes du jeu de données. `tableName`, où la date/heure de la colonne contient des valeurs comprises entre la plage spécifiée de `2023-04-01 00:00:00` et `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Vous pouvez combiner la limite des colonnes et le filtre pour créer des requêtes de calcul hautement spécifiques pour vos colonnes de jeux de données. Par exemple, la requête suivante calcule les statistiques sur les colonnes `commerce`, `id`, et `timestamp` pour le jeu de données `tableName`, où la date/heure de la colonne contient des valeurs comprises entre la plage spécifiée de `2023-04-01 00:00:00` et `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

<!-- Commented out until the <alias_name> feature is released.
## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. 
-->

<!-- Commented out until the <alias_name> feature is released.

## Show the statistics {#show-statistics}

The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  

Even with a filter condition and a column list, the computation can target a large amount of data. Query Service generates a universally unique identifier for the statistics ID to store this calculated information. You can then use this statistics ID to look up the computed statistics with the `SHOW STATISTICS` command at any time within that session. 

The statistics ID and the statistics generated are only valid for this particular session and cannot be accessed across different PSQL sessions. The computed statistics are not currently persistent. To display the statistics, use the command seen below.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

An output might look similar to the example below. 

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
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

-->

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous comprenez mieux comment générer des statistiques au niveau des colonnes à partir d’un jeu de données ADLS à l’aide d’une requête SQL. Il est recommandé de lire le [guide de syntaxe SQl](../sql/syntax.md) pour découvrir d’autres fonctionnalités d’Adobe Experience Platform Query Service.
