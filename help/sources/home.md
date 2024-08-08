---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteurs source;connecteurs source;sources;sources de données;source de données;connexion à la source de données
solution: Experience Platform
title: Présentation des connecteurs source
description: Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 8541af0e2c0a2f5709f1621877ca204b0d3d64bd
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 73%

---

# Présentation des connecteurs source

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, les stockages dans le cloud, des bases de données, etc.

[!DNL Flow Service] est utilisé pour collecter et centraliser les données client provenant de diverses sources dans Platform. Le service fournit une interface utilisateur et une API RESTful qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Experience Platform vous permet de centraliser les données que vous collectez de sources disparates et d’utiliser les informations ainsi acquises pour aller plus loin.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Sources d’entreprise avancées {#advanced-enterprise-sources}

Les sources suivantes sont disponibles uniquement pour les clients [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE Diffusion en continu]{type=Positive}
- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE Diffusion en continu]{type=Positive}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE Diffusion en continu]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE Diffusion en continu]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE Batch]{type=Informative}

## Sources construites par les Adobes et construites par les partenaires {#adobe-and-partner-built-sources}

Certains des connecteurs du catalogue des sources Experience Platform sont créés et gérés par Adobe, tandis que d’autres sont créés et gérés par des sociétés partenaires à l’aide du [SDK Sources](/help/sources/sources-sdk/overview.md). Une note en haut de la page de documentation pour chaque connecteur créé par un partenaire indique si une source est créée et gérée par le partenaire. Par exemple, le [connecteur Amazon S3](/help/sources/connectors/cloud-storage/s3.md) est créé par Adobe, tandis que le [connecteur RainFocus](/help/sources/connectors/analytics/rainfocus.md) est créé et géré par l’équipe RainFocus.

Pour les connecteurs créés et gérés par un partenaire, les problèmes liés au connecteur peuvent devoir être résolus par l’équipe du partenaire (la méthode de contact est fournie dans la note de la page de documentation). Pour tout problème concernant les connecteurs créés et gérés par Adobe, contactez votre personne représentante d’Adobe ou l’Assistance clientèle.

## Catégories de sources

Les sources dans Experience Platform sont regroupées dans les catégories suivantes :

### Applications Adobe {#adobe-applications}

Experience Platform permet d’ingérer des données provenant d’autres applications Adobe, notamment Adobe Analytics et Adobe Audience Manager. Pour plus d’informations, consultez les documents connexes suivants :

- [Présentation de la source Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Créer une connexion source Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Présentation de la source de données de classifications Adobe Analytics](connectors/adobe-applications/classifications.md)
   - [Créer une connexion de source de données de classifications Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/classifications.md)
- [Présentation de source de données de la suite de rapports Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Créer une connexion source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Présentation de la source Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Créer une connexion source Adobe Campaign Managed Cloud Services à l’aide de l’interface utilisateur de Platform](./tutorials/ui/create/adobe-applications/campaign.md)
- [Présentation de la source Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Présentation de la source de collecte de données Adobe](connectors/adobe-applications/data-collection.md)
   - [Créer une connexion source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [Présentation de la source [!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Créer une connexion source  [!DNL Marketo Engage]  dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Création d’une connexion source et d’un flux de données pour les données d’activité personnalisées [!DNL Marketo Engage] ](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Publicité {#advertising}

Experience Platform prend en charge l’ingestion de données provenant d’un système publicitaire tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Google Ads](connectors/advertising/ads.md) [!BADGE Batch]{type=Informative}

### Analytics {#analytics}

Experience Platform prend en charge l’ingestion de données provenant d’un système Analytics tiers. Pour plus d’informations, lisez les documents connexes suivants :

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE Batch]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE Diffusion en continu]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE Diffusion en continu]{type=Positive}

### Stockage dans le cloud {#cloud-storage}

Les sources de stockage dans le cloud peuvent introduire vos propres données dans Platform sans avoir à les télécharger, les formater ou les transférer. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. L’interface utilisateur permet d’intégrer chaque étape du processus dans le workflow des sources. Pour plus d’informations, consultez les documents connexes suivants :

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE Batch]{type=Informative}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE Batch]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE Batch]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE Batch]{type=Informative}

### Consentement et préférences {#consent}

Experience Platform prend en charge l’ingestion de données à partir d’une plateforme tierce de gestion des préférences et du consentement. Pour plus d’informations, consultez les documents connexes suivants :

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE Batch]{type=Informative}

### Gestion de la relation client (CRM) {#customer-relationship-management}

Les systèmes de gestion de la relation client (CRM) fournissent des données qui peuvent aider à établir des relations avec la clientèle, qui à leur tour, favorisent la fidélisation client. Experience Platform prend en charge l’ingestion de données de gestion de la relation client (CRM) provenant de [!DNL Microsoft Dynamics 365] et de [!DNL Salesforce]. Pour plus d’informations, consultez les documents connexes suivants :

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE Batch]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE Batch]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE Batch]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE Batch]{type=Informative}

### Succès client {#customer-success}

Experience Platform prend en charge l’ingestion de données provenant d’une application de succès client tierce. Pour plus d’informations, consultez les documents connexes suivants :

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE Batch]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE Batch]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE Batch]{type=Informative}

### Base de données {#database}

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE Batch]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE Batch]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE Batch]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE Batch]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE Batch]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE Batch]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE Batch]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE Batch]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE Batch]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE Batch]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE Batch]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE Batch]{type=Informative}

### Partenaires de données et d’identité {#data-partner}

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) [!BADGE Batch]{type=Informative}
- [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) [!BADGE Batch]{type=Informative}
- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE Batch]{type=Informative}

### eCommerce {#ecommerce}

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers d’eCommerce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE Batch]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE Batch]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE Diffusion en continu]{type=Positive}

### Système local {#local-system}

Experience Platform prend en charge l’ingestion de données à partir de votre système local. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [Téléchargement de fichier local](connectors/local-system/local-file-upload.md)

### Automatisation du marketing {#marketing-automation}

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers d’automatisation du marketing. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Braze]](connectors/marketing-automation/braze.md) [!BADGE Diffusion en continu]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE Diffusion en continu]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE Diffusion en continu]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE Batch]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE Batch]{type=Informative}
- [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE Batch]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Paiements {#payments}

Experience Platform prend en charge l’ingestion de données provenant d’un système de paiement tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE Batch]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE Batch]{type=Informative}
- [[!DNL Stripe]](connectors/payments/stripe.md) [!BADGE Batch]{type=Informative}

### Diffusion en continu {#streaming}

Experience Platform prend en charge l’ingestion de données à partir de sources de diffusion en continu. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE Diffusion en continu]{type=Positive}

### Protocoles {#protocols}

Experience Platform prend en charge l’ingestion de données provenant d’un système de protocoles tiers. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE Batch]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE Batch]{type=Informative}

## Contrôle d’accès des sources dans l’ingestion des données

Vous pouvez gérer les autorisations relatives aux sources dans l’ingestion des données dans Adobe Admin Console. Vous pouvez accéder aux autorisations via l’onglet **[!UICONTROL Autorisations]** d’un profil de produit particulier. Dans le panneau **[!UICONTROL Modifier les autorisations]**, vous pouvez accéder aux autorisations relatives aux sources à l’aide de l’entrée de menu **[!UICONTROL d’ingestion des données]**. L’autorisation **[!UICONTROL Afficher les sources]** accorde un accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**, tandis que l’autorisation **[!UICONTROL Gérer les sources]** donne un accès complet permettant de lire, créer, modifier et désactiver les sources.

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction des différentes combinaisons d’autorisations :

| Niveau d’autorisation | Description |
| ---- | ----|
| **[!UICONTROL Afficher les sources]** activée | Accordez un accès en lecture seule aux sources dans chaque type de source dans l’onglet Catalogue, ainsi que dans les onglets Parcourir, Comptes et Flux de données. |
| **[!UICONTROL Gérer les sources]** activée | Outre les fonctions incluses dans **[!UICONTROL Afficher les sources]**, elle accorde un accès à l’option **[!UICONTROL Connecter une source]** dans **[!UICONTROL Catalogue]** et l’option **[!UICONTROL Sélectionner les données]** dans **[!UICONTROL Parcourir]**. **[!UICONTROL Gérer les sources]** vous permet également d’activer ou de désactiver **[!UICONTROL les flux de données]** et de modifier leurs planifications. |
| **[!UICONTROL Afficher les sources]** désactivée et **[!UICONTROL Gérer les sources]** désactivée | Révoquez tous les accès aux sources. |

Pour plus d’informations sur les autorisations disponibles accordées par le biais des autorisations d’Adobe, consultez la [présentation du contrôle d’accès](../access-control/home.md).

### Contrôle d’accès basé sur les attributs

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs.

Grâce au contrôle d’accès basé sur les attributs, vous pouvez appliquer des configurations de mappage aux champs pour lesquels vous disposez d’autorisations. En outre, vous ne pouvez pas ingérer de données dans un jeu de données si vous n’avez pas accès à tous les champs du jeu de données.

#### Prise en charge du contrôle d’accès basé sur les attributs dans les sources

>[!TIP]
>
>Le contrôle d’accès basé sur les attributs fonctionne comme suit : **rôles** sont créés pour classer les types d’utilisateurs qui interagissent avec votre instance Platform. **Les libellés** sont appliqués à **rôles** pour désigner l’accès à ce rôle donné. **Les libellés** sont également appliqués aux ressources telles que les champs de schéma et les segments. Pour qu’un utilisateur ait accès à certains champs de schéma et segments, ils doivent être ajoutés à *un rôle avec le même libellé affecté à la ressource interrogée*. Pour plus d’informations, consultez le [guide de bout en bout du contrôle d’accès basé sur les attributs](../access-control/abac/end-to-end-guide.md).

- Appliquez des libellés aux champs de schéma pour définir l’accès à des champs de schéma spécifiques de votre entreprise. Une fois l’accès à des champs de schéma spécifiques établi, les utilisateurs ne pourront créer des mappages que pour les champs auxquels ils ont accès.
- Les utilisateurs ne disposant pas des rôles appropriés ne pourront pas créer ni mettre à jour des flux de données avec des mappages qui impliquent des champs de schéma inaccessibles. En outre, les utilisateurs non autorisés ne peuvent pas mettre à jour, supprimer, activer ou désactiver les flux de données existants avec des champs de schéma inaccessibles.
- En outre, un flux de données doit avoir exactement le même identifiant de schéma et la même version dans son mappage, son jeu de données cible et sa connexion cible.

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../access-control/abac/overview.md).

## Conditions générales {#terms-and-conditions}

En utilisant l’une des sources libellées comme étant en version Beta (« Beta »), vous reconnaissez que la version Beta est fournie ***« telle quelle », sans garantie d’aucune sorte***.

Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge cette version Beta. Nous vous conseillons d’utiliser l’ Informatif et de ne pas vous fier de quelque manière que ce soit au bon fonctionnement ou aux bonnes performances de ce Beta et/ou du matériel d’accompagnement. La version Beta est considérée comme étant une information confidentielle dʼAdobe.

Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts rencontrés lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ces commentaires.

Envoyez vos commentaires ou créez un ticket dʼassistance pour partager vos suggestions, signaler un bug ou demander une amélioration de fonctionnalité.
