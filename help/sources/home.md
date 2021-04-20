---
keywords: Experience Platform ; accueil ; rubriques populaires ; connecteurs source ; connecteur source ; sources ; sources de données ; source de données ; connexion à la source de données
solution: Experience Platform
title: Présentation des connecteurs source
topic-legacy: overview
description: Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 57%

---

# Présentation des connecteurs source

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources, telles que des applications d’Adobe, des enregistrements basés sur le cloud, des bases de données, etc.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates au sein de Platform. Le service fournit une interface utilisateur et une API RESTful qui vous permettent de configurer facilement des connexions source à divers fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Experience Platform vous permet de centraliser les données que vous collectez de sources disparates et d’utiliser les informations ainsi acquises pour aller plus loin.

## Types de sources

Les sources dans Experience Platform sont regroupées dans les catégories suivantes :

### Applications Adobe

Experience Platform permet d’ingérer des données provenant d’autres applications Adobe, notamment Adobe Analytics, Adobe Audience Manager et [!DNL Experience Platform Launch]. Consultez les documents connexes suivants pour plus d’informations :

- [Présentation du connecteur Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Création d’une connexion source Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation du connecteur de données Classifications Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Création d’une connexion à la source de données des classifications Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/classifications.md)
- [Présentation du connecteur de données Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Création d’une connexion source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Création d’une connexion source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] présentation du connecteur](connectors/adobe-applications/marketo/marketo.md)
- [Créer une connexion  [!DNL Marketo Engage] source dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/marketo.md)

### Publicité

L’Experience Platform prend en charge l’importation de données à partir d’un système de publicité tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Google AdWords]](connectors/advertising/ads.md) connecteur

### Stockage dans le cloud

Les sources de stockage dans le cloud peuvent introduire vos propres données dans Platform sans avoir à les télécharger, les formater ou les transférer. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée au workflow des sources à l’aide de l’interface utilisateur. Consultez les documents connexes suivants pour plus d’informations :

- [[!DNL Azure Data Lake Storage Gen2] connecteur](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] connecteur](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] connecteur](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] connecteur](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] connecteur](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] connecteur](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] connecteur](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] connecteur](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] connecteur](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] connecteur](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] connecteur](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] connecteur](connectors/cloud-storage/sftp.md)

### Gestion de la relation client (CRM)

Les systèmes de gestion de la relation client (CRM) fournissent des données qui peuvent aider à établir des relations avec la clientèle, qui à leur tour, favorisent la fidélisation client. L’Experience Platform prend en charge l’assimilation de données de gestion de la relation client à partir de [!DNL Microsoft Dynamics 365] et [!DNL Salesforce]. Consultez les documents connexes suivants pour plus d’informations :

- [[!DNL Microsoft Dynamics] connecteur](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] connecteur](connectors/crm/salesforce.md)

### Réussite des clients

Experience Platform prend en charge l’ingestion de données provenant d’une application de succès client tierce. Consultez les documents connexes suivants pour plus d’informations :

- [[!DNL Salesforce Service Cloud] connecteur](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] connecteur](connectors/customer-success/servicenow.md)

### Base de données

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Amazon Redshift] connecteur](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] connecteur](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] connecteur](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] connecteur](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] connecteur](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] connecteur](connectors/databases/ats.md)
- [[!DNL Couchbase] connecteur](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] connecteur](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] connecteur](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] connecteur](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] connecteur](connectors/databases/ibm-db2.md)
- [[!DNL Microsoft SQL Server] connecteur](connectors/databases/sql-server.md)
- [[!DNL MySQL] connecteur](connectors/databases/mysql.md)
- [[!DNL Oracle] connecteur](connectors/databases/oracle.md)
- [[!DNL Phoenix] connecteur](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] connecteur](connectors/databases/postgres.md)

### eCommerce

L’Experience Platform prend en charge l’importation de données à partir d’un système de commerce électronique tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Automatisation du marketing

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers d’automatisation du marketing. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL HubSpot] connecteur](connectors/marketing-automation/hubspot.md)

### Paiements

L’Experience Platform prend en charge l’assimilation de données à partir d’un système de paiement tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL PayPal] connecteur](connectors/payments/paypal.md)

### Protocoles

Experience Platform fournit la prise en charge de l’assimilation de données à partir d’un système de protocoles tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Generic OData] connecteur](connectors/protocols/odata.md)

## Contrôle d’accès des sources dans l’ingestion des données

Vous pouvez gérer les autorisations relatives aux sources dans l’ingestion des données dans Adobe Admin Console. Vous pouvez accéder aux autorisations via l’onglet **[!UICONTROL Autorisations]** d’un profil de produit particulier. Dans le panneau **[!UICONTROL Modifier les autorisations]**, vous pouvez accéder aux autorisations relatives aux sources à l’aide de l’entrée de menu **[!UICONTROL d’ingestion des données]**. L’autorisation **[!UICONTROL Afficher les sources]** accorde un accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**, tandis que l’autorisation **[!UICONTROL Gérer les sources]** donne un accès complet permettant de lire, créer, modifier et désactiver les sources.

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction des différentes combinaisons d’autorisations :

| Niveau d’autorisation | Description |
| ---- | ----|
| **[!UICONTROL Afficher les sources]** activée | Accordez un accès en lecture seule aux sources de chaque type de source dans l’onglet Catalogue, ainsi qu’aux onglets Parcourir, Comptes et Flux de données. |
| **[!UICONTROL Gérer les sources]** activée | Outre les fonctions incluses dans **[!UICONTROL Afficher les sources]**, elle accorde un accès à l’option **[!UICONTROL Connecter une source]** dans **[!UICONTROL Catalogue]** et l’option **[!UICONTROL Sélectionner les données]** dans **[!UICONTROL Parcourir]**. **[!UICONTROL Gérer les sources]** vous permet également d’activer ou de désactiver **[!UICONTROL les flux de données]** et de modifier leurs planifications. |
| **[!UICONTROL Afficher les sources]** désactivée et **[!UICONTROL Gérer les sources]** désactivée | Révoquez tous les accès aux sources. |

Pour plus d’informations sur les autorisations disponibles accordées à l’aide d’Admin Console, y compris ces quatre sources, consultez la [présentation du contrôle d’accès](../access-control/home.md).

## Termes et conditions {#terms-and-conditions}

En utilisant l&#39;une des sources étiquetées bêta (&quot;Beta&quot;), Vous reconnaissez par la présente que la version bêta est fournie ***&quot;en l&#39;état&quot; sans garantie d&#39;aucune sorte***.

L&#39;Adobe n&#39;a aucune obligation de maintenir, corriger, mettre à jour, modifier, modifier ou prendre en charge la version bêta. Nous vous conseillons de faire preuve de prudence et de ne pas vous fier de quelque façon que ce soit au bon fonctionnement ou au bon fonctionnement de cette version bêta et/ou du matériel qui l&#39;accompagne. La version bêta est considérée comme une information confidentielle d’Adobe.

Toute &quot;évaluation&quot; (information concernant la version bêta, y compris mais sans s&#39;y limiter, les problèmes ou les défauts que vous rencontrez lors de l&#39;utilisation de la version bêta, les suggestions, les améliorations et les recommandations) fournie par Vous à l&#39;Adobe est par la présente attribuée à l&#39;Adobe, y compris tous les droits, titres et intérêts liés à ces commentaires.

Envoyez des commentaires en cours ou créez un ticket d&#39;assistance pour partager vos suggestions ou signaler un bogue. Recherchez une amélioration de fonctionnalité.
