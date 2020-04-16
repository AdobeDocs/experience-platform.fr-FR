---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des connecteurs de source Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: e81f138f933d4bb2c36260480e360dfacd412da0

---


# Présentation des connecteurs source

Adobe Experience Platform permet d’assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plateforme. Vous pouvez assimiler des données à partir de diverses sources, telles que des applications Adobe, des  basés sur le cloud, des bases de données et bien d’autres.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à divers fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’exécution pour l’assimilation et de gérer le débit d’assimilation des données.

Avec Experience Platform, vous pouvez centraliser les données que vous collectez à partir de sources disparates et utiliser les informations qui en découlent pour en faire plus.

## Types de sources

Les sources dans la plateforme d’expérience sont regroupées dans le  suivant :

### Applications Adobe

Experience Platform permet d’assimiler des données à partir d’autres applications Adobe, notamment Adobe Analytics, Adobe  Gestionnaire de  et Experience Platform Launch. Pour plus d’informations, reportez-vous aux  connexes suivantes :

- [Présentation du connecteur  Gestionnaire de Adobe](connectors/adobe-applications/audience-manager.md)
- [Création d’un connecteur source Adobe   Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation du connecteur de données Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Création d’un connecteur source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Création d’un connecteur source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicité

Experience Platform prend en charge l’importation de données à partir d’un système de publicité tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux  connexes suivants :

- [Connecteur de publicités Google](connectors/advertising/ads.md)

### Stockage dans le cloud

Cloud  sources de peuvent importer vos propres données dans Platform sans avoir à les télécharger, les mettre en forme ou les télécharger. Les données insérées peuvent être formatées au format JSON XDM, parquet XDM ou délimitées. Chaque étape du processus est intégrée dans le flux de travaux Sources à l’aide de l’interface utilisateur. Pour plus d’informations, reportez-vous aux  connexes suivantes :

- [Connecteur  Azure Data Lake  Gen2](connectors/cloud-storage/adls-gen2.md)
- [Connecteur Azure Blob et Amazon S3](connectors/cloud-storage/blob-s3.md)
- [Connecteur FTP et SFTP](connectors/cloud-storage/ftp-sftp.md)
- [Google Cloud connecteur](connectors/cloud-storage/google-cloud-storage.md)

### Gestion de la relation client

Les systèmes de gestion de la relation client fournissent des données qui peuvent aider à établir des relations avec la clientèle, ce qui, à son tour, favorise la fidélité et favorise la rétention des clients. Experience Platform prend en charge l’assimilation de données CRM à partir de Microsoft Dynamics 365 et de Salesforce. Pour plus d’informations, reportez-vous aux  connexes suivantes :

- [Connecteur Microsoft Dynamics ](connectors/crm/ms-dynamics.md)
- [Connecteur Salesforce](connectors/crm/salesforce.md)

### Succès des clients

Experience Platform prend en charge l’assimilation de données à partir d’une application de succès cliente tierce. Pour plus d’informations, reportez-vous aux  connexes suivantes :

- [Connecteur Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md)
- [Connecteur ServiceNow](connectors/customer-success/servicenow.md)

### Base de données

Experience Platform prend en charge l’assimilation de données à partir d’une base de données tierce. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux  connexes suivants :

- [Connecteur Amazon Redshift](connectors/databases/redshift.md)
- [Apache Hive sur le connecteur HDInsights Azure](connectors/databases/hive.md)
- [Apache Spark sur le connecteur HDInsights Azure](connectors/databases/spark.md)
- [Connecteur Azure Synapse Analytics](connectors/databases/synapse-analytics.md)
- [de table Azure connecteur](connectors/databases/ats.md)
- [Connecteur Google BigQuery](connectors/databases/bigquery.md)
- [Connecteur MariaDB](connectors/databases/mariadb.md)
- [Connecteur Microsoft SQL Server](connectors/databases/sql-server.md)
- [Connecteur MySQL](connectors/databases/mysql.md)
- [Connecteur Phoenix](connectors/databases/phoenix.md)
- [Connecteur PostgreSQL](connectors/databases/postgres.md)

### Automatisation du marketing

Experience Platform prend en charge l’importation de données à partir d’un système tiers d’automatisation du marketing. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux  connexes suivants :

- [Connecteur HubSpot](connectors/marketing-automation/hubspot.md)

### Paiements

Experience Platform prend en charge l’importation de données à partir d’un système de paiement tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux  connexes suivants :

- [Connecteur PayPal](connectors/payments/paypal.md)

### Protocoles

Experience Platform prend en charge l’assimilation de données à partir d’un système de protocoles tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux  connexes suivants :

- [Connecteur OData générique](connectors/protocols/odata.md)

## pour les sources dans l’assimilation des données

Les autorisations relatives aux sources dans l’assimilation des données peuvent être gérées dans la console d’administration Adobe. Vous pouvez accéder aux autorisations via l’onglet *Autorisations* d’un  de produit particulier. Dans le panneau **Modifier les autorisations** , vous pouvez accéder aux autorisations relatives aux sources par le biais de l’entrée de menu d’importation *de* données. L’autorisation Sources **** accorde un accès en lecture seule aux sources disponibles dans l’onglet *Catalogue* et aux sources authentifiées dans l’onglet *Parcourir* , tandis que l’autorisation **Gérer les sources donne un accès complet aux sources de lecture, de création, de modification et de désactivation.**

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction de différentes combinaisons de ces autorisations :

| Niveau d&#39;autorisation | Description |
| ---- | ----|
| **Sources**  activées | Accordez un accès en lecture seule aux sources dans chaque type de source dans l’onglet *Catalogue* , ainsi qu’aux onglets *Parcourir*, *Comptes* et *Flux de données.* |
| **Gérer les sources** le | Outre les fonctions incluses dans les sources **de**, l’option *Connect Source* est accessible dans le *catalogue* et l’option *Sélectionner les données dans le de navigation.*** **Gérer les sources** vous permet également d’activer ou de désactiver *les flux* de données et de modifier leurs planifications. |
| **Sources**  désactivées et **gestion des sources** désactivées | Révoquez tous les accès aux sources. |

Pour plus d&#39;informations sur les autorisations disponibles accordées par le biais de la Console d&#39;administration, y compris ces quatre sources, consultez la présentation [du](../access-control/home.md).
