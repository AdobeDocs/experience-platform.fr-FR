---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des connecteurs de source d'Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: a9ce046d6ee8622e23f31edbbf777b045109c13b
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 1%

---


# Présentation des connecteurs source

L’Adobe Experience Platform permet l’assimilation de données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform. Vous pouvez ingérer des données à partir de diverses sources, telles que des applications Adobe, des enregistrements basés sur le cloud, des bases de données, etc.

L’Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à divers fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir les heures d’exécution pour l’assimilation et de gérer le débit d’assimilation des données.

Avec Experience Platform, vous pouvez centraliser les données que vous collectez à partir de sources disparates et utiliser les connaissances que vous en tirez pour en faire plus.

## Types de sources

Les sources dans l’Experience Platform sont regroupées dans les catégories suivantes :

### Applications Adobe

L’Experience Platform permet l’assimilation de données à partir d’autres applications Adobe, notamment Adobe Analytics, Adobe Audience Manager et Experience Platform Launch. Pour plus d’informations, consultez les documents connexes suivants :

- [Présentation du connecteur d&#39;Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Création d’un connecteur de source d’Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation du connecteur de données Adobe](connectors/adobe-applications/analytics.md)
- [Création d’un connecteur source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Création d’un connecteur source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicité

L’Experience Platform prend en charge l’importation de données à partir d’un système de publicité tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur Google AdWords](connectors/advertising/ads.md)

### Stockage dans le cloud

Les sources d’enregistrement Cloud peuvent importer vos propres données dans Platform sans avoir à télécharger, mettre en forme ou télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources à l’aide de l’interface utilisateur. Pour plus d’informations, consultez les documents connexes suivants :

- [Connecteur Azure Data Lake Enregistrement Gen2](connectors/cloud-storage/adls-gen2.md)
- [Connecteur Azure Blob et Amazon S3](connectors/cloud-storage/blob-s3.md)
- [Connecteur Amazon Kinesis](connectors/cloud-storage/kinesis.md)
- [Connecteur Apache HDFS](connectors/cloud-storage/hdfs.md)
- [Connecteur de concentrateurs de Événement Azure](connectors/cloud-storage/eventhub.md)
- [Connecteur d&#39;Enregistrement de fichiers Azure](connectors/cloud-storage/azure-file-storage.md)
- [Connecteur FTP et SFTP](connectors/cloud-storage/ftp-sftp.md)
- [Connecteur d’Enregistrement Google Cloud](connectors/cloud-storage/google-cloud-storage.md)

### Gestion de la relation client

Les systèmes de gestion de la relation client fournissent des données qui peuvent aider à établir des relations client, ce qui à son tour favorise la fidélité et favorise la rétention des clients. Experience Platform fournit une prise en charge pour l&#39;assimilation de données CRM à partir de Microsoft Dynamics 365 et de Salesforce. Pour plus d’informations, consultez les documents connexes suivants :

- [Connecteur Microsoft Dynamics ](connectors/crm/ms-dynamics.md)
- [Connecteur Salesforce](connectors/crm/salesforce.md)

### Réussite des clients

L’Experience Platform prend en charge l’assimilation de données à partir d’une application de succès client tierce. Pour plus d’informations, consultez les documents connexes suivants :

- [Connecteur Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md)
- [Connecteur ServiceNow](connectors/customer-success/servicenow.md)

### Base de données

L’Experience Platform prend en charge l’assimilation de données à partir d’une base de données tierce. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur Amazon Redshift](connectors/databases/redshift.md)
- [Apache Hive sur le connecteur Azure HDInsights](connectors/databases/hive.md)
- [Apache Spark sur Azure HDInsights connector](connectors/databases/spark.md)
- [Connecteur Azure Data Explorer](connectors/databases/data-explorer.md)
- [Connecteur Analytics Azure Synapse](connectors/databases/synapse-analytics.md)
- [Connecteur d&#39;Enregistrement de table Azure](connectors/databases/ats.md)
- [Connecteur Couchbase](connectors/databases/couchbase.md)
- [Connecteur Google BigQuery](connectors/databases/bigquery.md)
- [Connecteur GreenPlum](connectors/databases/greenplum.md)
- [Connecteur HP Vertica](connectors/databases/hp-vertica.md)
- [Connecteur IBM DB2](connectors/databases/ibm-db2.md)
- [Connecteur MariaDB](connectors/databases/mariadb.md)
- [Connecteur Microsoft SQL Server](connectors/databases/sql-server.md)
- [Connecteur MySQL](connectors/databases/mysql.md)
- [Connecteur Oracle](connectors/databases/oracle.md)
- [Connecteur Phoenix](connectors/databases/phoenix.md)
- [Connecteur PostgreSQL](connectors/databases/postgres.md)

### Automatisation du marketing

L’Experience Platform prend en charge l’importation de données à partir d’un système tiers d’automatisation du marketing. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur HubSpot](connectors/marketing-automation/hubspot.md)

### Paiements

L’Experience Platform prend en charge l’assimilation de données à partir d’un système de paiement tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur PayPal](connectors/payments/paypal.md)

### Protocoles

Experience Platform fournit la prise en charge de l’assimilation de données à partir d’un système de protocoles tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur OData générique](connectors/protocols/odata.md)

## Contrôle d&#39;accès des sources dans l&#39;assimilation des données

Les autorisations pour les sources dans l’assimilation de données peuvent être gérées dans l’Adobe Admin Console. Vous pouvez accéder aux autorisations par le biais de l’onglet *Autorisations* dans un profil de produits particulier. Dans le panneau **Modifier les autorisations** , vous pouvez accéder aux autorisations relatives aux sources par le biais de l’entrée de menu d’assimilation *des* données. L’autorisation Sources **de** Vue accorde un accès en lecture seule aux sources disponibles dans l’onglet *Catalogue* et aux sources authentifiées dans l’onglet *Parcourir* , tandis que l’autorisation **Gérer les sources accorde un accès complet à la lecture, à la création, à la modification et à la désactivation des sources.**

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction de différentes combinaisons de ces autorisations :

| Niveau d&#39;autorisation | Description |
| ---- | ----|
| **Sources** de Vue activées | Accordez un accès en lecture seule aux sources de chaque type de source dans l’onglet *Catalogue* , ainsi qu’aux onglets *Parcourir*, *Comptes* et *Flux de données.* |
| **Gérer les sources** sur | Outre les fonctions incluses dans les sources **de** Vue, accorde l&#39;accès à l&#39;option *Connect Source* dans le *catalogue* et à l&#39;option *Sélectionner les données dans Parcourir.*** **Gérer les sources** vous permet également d’activer ou de désactiver *DataFlows* et de modifier leurs planifications. |
| **Sources** de Vue désactivées et **gestion des sources** désactivées | Révoquer tous les accès aux sources. |

Pour plus d’informations sur les autorisations disponibles accordées par l’intermédiaire de l’Admin Console, y compris ces quatre sources, voir l’aperçu [du](../access-control/home.md)contrôle d&#39;accès.

## Termes et conditions {#terms-and-conditions}

En utilisant l&#39;une des sources étiquetées bêta (&quot;bêta&quot;), Vous reconnaissez que la version bêta est fournie ***&quot;telle quelle&quot; sans aucune garantie***.

Adobe n&#39;a aucune obligation de maintenir, corriger, mettre à jour, modifier, modifier ou prendre en charge la version bêta. Nous vous conseillons de faire preuve de prudence et de ne pas vous fier de quelque façon que ce soit au bon fonctionnement ou au bon fonctionnement de cette version bêta et/ou du matériel qui l&#39;accompagne. La version bêta est considérée comme une information confidentielle d’Adobe.

Toute &quot;évaluation&quot; (information concernant la version bêta, y compris mais sans s&#39;y limiter, les problèmes ou les défauts que vous rencontrez lors de l&#39;utilisation de la version bêta, suggestions, améliorations et recommandations) fournie par Vous à Adobe est par la présente attribuée à Adobe, y compris tous les droits, titres et intérêts liés à ces commentaires.

Envoyez des commentaires en cours ou créez un ticket d&#39;assistance pour partager vos suggestions ou signaler un bogue. Recherchez une amélioration de fonctionnalité.
