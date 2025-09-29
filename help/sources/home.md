---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteurs source;connecteurs source;sources;sources de données;source de données;connexion à la source de données
solution: Experience Platform
title: Présentation des connecteurs source
description: Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 55%

---

# Présentation des connecteurs source

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, les stockages dans le cloud, les bases de données, etc.

[!DNL Flow Service] est utilisé pour collecter et centraliser les données client provenant de diverses sources dans Experience Platform. Le service fournit une interface utilisateur et une API RESTful qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Experience Platform vous permet de centraliser les données que vous collectez de sources disparates et d’utiliser les informations ainsi acquises pour aller plus loin.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

>[!BEGINSHADEBOX]

## Sources créées par Adobe et par les partenaires {#adobe-and-partner-built-sources}

Certains des connecteurs du catalogue de sources Experience Platform sont créés et gérés par Adobe, tandis que d’autres sont créés et gérés par des sociétés partenaires à l’aide de [Sources SDK](/help/sources/sources-sdk/overview.md). Une note en haut de la page de documentation pour chaque connecteur créé par le partenaire indique si une source est créée et gérée par le partenaire. Par exemple, le connecteur [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) est créé par Adobe, tandis que le connecteur [RainFocus](/help/sources/connectors/analytics/rainfocus.md) est créé et géré par l’équipe RainFocus.

Pour les connecteurs créés et gérés par un partenaire, les problèmes liés au connecteur peuvent devoir être résolus par l’équipe du partenaire (la méthode de contact est fournie dans la note de la page de documentation). Pour tout problème concernant les connecteurs créés et gérés par Adobe, contactez votre personne représentante d’Adobe ou l’Assistance clientèle.

>[!ENDSHADEBOX]

## Catalogue des sources

Lisez les sections suivantes pour obtenir la liste de toutes les sources disponibles dans le catalogue des sources.

### Applications Adobe {#adobe-applications}

Experience Platform permet d’ingérer des données provenant d’autres applications Adobe, notamment Adobe Analytics et Adobe Audience Manager. Pour plus d’informations, consultez les documents connexes suivants :

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Créer une connexion source Adobe Audience Manager dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Données de classifications Adobe Analytics](connectors/adobe-applications/classifications.md)
   - [Créer une connexion de source de données de classifications Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/classifications.md)
- [Données de suite de rapports Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Créer une connexion source Adobe Analytics dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Créer une connexion source Adobe Campaign Managed Cloud Services à l’aide de l’interface utilisateur de Platform](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Collection de données Adobe](connectors/adobe-applications/data-collection.md)
   - [Créer une connexion source Attributs du client dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Créer une connexion source  [!DNL Marketo Engage]  dans l’interface utilisateur](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Créer une connexion source et  [!DNL Marketo Engage]  flux de données pour les données d’activité personnalisées](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Sources d’entreprise avancées {#advanced-enterprise-sources}

Les sources suivantes sont disponibles uniquement pour les clients [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

| Source | Catégorie | Type d’ingestion | Cloud |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | Stockage cloud | Diffusion en continu | Azure, AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | Base de données | Lot | Azure, AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | Base de données | Lot | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | Espace de stockage dans le cloud | Diffusion en continu | Azure, AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | Base de données | Lot | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | Base de données | Lot | Azure, AWS |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | Espace de stockage dans le cloud | Diffusion en continu | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | Base de données | Diffusion en continu | Azure, AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | Base de données | Lot | Azure, AWS |

{style="table-layout:auto"}

### Advertising {#advertising}

Vous pouvez utiliser les sources suivantes pour ingérer des données publicitaires dans Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [Google Ads](connectors/advertising/ads.md) | Lot | Azure |

{style="table-layout:auto"}

### Analytics {#analytics}

Vous pouvez utiliser les sources suivantes pour ingérer des données d’analyse dans Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | Lot | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | Diffusion en continu | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | Diffusion en continu | Azure |

{style="table-layout:auto"}

### Espace de stockage dans le cloud {#cloud-storage}

Les sources de stockage dans le cloud peuvent importer vos propres données dans Experience Platform sans avoir à les télécharger, les formater ou les charger. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. L’interface utilisateur permet d’intégrer chaque étape du processus dans le workflow des sources. Pour plus d’informations, consultez les documents connexes suivants :

Vous pouvez utiliser les sources suivantes pour ingérer des données d’espace de stockage vers Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | Lot | Azure |
| [[!DNL Azure Blob Storage]](connectors/cloud-storage/blob.md) | Lot | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | Lot | Azure, AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | Lot | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | Lot | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | Lot | Azure, AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | Lot | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | Lot | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | Lot | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | Lot | Azure |

{style="table-layout:auto"}

### Consentement et préférences {#consent}

Vous pouvez utiliser les sources suivantes pour ingérer des données de consentement et de préférences vers Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Didomi]](../sources/connectors/consent-and-preferences/didomi.md) | Diffusion en continu | Azure |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | Lot | Azure |

{style="table-layout:auto"}

### Gestion de la relation client (CRM) {#customer-relationship-management}

Les systèmes de gestion de la relation client (CRM) fournissent des données qui peuvent aider à établir des relations avec la clientèle, qui à leur tour, favorisent la fidélisation de la clientèle. Experience Platform prend en charge l’ingestion de données de gestion de la relation client (CRM) provenant de [!DNL Microsoft Dynamics 365] et de [!DNL Salesforce]. Pour plus d’informations, consultez les documents connexes suivants :

Vous pouvez utiliser les sources suivantes pour ingérer des données CRM dans Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | Lot | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | Lot | Azure, AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | Lot | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | Lot | Azure |

{style="table-layout:auto"}

### Succès client {#customer-success}

Vous pouvez utiliser les sources suivantes pour ingérer des données de succès client dans Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | Lot | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | Lot | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | Lot | Azure |

{style="table-layout:auto"}

### Base de données {#database}

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Consultez les documents connexes suivants pour plus d’informations sur des connecteurs source spécifiques :

Vous pouvez utiliser les sources suivantes pour ingérer des données de votre base de données vers Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | Lot | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | Lot | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | Lot | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | Lot | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | Lot | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | Lot | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | Lot | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | Lot | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | Lot | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | Lot | Azure, AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | Lot | Azure, AWS |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | Lot | Azure, AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | Lot | Azure |

{style="table-layout:auto"}

### Partenaires de données et d’identité {#data-partner}

Vous pouvez utiliser les sources suivantes pour ingérer des données et des données de partenaire d’identité dans Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | Lot | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | Lot | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | Lot | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | Lot | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | Lot | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | Lot | Azure |

{style="table-layout:auto"}

### commerce électronique {#ecommerce}

Vous pouvez utiliser les sources suivantes pour ingérer des données d’e-commerce vers Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | Lot | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | Lot | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | Diffusion en continu | Azure |

{style="table-layout:auto"}

### Système local {#local-system}

Vous pouvez utiliser les sources suivantes pour ingérer des données à partir de votre système local vers Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [Téléchargement de fichiers locaux](connectors/local-system/local-file-upload.md) | Lot | Azure |

{style="table-layout:auto"}

### Fidélité {#loyalty}

Vous pouvez utiliser les sources suivantes pour ingérer la fidélité des données à Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Capillary Streaming Events]](connectors/loyalty/capillary.md) | Diffusion en continu | Azure |

{style="table-layout:auto"}

### Automatisation du marketing {#marketing-automation}

Vous pouvez utiliser les sources suivantes pour ingérer des données d’automatisation du marketing dans Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | Diffusion en continu | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | Diffusion en continu | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | Diffusion en continu | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | Lot | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | Lot | Azure |
| [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) | Lot | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | Lot | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | Lot | Azure |
| [[!DNL Relay Connector]](tutorials/ui/create/marketing-automation/relay-connector.md) | Diffusion en continu | Azure |
| [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) | Lot | Azure, AWS |

{style="table-layout:auto"}

### Paiements {#payments}

Vous pouvez utiliser les sources suivantes pour ingérer des données de paiements dans Experience Platform.

| Source | Type d’ingestion | Cloud |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | Lot | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | Lot | Azure |

{style="table-layout:auto"}

### Diffusion en continu {#streaming}

Vous pouvez utiliser les sources suivantes pour diffuser des données vers Experience Platform.

| Source | Type d’ingestion | Prise en charge du cloud |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | Diffusion en continu | Azure, AWS |

{style="table-layout:auto"}

### Protocoles {#protocols}

Vous pouvez utiliser les sources suivantes pour ingérer des données de protocole vers Experience Platform.

| Source | Type d’ingestion | Prise en charge du cloud |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | Lot | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | Lot | Azure |

{style="table-layout:auto"}

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
>Le fonctionnement du contrôle d’accès basé sur les attributs est le suivant : les **rôles** sont créés pour catégoriser les types d’utilisateurs qui interagissent avec votre instance Experience Platform. Les **libellés** sont appliqués aux **rôles** pour désigner l’accès de ce rôle donné. Les **libellés** sont également appliqués aux ressources telles que les champs de schéma et les segments. Pour qu’un utilisateur ait accès à certains segments et champs de schéma, il doit être ajouté à *un rôle avec le même libellé que celui attribué à la ressource interrogée*. Pour plus d’informations, consultez le guide [complet du contrôle d’accès basé sur les attributs](../access-control/abac/end-to-end-guide.md).

- Appliquez des libellés aux champs de schéma pour définir l’accès à des champs de schéma spécifiques dans votre organisation. Une fois l’accès à des champs de schéma spécifiques établi, les utilisateurs ne pourront créer des mappages que pour les champs auxquels ils ont accès.
- Les utilisateurs ne disposant pas des rôles appropriés ne pourront pas créer ni mettre à jour des flux de données avec des mappages impliquant des champs de schéma inaccessibles. En outre, les utilisateurs non autorisés ne peuvent pas mettre à jour, supprimer, activer ou désactiver les flux de données existants avec des champs de schéma inaccessibles.
- En outre, un flux de données doit avoir exactement le même identifiant de schéma et la même version dans son mappage, son jeu de données cible et sa connexion cible. Cela s’applique à la fois aux schémas XDM standard et aux schémas basés sur des modèles.

>[!NOTE]
>
>Les schémas basés sur des modèles comportent des exigences supplémentaires, notamment les champs clé primaire et identifiant de version . Pour plus d’informations, consultez la présentation du schéma [basé sur un modèle](../xdm/schema/model-based.md).

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../access-control/abac/overview.md).

## Conditions générales {#terms-and-conditions}

En utilisant l’une des sources libellées comme étant en version Beta (« Beta »), vous reconnaissez que la version Beta est fournie ***« telle quelle », sans garantie d’aucune sorte***.

Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge cette version Beta. Il est conseillé d’utiliser le Beta et/ou les éléments qui l’accompagnent pour vous informer et de ne pas vous fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ce dernier. La version Beta est considérée comme étant une information confidentielle dʼAdobe.

Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts rencontrés lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ces commentaires.

Envoyez vos commentaires ou créez un ticket dʼassistance pour partager vos suggestions, signaler un bug ou demander une amélioration de fonctionnalité.
