---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des connecteurs de source Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 8ee88b27c79610827ff2627999e303b5fc43e1c6

---


# Présentation des connecteurs source

Adobe Experience Platform permet l’assimilation de données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme. Vous pouvez ingérer des données à partir de diverses sources, telles que des applications Adobe, des enregistrements basés sur le cloud, des bases de données, etc.

La plate-forme d’expérience fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à divers fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir les heures d’exécution pour l’assimilation et de gérer le débit d’assimilation des données.

Avec la plateforme d’expérience, vous pouvez centraliser les données que vous collectez à partir de sources disparates et utiliser les connaissances acquises pour en faire plus.

## Types de sources

Les sources de la plate-forme d’expérience sont regroupées dans les catégories suivantes :

### Applications Adobe

Experience Platform permet d’importer des données d’autres applications Adobe, notamment Adobe Analytics, Adobe Audience Manager et Experience Platform Launch. Pour plus d’informations, consultez les documents connexes suivants :

- [Présentation du connecteur Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Création d’un connecteur source Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation du connecteur de données Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Création d’un connecteur source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Création d’un connecteur source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicité

Experience Platform prend en charge l’importation de données à partir d’un système de publicité tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur Publicités Google](connectors/advertising/ads.md)

### Stockage dans le cloud

Les sources d’enregistrement Cloud peuvent importer vos propres données dans Platform sans avoir à télécharger, mettre en forme ou télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources à l’aide de l’interface utilisateur. Pour plus d’informations, consultez les documents connexes suivants :

- [Connecteur Azure Data Lake Enregistrement Gen2](connectors/cloud-storage/adls-gen2.md)
- [Connecteur Azure Blob et Amazon S3](connectors/cloud-storage/blob-s3.md)
- [Connecteur FTP et SFTP](connectors/cloud-storage/ftp-sftp.md)
- [Connecteur d’Enregistrement Google Cloud](connectors/cloud-storage/google-cloud-storage.md)

### Gestion de la relation client

Les systèmes de gestion de la relation client fournissent des données qui peuvent aider à établir des relations client, ce qui à son tour favorise la fidélité et favorise la rétention des clients. Experience Platform prend en charge l’assimilation de données CRM à partir de Microsoft Dynamics 365 et de Salesforce. Pour plus d’informations, consultez les documents connexes suivants :

- [Connecteur Microsoft Dynamics ](connectors/crm/ms-dynamics.md)
- [Connecteur Salesforce](connectors/crm/salesforce.md)

### Réussite des clients

Experience Platform prend en charge l’assimilation de données à partir d’une application de succès client tierce. Pour plus d’informations, consultez les documents connexes suivants :

- [Connecteur Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md)
- [Connecteur ServiceNow](connectors/customer-success/servicenow.md)

### Base de données

Experience Platform prend en charge l’assimilation de données à partir d’une base de données tierce. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur Amazon Redshift](connectors/databases/redshift.md)
- [Apache Hive sur le connecteur Azure HDInsights](connectors/databases/hive.md)
- [Apache Spark sur Azure HDInsights connector](connectors/databases/spark.md)
- [Connecteur Azure Data Explorer](connectors/databases/data-explorer.md)
- [Connecteur Azure Synapse Analytics](connectors/databases/synapse-analytics.md)
- [Connecteur d&#39;Enregistrement de table Azure](connectors/databases/ats.md)
- [Connecteur Google BigQuery](connectors/databases/bigquery.md)
- [Connecteur IBM DB2](connectors/databases/ibm-db2.md)
- [Connecteur MariaDB](connectors/databases/mariadb.md)
- [Connecteur Microsoft SQL Server](connectors/databases/sql-server.md)
- [Connecteur MySQL](connectors/databases/mysql.md)
- [Connecteur Oracle](connectors/databases/oracle.md)
- [Connecteur Phoenix](connectors/databases/phoenix.md)
- [Connecteur PostgreSQL](connectors/databases/postgres.md)

### Automatisation du marketing

Experience Platform prend en charge l’assimilation de données à partir d’un système d’automatisation marketing tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur HubSpot](connectors/marketing-automation/hubspot.md)

### Paiements

Experience Platform prend en charge l’importation de données à partir d’un système de paiement tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur PayPal](connectors/payments/paypal.md)

### Protocoles

Experience Platform prend en charge l’assimilation de données à partir d’un système de protocoles tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [Connecteur OData générique](connectors/protocols/odata.md)

## Contrôle d&#39;accès des sources dans l&#39;assimilation des données

Les autorisations relatives aux sources dans l’assimilation des données peuvent être gérées dans la console d’administration Adobe. Vous pouvez accéder aux autorisations par le biais de l’onglet *Autorisations* dans un profil de produits particulier. Dans le panneau **Modifier les autorisations** , vous pouvez accéder aux autorisations relatives aux sources par le biais de l’entrée de menu d’assimilation *des* données. L’autorisation Sources **de** Vue accorde un accès en lecture seule aux sources disponibles dans l’onglet *Catalogue* et aux sources authentifiées dans l’onglet *Parcourir* , tandis que l’autorisation **Gérer les sources accorde un accès complet à la lecture, à la création, à la modification et à la désactivation des sources.**

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction de différentes combinaisons de ces autorisations :

| Niveau d&#39;autorisation | Description |
| ---- | ----|
| **Sources** de Vue activées | Accordez un accès en lecture seule aux sources de chaque type de source dans l’onglet *Catalogue* , ainsi qu’aux onglets *Parcourir*, *Comptes* et *Flux de données.* |
| **Gérer les sources** sur | Outre les fonctions incluses dans les sources **de** Vue, accorde l&#39;accès à l&#39;option *Connect Source* dans le *catalogue* et à l&#39;option *Sélectionner les données dans Parcourir.*** **Gérer les sources** vous permet également d’activer ou de désactiver *DataFlows* et de modifier leurs planifications. |
| **Sources** de Vue désactivées et **gestion des sources** désactivées | Révoquer tous les accès aux sources. |

Pour plus d&#39;informations sur les autorisations disponibles accordées par le biais de la Console d&#39;administration, y compris ces quatre sources, consultez la présentation [du](../access-control/home.md)contrôle d&#39;accès.
