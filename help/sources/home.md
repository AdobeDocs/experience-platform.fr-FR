---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des connecteurs de source d'Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---


# Présentation des connecteurs source

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Vous pouvez ingérer des données à partir de diverses sources, telles que des applications Adobe, des enregistrements basés sur le cloud, des bases de données, etc.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à divers fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir les heures d’exécution pour l’assimilation et de gérer le débit d’assimilation des données.

Vous [!DNL Experience Platform]pouvez ainsi centraliser les données que vous collectez à partir de sources disparates et utiliser les connaissances acquises pour en faire plus.

## Types de sources

Les sources dans [!DNL Experience Platform] sont regroupées dans les catégories suivantes :

### Applications Adobe

[!DNL Experience Platform] permet l’assimilation de données à partir d’autres applications Adobe, y compris Adobe Analytics, Adobe Audience Manager et [!DNL Experience Platform Launch]. Pour plus d’informations, consultez les documents connexes suivants :

- [Présentation du connecteur d&#39;Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Création d’un connecteur de source d’Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation du connecteur de données Adobe](connectors/adobe-applications/analytics.md)
- [Création d’un connecteur source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Création d’un connecteur source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Publicité

[!DNL Experience Platform] prend en charge l’importation de données à partir d’un système de publicité tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [!DNL Google AdWords](connectors/advertising/ads.md) connecteur

### Stockage dans le cloud

Les sources d’enregistrement Cloud peuvent importer vos propres données [!DNL Platform] sans avoir à les télécharger, les mettre en forme ou les télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources à l’aide de l’interface utilisateur. Pour plus d’informations, consultez les documents connexes suivants :

- [!DNL Azure Data Lake Storage Gen2](connectors/cloud-storage/adls-gen2.md) connecteur
- [!DNL Azure Blob and Amazon S3](connectors/cloud-storage/blob-s3.md) connecteur
- [!DNL Amazon Kinesis](connectors/cloud-storage/kinesis.md) connecteur
- [!DNL Apache HDFS](connectors/cloud-storage/hdfs.md) connecteur
- [!DNL Azure Event Hubs](connectors/cloud-storage/eventhub.md) connecteur
- [!DNL Azure File Storage](connectors/cloud-storage/azure-file-storage.md) connecteur
- [!DNL FTP and SFTP](connectors/cloud-storage/ftp-sftp.md) connecteur
- [!DNL Google Cloud Storage](connectors/cloud-storage/google-cloud-storage.md) connecteur

### Gestion de la relation client

Les systèmes de gestion de la relation client fournissent des données qui peuvent aider à établir des relations client, ce qui à son tour favorise la fidélité et favorise la rétention des clients. [!DNL Experience Platform] prend en charge l’assimilation de données de gestion de la relation client à partir de [!DNL Microsoft Dynamics 365] et [!DNL Salesforce]. Pour plus d’informations, consultez les documents connexes suivants :

- [!DNL Microsoft Dynamics](connectors/crm/ms-dynamics.md) connecteur
- [!DNL Salesforce](connectors/crm/salesforce.md) connecteur

### Réussite des clients

[!DNL Experience Platform] prend en charge l’importation de données à partir d’une application de succès client tierce. Pour plus d’informations, consultez les documents connexes suivants :

- [!DNL Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md) connecteur
- [!DNL ServiceNow](connectors/customer-success/servicenow.md) connecteur

### Base de données

[!DNL Experience Platform] prend en charge l’importation de données à partir d’une base de données tierce. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [!DNL Amazon Redshift](connectors/databases/redshift.md) connecteur
- [!DNL Apache Hive on Azure HDInsights](connectors/databases/hive.md) connecteur
- [!DNL Apache Spark on Azure HDInsights](connectors/databases/spark.md) connecteur
- [!DNL Azure Data Explorer](connectors/databases/data-explorer.md) connecteur
- [!DNL Azure Synapse Analytics](connectors/databases/synapse-analytics.md) connecteur
- [!DNL Azure Table Storage](connectors/databases/ats.md) connecteur
- [!DNL Couchbase](connectors/databases/couchbase.md) connecteur
- [!DNL Google BigQuery](connectors/databases/bigquery.md) connecteur
- [!DNL GreenPlum](connectors/databases/greenplum.md) connecteur
- [!DNL HP Vertica](connectors/databases/hp-vertica.md) connecteur
- [!DNL IBM DB2](connectors/databases/ibm-db2.md) connecteur
- [!DNL MariaDB](connectors/databases/mariadb.md) connecteur
- [!DNL Microsoft SQL Server](connectors/databases/sql-server.md) connecteur
- [!DNL MySQL](connectors/databases/mysql.md) connecteur
- [!DNL Oracle](connectors/databases/oracle.md) connecteur
- [!DNL Phoenix](connectors/databases/phoenix.md) connecteur
- [!DNL PostgreSQL](connectors/databases/postgres.md) connecteur

### Automatisation du marketing

[!DNL Experience Platform] prend en charge l’importation de données à partir d’un système tiers d’automatisation du marketing. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [!DNL HubSpot](connectors/marketing-automation/hubspot.md) connecteur

### Paiements

[!DNL Experience Platform] prend en charge l’importation de données à partir d’un système de paiement tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [!DNL PayPal](connectors/payments/paypal.md) connecteur

### Protocoles

[!DNL Experience Platform] prend en charge l’importation de données à partir d’un système de protocoles tiers. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux documents connexes suivants :

- [!DNL Generic OData](connectors/protocols/odata.md) connecteur

## Contrôle d&#39;accès des sources dans l&#39;assimilation des données

Les autorisations pour les sources dans l’assimilation de données peuvent être gérées dans l’Adobe Admin Console. Vous pouvez accéder aux autorisations par le biais de l’onglet *[!UICONTROL Autorisations]* dans un profil de produits particulier. Dans le panneau **[!UICONTROL Modifier les autorisations]** , vous pouvez accéder aux autorisations relatives aux sources par le biais de l’entrée de menu d’assimilation *[!UICONTROL des]* données. L’autorisation Sources **[!UICONTROL de]** Vue accorde un accès en lecture seule aux sources disponibles dans l’onglet *[!UICONTROL Catalogue]* et aux sources authentifiées dans l’onglet *[!UICONTROL Parcourir]* , tandis que l’autorisation **[!UICONTROL Gérer les sources accorde un accès complet à la lecture, à la création, à la modification et à la désactivation des sources.]**

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction de différentes combinaisons de ces autorisations :

| Niveau d&#39;autorisation | Description |
| ---- | ----|
| **[!UICONTROL Sources]** de Vue activées | Accordez un accès en lecture seule aux sources de chaque type de source dans l’onglet *Catalogue* , ainsi qu’aux onglets *Parcourir*, *Comptes* et *Flux de données.* |
| **[!UICONTROL Gérer les sources]** sur | Outre les fonctions incluses dans les sources **[!UICONTROL de]** Vue, accorde l&#39;accès à l&#39;option *[!UICONTROL Connect Source]* dans le *[!UICONTROL catalogue]* et à l&#39;option *[!UICONTROL Sélectionner les données dans Parcourir.]*** **[!UICONTROL Gérer les sources]** vous permet également d’activer ou de désactiver *[!UICONTROL DataFlows]* et de modifier leurs planifications. |
| **[!UICONTROL Sources]** de Vue désactivées et **[!UICONTROL gestion des sources]** désactivées | Révoquer tous les accès aux sources. |

Pour plus d’informations sur les autorisations disponibles accordées par l’intermédiaire de l’Admin Console, y compris ces quatre sources, voir l’aperçu [du](../access-control/home.md)contrôle d&#39;accès.

## Termes et conditions {#terms-and-conditions}

En utilisant l&#39;une des sources étiquetées bêta (&quot;bêta&quot;), Vous reconnaissez que la version bêta est fournie ***&quot;telle quelle&quot; sans aucune garantie***.

Adobe n&#39;a aucune obligation de maintenir, corriger, mettre à jour, modifier, modifier ou prendre en charge la version bêta. Nous vous conseillons de faire preuve de prudence et de ne pas vous fier de quelque façon que ce soit au bon fonctionnement ou au bon fonctionnement de cette version bêta et/ou du matériel qui l&#39;accompagne. La version bêta est considérée comme une information confidentielle d’Adobe.

Toute &quot;évaluation&quot; (information concernant la version bêta, y compris mais sans s&#39;y limiter, les problèmes ou les défauts que vous rencontrez lors de l&#39;utilisation de la version bêta, suggestions, améliorations et recommandations) fournie par Vous à Adobe est par la présente attribuée à Adobe, y compris tous les droits, titres et intérêts liés à ces commentaires.

Envoyez des commentaires en cours ou créez un ticket d&#39;assistance pour partager vos suggestions ou signaler un bogue. Recherchez une amélioration de fonctionnalité.
