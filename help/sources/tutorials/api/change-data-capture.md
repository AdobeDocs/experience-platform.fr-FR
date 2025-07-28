---
title: Activer la capture de données de modification pour les connexions source dans l’API
description: Découvrez comment activer la capture de données de modification pour les connexions source dans l’API
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Activer la capture de données de modification pour les connexions source dans l’API

La capture de données modifiées dans les sources Adobe Experience Platform est une fonctionnalité que vous pouvez utiliser pour maintenir la synchronisation des données en temps réel entre vos systèmes source et de destination.

Actuellement, Experience Platform prend en charge la **copie incrémentielle des données**, qui garantit que les enregistrements nouvellement créés ou mis à jour dans le système source sont régulièrement copiés dans les jeux de données ingérés. Ce processus repose sur l’utilisation de la colonne **horodatage**, par exemple `LastModified` pour effectuer le suivi des modifications et capturer **uniquement les données nouvellement insérées ou mises à jour**. Cependant, cette méthode ne tient pas compte des enregistrements supprimés, ce qui peut entraîner des incohérences des données au fil du temps.

Avec la capture de données de modification, un flux donné capture et applique toutes les modifications, y compris les insertions, les mises à jour et les suppressions. De même, les jeux de données Experience Platform restent entièrement synchronisés avec le système source.

Vous pouvez utiliser la capture de données de modification pour les sources suivantes :

## [!DNL Amazon S3]

Assurez-vous que `_change_request_type` est présent dans le fichier [!DNL Amazon S3] que vous avez l’intention d’ingérer dans Experience Platform. En outre, vous devez vous assurer que les valeurs valides suivantes sont incluses dans le fichier :

* `u` : pour les insertions et les mises à jour
* `d` : pour les suppressions.

Si `_change_request_type` n’est pas présent dans votre fichier , la valeur par défaut de `u` est utilisée.

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Amazon S3] :

* [Créer une connexion  [!DNL Amazon S3]  base](../api/create/cloud-storage/s3.md).
* [Créer une connexion source pour un espace de stockage dans le cloud](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Blob]

Assurez-vous que `_change_request_type` est présent dans le fichier [!DNL Azure Blob] que vous avez l’intention d’ingérer dans Experience Platform. En outre, vous devez vous assurer que les valeurs valides suivantes sont incluses dans le fichier :

* `u` : pour les insertions et les mises à jour
* `d` : pour les suppressions.

Si `_change_request_type` n’est pas présent dans votre fichier , la valeur par défaut de `u` est utilisée.

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Azure Blob] :

* [Créer une connexion  [!DNL Azure Blob]  base](../api/create/cloud-storage/blob.md).
* [Créer une connexion source pour un espace de stockage dans le cloud](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Databricks]

Vous devez activer l’option **modifier le flux de données** dans votre table de [!DNL Azure Databricks] pour utiliser la capture de données de modification dans votre connexion source.

Utilisez les commandes suivantes pour activer explicitement l’option Modifier le flux de données dans [!DNL Azure Databricks]

**Nouveau tableau**

Pour appliquer le flux de données de modification à un nouveau tableau, vous devez définir la propriété de tableau `delta.enableChangeDataFeed` sur `TRUE` dans la commande `CREATE TABLE`.

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Table existante**

Pour appliquer le flux de données de modification à un tableau existant, vous devez définir la propriété de tableau `delta.enableChangeDataFeed` sur `TRUE` dans la commande `ALTER TABLE`.

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Toutes les nouvelles tables**

Pour appliquer le flux de données de modification à tous les nouveaux tableaux, vous devez définir vos propriétés par défaut sur `TRUE`.

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

Pour plus d’informations, consultez le guide [[!DNL Azure Databricks]  sur l’activation du flux de données de modification](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed).

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Azure Databricks] :

* [Créer une connexion  [!DNL Azure Databricks]  base](../api/create/databases/databricks.md).
* [Créer une connexion source pour une base de données](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Data Landing Zone]

Vous devez activer l’option **modifier le flux de données** dans votre table de [!DNL Data Landing Zone] pour utiliser la capture de données de modification dans votre connexion source.

Utilisez les commandes suivantes pour activer explicitement l’option Modifier le flux de données dans [!DNL Data Landing Zone].

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Data Landing Zone] :

* [Créer une connexion  [!DNL Data Landing Zone]  base](../api/create/cloud-storage/data-landing-zone.md).
* [Créer une connexion source pour un espace de stockage dans le cloud](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Google BigQuery]

Pour utiliser la capture de données de modification dans votre connexion source [!DNL Google BigQuery]. Accédez à la page [!DNL Google BigQuery] dans la console [!DNL Google Cloud] et définissez `enable_change_history` sur `TRUE`. Cette propriété active l&#39;historique des modifications de votre tableau de données.

Pour plus d’informations, consultez le guide sur les instructions de langage de définition de données dans [ [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Google BigQuery] :

* [Créer une connexion  [!DNL Google BigQuery]  base](../api/create/databases/bigquery.md).
* [Créer une connexion source pour une base de données](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Google Cloud Storage]

Assurez-vous que `_change_request_type` est présent dans le fichier [!DNL Google Cloud Storage] que vous avez l’intention d’ingérer dans Experience Platform. En outre, vous devez vous assurer que les valeurs valides suivantes sont incluses dans le fichier :

* `u` : pour les insertions et les mises à jour
* `d` : pour les suppressions.

Si `_change_request_type` n’est pas présent dans votre fichier , la valeur par défaut de `u` est utilisée.

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Google Cloud Storage] :

* [Créer une connexion  [!DNL Google Cloud Storage]  base](../api/create/cloud-storage/google.md).
* [Créer une connexion source pour un espace de stockage dans le cloud](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL SFTP]

Assurez-vous que `_change_request_type` est présent dans le fichier [!DNL SFTP] que vous avez l’intention d’ingérer dans Experience Platform. En outre, vous devez vous assurer que les valeurs valides suivantes sont incluses dans le fichier :

* `u` : pour les insertions et les mises à jour
* `d` : pour les suppressions.

Si `_change_request_type` n’est pas présent dans votre fichier , la valeur par défaut de `u` est utilisée.

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL SFTP] :

* [Créer une connexion  [!DNL SFTP]  base](../api/create/cloud-storage/sftp.md).
* [Créer une connexion source pour un espace de stockage dans le cloud](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL Snowflake]

Vous devez activer le **suivi des modifications** dans vos tables [!DNL Snowflake] pour utiliser la capture de données de modification dans vos connexions source.

Dans [!DNL Snowflake], activez le suivi des modifications à l’aide de l’`ALTER TABLE` et définissez `CHANGE_TRACKING` sur `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Pour plus d’informations, consultez le guide [[!DNL Snowflake]  sur l’utilisation de la clause de modification ](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Snowflake] :

* [Créer une connexion  [!DNL Snowflake]  base](../api/create/databases/snowflake.md).
* [Créer une connexion source pour une base de données](../api/collect/database-nosql.md#create-a-source-connection).

