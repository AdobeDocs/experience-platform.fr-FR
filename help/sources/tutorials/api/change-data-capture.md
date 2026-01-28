---
title: Activer la capture de données de modification pour les connexions source dans l’API
description: Découvrez comment activer la capture de données de modification pour les connexions source dans l’API
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: bd28d5be932823b8bf9c98280f97694ff221d76d
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---

# Activer la capture de données de modification pour les connexions source dans l’API

>[!AVAILABILITY]
>
>Vous pouvez désormais utiliser la capture de données de modification pour les sources [!DNL Amazon S3] et [!DNL Data Landing Zone] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS) en étant connecté à un centre de données VA6. Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Utilisez la capture de données de modification dans les sources Adobe Experience Platform pour que vos systèmes source et de destination restent synchronisés en temps quasi réel.

Experience Platform prend actuellement en charge la **copie incrémentielle de données**, qui transfère régulièrement les enregistrements nouvellement créés ou mis à jour du système source vers les jeux de données ingérés. Cette méthode repose sur une **colonne d’horodatage** pour suivre les modifications, mais elle ne détecte pas les suppressions, ce qui peut entraîner des incohérences des données au fil du temps.

En revanche, la capture de données de modification capture et applique les insertions, les mises à jour et les suppressions en temps quasi réel. Ce suivi complet des modifications garantit que les jeux de données restent entièrement alignés sur le système source et fournit un historique complet des modifications, au-delà de ce que la copie incrémentielle prend en charge. Toutefois, les opérations de suppression nécessitent une attention particulière, car elles affectent toutes les applications utilisant les jeux de données cibles.

La capture de données modifiées dans Experience Platform nécessite **[Data Mirror](../../../xdm/data-mirror/overview.md)** avec des [schémas relationnels](../../../xdm/schema/relational.md). Vous pouvez fournir des données de modification à Data Mirror de deux manières :

* **[Suivi manuel des modifications](#file-based-sources)** : incluez une colonne `_change_request_type` dans votre jeu de données pour les sources qui ne génèrent pas d’enregistrements de capture de données de modification de manière native
* **[Exportations natives de capture de données de modification](#database-sources)** : utilisez les enregistrements de capture de données de modification exportés directement depuis votre système source

Les deux approches nécessitent Data Mirror avec des schémas relationnels pour préserver les relations et appliquer l’unicité.

## Data Mirror avec schémas relationnels

>[!AVAILABILITY]
>
>Les schémas Data Mirror et relationnels sont disponibles pour les détenteurs de licence Adobe Journey Optimizer **Campagnes orchestrées**. Ils sont également disponibles en tant que **version limitée** pour les utilisateurs de Customer Journey Analytics, selon votre licence et l’activation des fonctionnalités. Contactez votre représentant Adobe pour obtenir l’accès.

>[!NOTE]
>
>**Utilisateurs des campagnes orchestrées** : utilisez les fonctionnalités Data Mirror décrites dans ce document pour travailler avec les données client qui conservent l’intégrité du référentiel. Même si votre source n’utilise pas la mise en forme de capture de données de modification, Data Mirror prend en charge des fonctionnalités relationnelles telles que l’application des clés primaires, les upserts au niveau des enregistrements et les relations de schéma. Ces fonctionnalités assurent une modélisation des données cohérente et fiable sur les jeux de données connectés.

Data Mirror utilise des schémas relationnels pour étendre la capture de données de modification et activer des fonctionnalités avancées de synchronisation de base de données. Pour obtenir un aperçu de Data Mirror, consultez [Présentation de Data Mirror](../../../xdm/data-mirror/overview.md).

Les schémas relationnels étendent Experience Platform pour appliquer l’unicité des clés primaires, suivre les modifications au niveau des lignes et définir des relations au niveau du schéma. Avec la capture de données de modification, ils appliquent les insertions, les mises à jour et les suppressions directement dans le lac de données, réduisant ainsi le besoin d&#39;extraire, de transformer, de charger (ETL) ou de réconciliation manuelle.

Consultez [ Présentation des schémas relationnels ](../../../xdm/schema/relational.md) pour plus d’informations.

### Schéma relationnel requis pour la capture de données de modification

Avant d’utiliser un schéma relationnel avec capture de données de modification, configurez les identifiants suivants :

* Identifier de manière unique chaque enregistrement avec une clé primaire.
* Appliquez les mises à jour en séquence à l’aide d’un identifiant de version.
* Pour les schémas de série temporelle, ajoutez un identifiant d’horodatage.

### Gestion des colonnes de contrôle {#control-column-handling}

Utilisez la colonne `_change_request_type` pour spécifier le mode de traitement de chaque ligne :

* `u` — upsert (par défaut si la colonne est absente)
* `d` — supprimer

Cette colonne est évaluée uniquement lors de l’ingestion et n’est ni stockée ni mappée à des champs XDM.

### Workflow {#workflow}

Pour activer la capture de données de modification avec un schéma relationnel :

1. Créez un schéma relationnel.
2. Ajoutez les descripteurs requis :
   * [descripteur de clé de Principal](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [Descripteur de version](../../../xdm/api/descriptors.md#version-descriptor)
   * [Descripteur d’horodatage](../../../xdm/api/descriptors.md#timestamp-descriptor) (série temporelle uniquement)
3. Créez un jeu de données à partir du schéma et activez la capture de données de modification.
4. Pour l’ingestion basée sur des fichiers uniquement : ajoutez la colonne `_change_request_type` à vos fichiers sources si vous devez spécifier explicitement les opérations de suppression. Les configurations d’exportation CDC le gèrent automatiquement pour les sources de base de données.
5. Terminez la configuration de la connexion source pour activer l’ingestion.

>[!NOTE]
>
>La colonne `_change_request_type` n’est nécessaire que pour les sources basées sur des fichiers (Amazon S3, Azure Blob, Google Cloud Storage, SFTP) lorsque vous souhaitez contrôler explicitement le comportement de changement au niveau des lignes. Pour les sources de base de données disposant de fonctionnalités CDC natives, les opérations de modification sont gérées automatiquement via les configurations d’exportation CDC. L’ingestion basée sur des fichiers suppose des opérations d’upsert par défaut. Il vous suffit d’ajouter cette colonne si vous souhaitez spécifier des opérations de suppression dans vos chargements de fichiers.

>[!IMPORTANT]
>
>**La planification de la suppression des données est requise**. Toutes les applications qui utilisent des schémas relationnels doivent comprendre les implications de suppression avant d&#39;implémenter la capture de données de modification. Planifiez la manière dont les suppressions affecteront les jeux de données associés, les exigences de conformité et les processus en aval. Voir [considérations relatives à l’hygiène des données](../../../hygiene/ui/record-delete.md#relational-record-delete) pour obtenir des conseils.

## Fournir des données de modification pour les sources basées sur des fichiers {#file-based-sources}

>[!IMPORTANT]
>
>La capture de données de modification basée sur des fichiers nécessite Data Mirror avec des schémas relationnels. Avant de suivre les étapes de formatage des fichiers ci-dessous, assurez-vous d’avoir terminé le workflow de configuration de [Data Mirror](#workflow) décrit précédemment dans ce document. Les étapes ci-dessous décrivent comment formater vos fichiers de données afin d’inclure les informations de suivi des modifications qui seront traitées par Data Mirror.

Pour les sources basées sur des fichiers ([!DNL Amazon S3], [!DNL Azure Blob], [!DNL Google Cloud Storage] et [!DNL SFTP]), incluez une colonne `_change_request_type` dans vos fichiers.

Utilisez les valeurs `_change_request_type` définies dans la section [Gestion des colonnes de contrôle](#control-column-handling) ci-dessus.

>[!IMPORTANT]
>
>Pour les **sources basées sur des fichiers uniquement**, certaines applications peuvent nécessiter une colonne `_change_request_type` avec `u` (upsert) ou `d` (delete) pour valider les fonctionnalités de suivi des modifications. Par exemple, la fonction Adobe Journey Optimizer **Campagnes orchestrées** nécessite cette colonne pour activer le bouton « Campagne orchestrée » et autoriser la sélection du jeu de données pour le ciblage. Les exigences de validation spécifiques à l’application peuvent varier.

Suivez les étapes spécifiques à la source ci-dessous.

### Sources d’espace de stockage {#cloud-storage-sources}

Activez la capture de données de modification pour les sources d’espace de stockage en procédant comme suit :

1. Créez une connexion de base pour votre source :

   | Source | Guide de connexion de base |
   |---|---|
   | [!DNL Amazon S3] | [Créer une connexion  [!DNL Amazon S3]  base](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [Créer une connexion  [!DNL Azure Blob]  base](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [Créer une connexion  [!DNL Google Cloud Storage]  base](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [Créer une connexion  [!DNL SFTP]  base](../api/create/cloud-storage/sftp.md) |

2. [Créer une connexion source pour un espace de stockage dans le cloud](../api/collect/cloud-storage.md#create-a-source-connection).

Toutes les sources d’espace de stockage utilisent le même format de colonne `_change_request_type` décrit dans la section [Sources basées sur des fichiers](#file-based-sources) ci-dessus.

## Sources de base de données {#database-sources}

### [!DNL Azure Databricks]

Pour utiliser la capture de données de modification avec [!DNL Azure Databricks], vous devez à la fois activer **modifier le flux de données** dans vos tables source et configurer Data Mirror avec des schémas relationnels dans Experience Platform.

Utilisez les commandes suivantes pour activer la modification du flux de données sur vos tableaux :

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

### [!DNL Data Landing Zone]

Pour utiliser la capture de données de modification avec [!DNL Data Landing Zone], vous devez à la fois activer **modifier le flux de données** dans vos tables source et configurer Data Mirror avec des schémas relationnels dans Experience Platform.

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Data Landing Zone] :

* [Créer une connexion  [!DNL Data Landing Zone]  base](../api/create/cloud-storage/data-landing-zone.md).
* [Créer une connexion source pour un espace de stockage dans le cloud](../api/collect/cloud-storage.md#create-a-source-connection).

### [!DNL Google BigQuery]

Pour utiliser la capture de données de modification avec [!DNL Google BigQuery], vous devez activer l’historique des modifications dans vos tables source et configurer Data Mirror avec des schémas relationnels dans Experience Platform.

Pour activer l’historique des modifications dans votre connexion source [!DNL Google BigQuery], accédez à la page [!DNL Google BigQuery] dans la console [!DNL Google Cloud] et définissez `enable_change_history` sur `TRUE`. Cette propriété active l&#39;historique des modifications de votre tableau de données.

Pour plus d’informations, consultez le guide sur les instructions de langage de définition de données dans [ [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Google BigQuery] :

* [Créer une connexion  [!DNL Google BigQuery]  base](../api/create/databases/bigquery.md).
* [Créer une connexion source pour une base de données](../api/collect/database-nosql.md#create-a-source-connection).

### [!DNL Snowflake]

Pour utiliser la capture de données de modification avec [!DNL Snowflake], vous devez activer le **suivi des modifications** dans vos tables source et configurer Data Mirror avec des schémas relationnels dans Experience Platform.

Dans [!DNL Snowflake], activez le suivi des modifications à l’aide de l’`ALTER TABLE` et définissez `CHANGE_TRACKING` sur `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Pour plus d’informations, consultez le guide [[!DNL Snowflake]  sur l’utilisation de la clause de modification ](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Lisez la documentation suivante pour savoir comment activer la capture de données de modification pour votre connexion source [!DNL Snowflake] :

* [Créer une connexion  [!DNL Snowflake]  base](../api/create/databases/snowflake.md).
* [Créer une connexion source pour une base de données](../api/collect/database-nosql.md#create-a-source-connection).
