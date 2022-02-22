---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteurs source;source;sources;sources de données;source de données;connexion à la source de données
solution: Experience Platform
title: Présentation des connecteurs source
topic-legacy: overview
description: Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 0154891cf2c68a38c08b9fe44251ec13325a7366
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 56%

---

# Présentation des connecteurs source

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, les stockages dans le cloud, des bases de données, etc.

[!DNL Flow Service] est utilisé pour collecter et centraliser des données client à partir de diverses sources disparates dans Platform. Le service fournit une interface utilisateur et une API RESTful qui vous permettent de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Experience Platform vous permet de centraliser les données que vous collectez de sources disparates et d’utiliser les informations ainsi acquises pour aller plus loin.

## Types de sources

Les sources dans Experience Platform sont regroupées dans les catégories suivantes :

### Applications Adobe

Experience Platform permet d’ingérer des données à partir d’autres applications Adobe, notamment Adobe Analytics et Adobe Audience Manager. Consultez les documents connexes suivants pour plus d’informations :

- [Présentation du connecteur Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Création d’une connexion source Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation de la connexion à la source de données Adobe Analytics Classifications](connectors/adobe-applications/classifications.md)
- [Création d’une connexion à la source de données Adobe Analytics Classifications dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/classifications.md)
- [Présentation de la connexion à la source de données de la suite de rapports Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Création d’une connexion source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Création d’une connexion source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] présentation du connecteur](connectors/adobe-applications/marketo/marketo.md)
- [Créez un [!DNL Marketo Engage] connexion source dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/marketo.md)

### Advertising

Experience Platform prend en charge l’ingestion de données à partir d’un système de publicité tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Google AdWords]](connectors/advertising/ads.md) connector

### Stockage dans le cloud

Les sources de stockage dans le cloud peuvent introduire vos propres données dans Platform sans avoir à les télécharger, les formater ou les transférer. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée au workflow des sources à l’aide de l’interface utilisateur. Consultez les documents connexes suivants pour plus d’informations :

- [[!DNL Azure Data Lake Storage Gen2] connector](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] connector](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] connector](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] connector](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] connector](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] connector](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] connector](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP] connector](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] connector](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] connector](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] connector](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] connector](connectors/cloud-storage/sftp.md)

### Gestion de la relation client (CRM)

Les systèmes de gestion de la relation client (CRM) fournissent des données qui peuvent aider à établir des relations avec la clientèle, qui à leur tour, favorisent la fidélisation client. Experience Platform prend en charge l’ingestion de données CRM à partir de [!DNL Microsoft Dynamics 365] et [!DNL Salesforce]. Consultez les documents connexes suivants pour plus d’informations :

- [[!DNL Microsoft Dynamics] connector](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] connector](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Succès des clients

Experience Platform prend en charge l’ingestion de données provenant d’une application de succès client tierce. Consultez les documents connexes suivants pour plus d’informations :

- [[!DNL Salesforce Service Cloud] connector](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] connector](connectors/customer-success/servicenow.md)

### Base de données

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Amazon Redshift] connector](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] connector](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] connector](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] connector](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] connector](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] connector](connectors/databases/ats.md)
- [[!DNL Couchbase] connector](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] connector](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] connector](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] connector](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] connector](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB] connector](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server] connector](connectors/databases/sql-server.md)
- [[!DNL MySQL] connector](connectors/databases/mysql.md)
- [[!DNL Oracle] connector](connectors/databases/oracle.md)
- [[!DNL Phoenix] connector](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] connector](connectors/databases/postgres.md)
- [[!DNL Snowflake] connector](connectors/databases/snowflake.md)

### eCommerce

Experience Platform prend en charge l’ingestion de données à partir d’un système eCommerce tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Système local

Experience Platform prend en charge l’ingestion de données à partir de votre système local. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Chargement de fichier local](connectors/local-system/local-file-upload.md)

### Automatisation du marketing

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers d’automatisation du marketing. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL MailChimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Paiements

Experience Platform prend en charge l’ingestion de données provenant d’un système de paiement tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL PayPal] connector](connectors/payments/paypal.md)

### Diffusion en continu

Experience Platform prend en charge l’ingestion de données à partir de sources de diffusion en continu. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protocoles

Experience Platform prend en charge l’ingestion de données à partir d’un système de protocoles tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## Contrôle d’accès des sources dans l’ingestion des données

Vous pouvez gérer les autorisations relatives aux sources dans l’ingestion des données dans Adobe Admin Console. Vous pouvez accéder aux autorisations via l’onglet **[!UICONTROL Autorisations]** d’un profil de produit particulier. Dans le panneau **[!UICONTROL Modifier les autorisations]**, vous pouvez accéder aux autorisations relatives aux sources à l’aide de l’entrée de menu **[!UICONTROL d’ingestion des données]**. L’autorisation **[!UICONTROL Afficher les sources]** accorde un accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**, tandis que l’autorisation **[!UICONTROL Gérer les sources]** donne un accès complet permettant de lire, créer, modifier et désactiver les sources.

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction des différentes combinaisons d’autorisations :

| Niveau d’autorisation | Description |
| ---- | ----|
| **[!UICONTROL Afficher les sources]** activée | Accordez un accès en lecture seule aux sources dans chaque type de source dans l’onglet Catalogue , ainsi que dans les onglets Parcourir, Comptes et Flux de données . |
| **[!UICONTROL Gérer les sources]** activée | Outre les fonctions incluses dans **[!UICONTROL Afficher les sources]**, elle accorde un accès à l’option **[!UICONTROL Connecter une source]** dans **[!UICONTROL Catalogue]** et l’option **[!UICONTROL Sélectionner les données]** dans **[!UICONTROL Parcourir]**. **[!UICONTROL Gérer les sources]** vous permet également d’activer ou de désactiver **[!UICONTROL les flux de données]** et de modifier leurs planifications. |
| **[!UICONTROL Afficher les sources]** désactivée et **[!UICONTROL Gérer les sources]** désactivée | Révoquez tous les accès aux sources. |

Pour plus d’informations sur les autorisations disponibles accordées à l’aide d’Admin Console, y compris ces quatre sources, consultez la [présentation du contrôle d’accès](../access-control/home.md).

## Conditions d’utilisation {#terms-and-conditions}

En utilisant l’une des sources libellées bêta (&quot;Beta&quot;), Vous reconnaissez que la version bêta est fournie. ***&quot;en l’état&quot; sans aucune garantie***.

Adobe n’a aucune obligation de gérer, corriger, mettre à jour, modifier, modifier ou prendre en charge la version bêta. Nous vous conseillons de faire preuve de prudence et de ne pas vous fier de quelque manière que ce soit au bon fonctionnement ou aux bonnes performances d’une telle version bêta et/ou du matériel d’accompagnement. La version bêta est considérée comme des informations confidentielles d’Adobe.

Tout &quot;retour&quot; (informations relatives à la version bêta, y compris, mais sans s’y limiter, aux problèmes ou défauts que vous rencontrez lors de l’utilisation de la version bêta, suggestions, améliorations et recommandations) fourni par Vous à l’Adobe est affecté à l’Adobe, y compris tous les droits, titres et intérêts dans et à ces commentaires.

Envoyez des commentaires d’ouverture ou créez un ticket d’assistance pour partager vos suggestions ou signaler un bogue, recherchez une amélioration des fonctionnalités.
