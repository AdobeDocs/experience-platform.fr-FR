---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteurs source;connecteurs source;sources;sources de données;source de données;connexion à la source de données.
solution: Experience Platform
title: Présentation des connecteurs source
topic-legacy: overview
description: Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: f0b8b5d16739b2bec6e1a11b718962de3faed463
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 98%

---

# Présentation des connecteurs source

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, les stockages dans le cloud, des bases de données, etc.

[!DNL Flow Service] est utilisé pour collecter et centraliser les données client provenant de diverses sources dans Platform. Le service fournit une interface utilisateur et une API RESTful qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Experience Platform vous permet de centraliser les données que vous collectez de sources disparates et d’utiliser les informations ainsi acquises pour aller plus loin.

## Types de sources

Les sources dans Experience Platform sont regroupées dans les catégories suivantes :

### Applications Adobe {#adobe-applications}

Experience Platform permet d’ingérer des données provenant d’autres applications Adobe, notamment Adobe Analytics et Adobe Audience Manager. Pour plus d’informations, consultez les documents connexes suivants :

- [Présentation du connecteur Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Créer une connexion source Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation de la connexion source données de classifications Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Créer une connexion de source de données de classifications Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/classifications.md)
- [Présentation de la connexion de source de données de la suite de rapports Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Créer une connexion source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Créer une connexion source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [Présentation du connecteur [!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
- [Créer une connexion source  [!DNL Marketo Engage]  dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/marketo.md)

### Publicité {#advertising}

Experience Platform prend en charge l’ingestion de données provenant d’un système publicitaire tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- Connecteur [[!DNL Google AdWords]](connectors/advertising/ads.md)

### Stockage dans le cloud {#cloud-storage}

Les sources de stockage dans le cloud peuvent introduire vos propres données dans Platform sans avoir à les télécharger, les formater ou les transférer. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. L’interface utilisateur permet d’intégrer chaque étape du processus dans le workflow des sources. Pour plus d’informations, consultez les documents connexes suivants :

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### Consentement et préférences {#consent}

Experience Platform prend en charge l’ingestion de données à partir d’une plateforme tierce de gestion des préférences et du consentement. Pour plus d’informations, consultez les documents connexes suivants :

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)


### Gestion de la relation client (CRM) {#customer-relationship-management}

Les systèmes de gestion de la relation client (CRM) fournissent des données qui peuvent aider à établir des relations avec la clientèle, qui à leur tour, favorisent la fidélisation client. Experience Platform prend en charge l’ingestion de données de gestion de la relation client (CRM) provenant de [!DNL Microsoft Dynamics 365] et de [!DNL Salesforce]. Pour plus d’informations, consultez les documents connexes suivants :

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Succès client {#customer-success}

Experience Platform prend en charge l’ingestion de données provenant d’une application de succès client tierce. Pour plus d’informations, consultez les documents connexes suivants :

- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)

### Base de données {#database}

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)

### eCommerce {#ecommerce}

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers d’eCommerce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Système local {#local-system}

Experience Platform prend en charge l’ingestion de données à partir de votre système local. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Téléchargement de fichier local](connectors/local-system/local-file-upload.md)

### Automatisation du marketing {#marketing-automation}

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers d’automatisation du marketing. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Paiements {#payments}

Experience Platform prend en charge l’ingestion de données provenant d’un système de paiement tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### Diffusion en continu {#streaming}

Experience Platform prend en charge l’ingestion de données à partir de sources de diffusion en continu. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protocoles {#protocols}

Experience Platform prend en charge l’ingestion de données provenant d’un système de protocoles tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## Contrôle d’accès des sources dans l’ingestion des données

Vous pouvez gérer les autorisations relatives aux sources dans l’ingestion des données dans Adobe Admin Console. Vous pouvez accéder aux autorisations via l’onglet **[!UICONTROL Autorisations]** d’un profil de produit particulier. Dans le panneau **[!UICONTROL Modifier les autorisations]**, vous pouvez accéder aux autorisations relatives aux sources à l’aide de l’entrée de menu **[!UICONTROL d’ingestion des données]**. L’autorisation **[!UICONTROL Afficher les sources]** accorde un accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**, tandis que l’autorisation **[!UICONTROL Gérer les sources]** donne un accès complet permettant de lire, créer, modifier et désactiver les sources.

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction des différentes combinaisons d’autorisations :

| Niveau d’autorisation | Description |
| ---- | ----|
| **[!UICONTROL Afficher les sources]** activée | Accordez un accès en lecture seule aux sources dans chaque type de source dans l’onglet Catalogue, ainsi que dans les onglets Parcourir, Comptes et Flux de données. |
| **[!UICONTROL Gérer les sources]** activée | Outre les fonctions incluses dans **[!UICONTROL Afficher les sources]**, elle accorde un accès à l’option **[!UICONTROL Connecter une source]** dans **[!UICONTROL Catalogue]** et l’option **[!UICONTROL Sélectionner les données]** dans **[!UICONTROL Parcourir]**. **[!UICONTROL Gérer les sources]** vous permet également d’activer ou de désactiver **[!UICONTROL les flux de données]** et de modifier leurs planifications. |
| **[!UICONTROL Afficher les sources]** désactivée et **[!UICONTROL Gérer les sources]** désactivée | Révoquez tous les accès aux sources. |

Pour plus d’informations sur les autorisations disponibles accordées à l’aide d’Admin Console, y compris ces quatre sources, consultez la [présentation du contrôle d’accès](../access-control/home.md).

## Conditions générales {#terms-and-conditions}

En utilisant l’une des sources libellées comme étant en version Beta (« Beta »), vous reconnaissez que la version Beta est fournie ***« telle quelle », sans garantie d’aucune sorte***.

Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge cette version Beta. Il est recommandé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de cette version Beta et/ou des éléments qui l’accompagnent. La version Beta est considérée comme étant une information confidentielle dʼAdobe.

Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts que vous rencontrez lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ce commentaire.

Envoyez vos commentaires ou créez un ticket dʼassistance pour partager vos suggestions, signaler un bug ou demander une amélioration de fonctionnalité.
