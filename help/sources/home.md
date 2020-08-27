---
keywords: Experience Platform;home;popular topics;source connectors;source connector;sources;data sources;data source;data source connection
solution: Experience Platform
title: Présentation des connecteurs source Adobe Experience Platform
topic: overview
description: Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 53%

---


# Présentation des connecteurs source

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

With [!DNL Experience Platform], you can centralize data you collect from disparate sources and use the insights gained from it to do more.

## Types de sources

Sources in [!DNL Experience Platform] are grouped into the following categories:

### Applications Adobe

[!DNL Experience Platform] permet d’importer des données à partir d’autres applications d’Adobe, notamment Adobe Analytics, Adobe Audience Manager et [!DNL Experience Platform Launch]. Consultez les documents connexes suivants pour plus d’informations :

- [Présentation du connecteur Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Création d’un connecteur source Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation du connecteur de données Classifications Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Création d’un connecteur de source de données de classifications Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/classifications.md)
- [Présentation du connecteur de données Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Création d’un connecteur source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Création d’un connecteur source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicité

[!DNL Experience Platform] prend en charge l’importation de données à partir d’un système de publicité tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Connecteur [ !DNL Google AdWords]](connectors/advertising/ads.md)

### Stockage dans le cloud

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée au workflow des sources à l’aide de l’interface utilisateur. Consultez les documents connexes suivants pour plus d’informations :

- [Connecteur [ !DNL Azure Data Lake Enregistrement Gen2]](connectors/cloud-storage/adls-gen2.md)
- [Connecteur [ !DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [Connecteur [ !DNL Amazon]](connectors/cloud-storage/kinesis.md)
- [Connecteur [ !DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [Connecteur [ ! DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [Connecteur [ ! DNL Azure Événement Hubs]](connectors/cloud-storage/eventhub.md)
- [Connecteur [ ! DNL Azure File Enregistrement]](connectors/cloud-storage/azure-file-storage.md)
- [Connecteur [ !DNL FTP et SFTP]](connectors/cloud-storage/ftp-sftp.md)
- [Connecteur [ ! DNL Google Cloud Enregistrement]](connectors/cloud-storage/google-cloud-storage.md)

### Gestion de la relation client (CRM)

Les systèmes de gestion de la relation client (CRM) fournissent des données qui peuvent aider à établir des relations avec la clientèle, qui à leur tour, favorisent la fidélisation client. [!DNL Experience Platform] prend en charge l’assimilation de données de gestion de la relation client à partir de [!DNL Microsoft Dynamics 365] et [!DNL Salesforce]. Consultez les documents connexes suivants pour plus d’informations :

- [Connecteur [ !DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [Connecteur [ !DNL Salesforce]](connectors/crm/salesforce.md)

### Réussite des clients

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’une application de succès client tierce. Consultez les documents connexes suivants pour plus d’informations :

- [Connecteur [ !DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [Connecteur [ !DNL ServiceNow]](connectors/customer-success/servicenow.md)

### Base de données

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’une base de données tierce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Connecteur [ !DNL Amazon Redshift]](connectors/databases/redshift.md)
- [Connecteur [ !DNL Apache Hive sur Azure HDInsights]](connectors/databases/hive.md)
- [Connecteur [ ! DNL Apache Spark sur Azure HDInsights]](connectors/databases/spark.md)
- [Connecteur [ !DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [Connecteur [ !DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [Connecteur [ ! DNL Azure Table Enregistrement]](connectors/databases/ats.md)
- [Connecteur [ !DNL Couchbase]](connectors/databases/couchbase.md)
- [Connecteur [ !DNL Google BigQuery]](connectors/databases/bigquery.md)
- [Connecteur [ !DNL GreenPlum]](connectors/databases/greenplum.md)
- [Connecteur [ !DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [Connecteur [ !DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [Connecteur [ !DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [Connecteur [ !DNL MySQL]](connectors/databases/mysql.md)
- [Connecteur [ !DNL Oracle]](connectors/databases/oracle.md)
- [Connecteur [ !DNL Phoenix]](connectors/databases/phoenix.md)
- [Connecteur [ !DNL PostgreSQL]](connectors/databases/postgres.md)

### Automatisation du marketing

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’un système tiers d’automatisation du marketing. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Connecteur [ !DNL HubSpot]](connectors/marketing-automation/hubspot.md)

### Paiements

[!DNL Experience Platform] prend en charge l’importation de données à partir d’un système de paiement tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Connecteur [ !DNL PayPal]](connectors/payments/paypal.md)

### Protocoles

[!DNL Experience Platform] prend en charge l’importation de données à partir d’un système de protocoles tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Connecteur [ !DNL Generic OData]](connectors/protocols/odata.md)

## Contrôle d’accès des sources dans l’ingestion des données

Vous pouvez gérer les autorisations relatives aux sources dans l’ingestion des données dans Adobe Admin Console. Vous pouvez accéder aux autorisations via l’onglet *[!UICONTROL Autorisations]* d’un profil de produit particulier. Dans le panneau **[!UICONTROL Modifier les autorisations]**, vous pouvez accéder aux autorisations relatives aux sources à l’aide de l’entrée de menu *[!UICONTROL d’ingestion des données]*. L’autorisation **[!UICONTROL Afficher les sources]** accorde un accès en lecture seule aux sources disponibles dans l’onglet *[!UICONTROL Catalogue]* et aux sources authentifiées dans l’onglet *[!UICONTROL Parcourir]*, tandis que l’autorisation **[!UICONTROL Gérer les sources]** donne un accès complet permettant de lire, créer, modifier et désactiver les sources.

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction des différentes combinaisons d’autorisations :

| Niveau d’autorisation | Description |
| ---- | ----|
| **[!UICONTROL Afficher les sources]** activée | Accordez un accès en lecture seule aux sources dans chaque type de source dans l’onglet *Catalogue*, ainsi que dans les onglets *Parcourir*, *Comptes* et *Flux de données*. |
| **[!UICONTROL Gérer les sources]** activée | Outre les fonctions incluses dans **[!UICONTROL Afficher les sources]**, elle accorde un accès à l’option *[!UICONTROL Connecter une source]* dans *[!UICONTROL Catalogue]* et l’option *[!UICONTROL Sélectionner les données]* dans *[!UICONTROL Parcourir]*. **[!UICONTROL Gérer les sources]** vous permet également d’activer ou de désactiver *[!UICONTROL les flux de données]* et de modifier leurs planifications. |
| **[!UICONTROL Afficher les sources]** désactivée et **[!UICONTROL Gérer les sources]** désactivée | Révoquez tous les accès aux sources. |

Pour plus d’informations sur les autorisations disponibles accordées à l’aide d’Admin Console, y compris ces quatre sources, consultez la [présentation du contrôle d’accès](../access-control/home.md).

## Termes et conditions {#terms-and-conditions}

En utilisant l&#39;une des sources étiquetées bêta (&quot;bêta&quot;), Vous reconnaissez que la version bêta est fournie ***&quot;telle quelle&quot; sans aucune garantie***.

L&#39;Adobe n&#39;a aucune obligation de maintenir, corriger, mettre à jour, modifier, modifier ou prendre en charge la version bêta. Nous vous conseillons de faire preuve de prudence et de ne pas vous fier de quelque façon que ce soit au bon fonctionnement ou au bon fonctionnement de cette version bêta et/ou du matériel qui l&#39;accompagne. La version bêta est considérée comme une information confidentielle d’Adobe.

Toute &quot;évaluation&quot; (information concernant la version bêta, y compris mais sans s&#39;y limiter, les problèmes ou les défauts que vous rencontrez lors de l&#39;utilisation de la version bêta, les suggestions, les améliorations et les recommandations) fournie par Vous à l&#39;Adobe est par la présente attribuée à l&#39;Adobe, y compris tous les droits, titres et intérêts liés à ces commentaires.

Envoyez des commentaires en cours ou créez un ticket d&#39;assistance pour partager vos suggestions ou signaler un bogue. Recherchez une amélioration de fonctionnalité.
