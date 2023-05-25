---
title: Calcul des statistiques sur les jeux de données
description: Ce document décrit comment calculer les statistiques au niveau des colonnes sur les jeux de données Azure Data Lake Storage (ADLS) avec des commandes SQL.
source-git-commit: c42a7cd46f79bb144176450eafb00c2f81409380
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Calcul des statistiques des jeux de données

Vous pouvez désormais calculer les statistiques au niveau des colonnes sur [!DNL Azure Data Lake Storage] (ADLS) des jeux de données avec la variable `COMPUTE STATISTICS` et `SHOW STATISTICS` Commandes SQL. Les commandes SQL qui calculent les statistiques des jeux de données sont une extension de la fonction `ANALYZE TABLE` . Détails complets sur la variable `ANALYZE TABLE` se trouve dans la fonction [Documentation de référence SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Actuellement, les statistiques générées ne sont valides que pour cette session et ne sont pas persistantes entre les sessions. Elles ne sont pas accessibles dans différentes sessions PSQL.

Avec le `SHOW STATISTICS FOR <alias_name>` , vous pouvez voir les statistiques qui ont été calculées avec la variable `ANALYZE TABLE COMPUTE STATISTICS` . Grâce à la combinaison de ces commandes, vous pouvez désormais calculer les statistiques des colonnes sur l’ensemble du jeu de données, un sous-ensemble d’un jeu de données, toutes les colonnes ou un sous-ensemble de colonnes.

>[!IMPORTANT]
>
>Le `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, et `SHOW STATISTICS` Les commandes ne sont pas prises en charge sur les tables de l’entrepôt de données. Ces extensions pour la variable `ANALYZE TABLE` ne sont actuellement prises en charge que pour les tables ADLS. Pour plus d’informations, voir [Section ANALYZE TABLE](../sql/syntax.md#analyze-table) du guide de syntaxe SQL.

Ce guide vous aide à structurer vos requêtes afin que vous puissiez calculer les statistiques de colonnes d’un jeu de données ADLS. À l’aide de ces commandes, vous pouvez afficher les statistiques générées dans votre session via un client PSQL à l’aide d’une requête SQL.

## Calcul des statistiques {#compute-statistics}

D’autres éléments ont été ajoutés au `ANALYZE TABLE` qui vous permettent de **calculer les statistiques pour un sous-ensemble d’un jeu de données et pour certaines colonnes ;**. Pour ce faire, vous devez utiliser la variable `ANALYZE TABLE <tableName> COMPUTE STATISTICS` format.

>[!IMPORTANT]
>
>Le comportement par défaut calcule les statistiques pour la variable **jeu de données complet** et **toutes les colonnes**. Pour calculer les statistiques sur toutes les colonnes, vous utiliseriez le format de requête `ANALYZE TABLE COMPUTE STATISTICS`. Vous êtes **not** recommandé de l’utiliser sur un jeu de données ADLS, car la taille du jeu de données peut être très importante (potentiellement pétaoctets de données). Vous devez toujours envisager d’exécuter la commande d’analyse à l’aide de la commande `FILTERCONTEXT` et une liste de colonnes spécifiée. Reportez-vous aux sections de la section [limitation des colonnes analysées](#limit-included-columns) et [ajout d’une condition de filtre](#filter-condition) pour plus d’informations.

L’exemple illustré ci-dessous calcule les statistiques pour la variable `adc_geometric` jeu de données et pour **all** colonnes du jeu de données.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` ne prend pas en charge les types de données de tableau ou de mappage. Vous pouvez définir une `skip_stats_for_complex_datatypes` Indicateur à avertir ou à exclure si le cadre de données d’entrée comporte des colonnes avec des tableaux et des types de données de mappage. Par défaut, l’indicateur est défini sur true. Pour activer les notifications ou les erreurs, utilisez la commande suivante : `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

La sortie console n&#39;affiche pas les statistiques en réponse à la commande d&#39;analyse des statistiques de calcul du tableau. À la place, la console affiche une seule colonne de ligne de `Statistics ID` avec un identifiant unique universel pour référencer les résultats. Une fois l’opération terminée, `COMPUTE STATISTICS` , les résultats sont affichés comme suit :

```console
| Statistics ID    | 
| ---------------- |
| QqMtDfHQOdYJpZlb |
(1 row)
```

Pour afficher la sortie, vous devez utiliser la variable `SHOW STATISTICS` . Instructions sur [affichage des statistiques](#show-statistics) sont fournies ultérieurement dans le document.

## Limiter les colonnes incluses {#limit-included-columns}

Vous pouvez calculer des statistiques pour des colonnes de jeux de données spécifiques en les référençant par nom. Utilisez la variable `FOR COLUMNS (<col1>, <col2>)` pour cibler des colonnes spécifiques. L’exemple ci-dessous calcule les statistiques pour les colonnes  `commerce`, `id`, et `timestamp` pour le jeu de données `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Vous pouvez calculer les statistiques pour n’importe quel niveau racine ou colonne imbriquée. L’exemple suivant illustre ces références.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Ajout d’une condition de filtre d’horodatage {#filter-condition}

Vous pouvez ajouter une condition de filtre d’horodatage pour cibler l’analyse de vos colonnes. Vous pouvez l’utiliser pour filtrer les données historiques ou concentrer votre analyse des données sur une période spécifique. Le `FILTERCONTEXT` calcule les statistiques sur un sous-ensemble du jeu de données en fonction de la condition de filtre que vous fournissez.

Dans l’exemple ci-dessous, les statistiques sont calculées sur toutes les colonnes du jeu de données. `tableName`, où l’horodatage de la colonne contient des valeurs comprises entre la plage spécifiée de `2023-04-01 00:00:00` et `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Vous pouvez combiner la limite des colonnes et le filtre pour créer des requêtes de calcul hautement spécifiques pour vos colonnes de jeux de données. Par exemple, la requête suivante calcule les statistiques sur les colonnes `commerce`, `id`, et `timestamp` pour le jeu de données `tableName`, où l’horodatage de la colonne contient des valeurs comprises entre la plage spécifiée de `2023-04-01 00:00:00` et `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

<!-- ## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. -->

## Afficher les statistiques {#show-statistics}

<!-- Commented out until the <alias_name> feature is released.
The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  -->

Même avec une condition de filtrage et une liste de colonnes, le calcul peut cibler une grande quantité de données. Query Service génère un identifiant unique universel pour l’ID de statistiques afin de stocker ces informations calculées. Vous pouvez ensuite utiliser cet identifiant de statistique pour rechercher les statistiques calculées avec la variable `SHOW STATISTICS` à tout moment au cours de cette session.

L’identifiant de statistique et les statistiques générées ne sont valides que pour cette session particulière et ne sont pas accessibles dans différentes sessions PSQL. Les statistiques calculées ne sont actuellement pas persistantes. Pour afficher les statistiques, utilisez la commande ci-dessous.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

Une sortie peut ressembler à l’exemple ci-dessous.

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

## Étapes suivantes {#next-steps}

En lisant ce document, vous comprenez mieux comment générer des statistiques au niveau des colonnes à partir d’un jeu de données ADLS à l’aide d’une requête SQL. Il est recommandé de lire le [Guide de syntaxe SQl](../sql/syntax.md) pour découvrir d’autres fonctionnalités de Adobe Experience Platform Query Service.
