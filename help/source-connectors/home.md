---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des connecteurs de source Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 291d669cc0f5b009b23dc2771688ee54b53d08db

---


# Présentation des connecteurs source

Adobe Experience Platform permet d’assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plateforme. Vous pouvez assimiler des données à partir de diverses sources, telles que des applications Adobe, des  basés sur le cloud, des bases de données et bien d’autres.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à divers fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’exécution pour l’assimilation et de gérer le débit d’assimilation des données.

Avec Experience Platform, vous pouvez centraliser les données que vous collectez à partir de sources disparates et utiliser les informations qui en découlent pour en faire plus.

## Types de sources

Les sources dans la plateforme d’expérience sont regroupées dans le  suivant :

### Applications Adobe

Experience Platform permet d’assimiler des données à partir d’autres applications Adobe, notamment Adobe Analytics, Adobe  Gestionnaire de  et Experience Platform Launch. Pour plus d’informations, reportez-vous aux  connexes suivantes :

- [Présentation du connecteur  Gestionnaire de Adobe](./ui/adobe-applications/audience-manager.md)
- [Création d’un connecteur source Adobe   Manager dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)
- [Présentation du connecteur de données Adobe Analytics](./ui/adobe-applications/analytics.md)
- [Création d’un connecteur source Adobe Analytics dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)

### Stockage dans le cloud

Cloud  sources de peuvent importer vos propres données dans Platform sans avoir à les télécharger, les mettre en forme ou les télécharger. Chaque étape du processus est intégrée dans le flux de travaux Sources à l’aide de l’interface utilisateur. La prise en charge des fournisseurs de Cloud  les fournisseurs Amazon S3, Azure Blob, les serveurs FTP et les serveurs SFTP sont également pris en charge. Pour plus d’informations, reportez-vous aux  connexes suivantes :

- [Création d’un connecteur source Azure Blob ou Amazon S3 dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/amazon-s3-ui-tutorial.md)
- [Création d&#39;un connecteur source Azure Data Lake   Gen2 dans l&#39;interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/adls-gen2-ui-tutorial.md)
- [Création d’un connecteur source FTP ou SFTP dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/ftp-sftp-ui-tutorial.md)
- [Création d’un connecteur  source de Google Cloud  dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/google-cloud-storage-ui-tutorial.md)

### Gestion de la relation client

Les systèmes de gestion de la relation client fournissent des données qui peuvent aider à établir des relations avec la clientèle, ce qui, à son tour, favorise la fidélité et favorise la rétention des clients. Experience Platform prend en charge l’assimilation de données CRM à partir de Microsoft Dynamics 365 et de Salesforce. Pour plus d’informations, reportez-vous aux  connexes suivantes :

- [Création d’un connecteur source Microsoft Dynamics 365 ou Salesforce dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/dynamics-salesforce-ui-tutorial.md)
- [Création d’un connecteur source PayPal dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/paypal-tutorial.md)

### Succès des clients (CS)

Experience Platform prend en charge l’assimilation de données à partir d’une application de succès cliente tierce. Pour plus d’informations, reportez-vous aux  connexes suivantes :

- [Création d’un connecteur source Salesforce Service Cloud dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/salesforce-service-cloud-tutorial.md)
- [Création d’un connecteur source ServiceNow dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/servicenow-ui-tutorial.md)

### Base de données

Experience Platform prend en charge l’assimilation de données à partir d’une base de données tierce. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux  connexes suivants :

- [Création d’un connecteur source AWS Redshift dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/amazon-redshift-ui-tutorial.md)
- [Création d’un connecteur source Azure Synapse Analytics dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/azure-synapse-analytics-ui-tutorial.md)
- [Création d’un connecteur source Google BigQuery dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/google-big-query-ui-tutorial.md)
- [Création d’un connecteur source MariaDB dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/database-nosql/mariadb-api-tutorial.md)
- [Création d’un connecteur source Microsoft SQL Server dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/sql-server-ui-tutorial.md)
- [Création d’un connecteur source MySQL dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/mysql-ui-tutorial.md)
- [Création d’un connecteur source PostgreSQL dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/postgresql-tutorial.md)

### Automatisation du marketing

Experience Platform prend en charge l’importation de données à partir d’un système tiers d’automatisation du marketing. Pour plus d’informations sur des connecteurs source spécifiques, reportez-vous aux  connexes suivants :

- [Création d’un connecteur source HubSpot dans l’interface utilisateur](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/marketing-automation/hubspot-tutorial.md)

## Didacticiels sur les API

Vous pouvez créer des connecteurs source à l’aide de l’API du service de flux. Pour plus d’informations, reportez-vous au didacticiel sur l’API [sources](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md).

## pour les sources dans l’assimilation des données

Les autorisations relatives aux sources dans l’assimilation des données peuvent être gérées dans la console d’administration Adobe. Vous pouvez accéder aux autorisations via l’onglet *Autorisations* d’un  de produit particulier. Dans le panneau **Modifier les autorisations** , vous pouvez accéder aux autorisations relatives aux sources par le biais de l’entrée de menu d’importation *de* données. L’autorisation Sources **** accorde un accès en lecture seule aux sources disponibles dans l’onglet *Catalogue* et aux sources authentifiées dans l’onglet *Parcourir* , tandis que l’autorisation **Gérer les sources donne un accès complet aux sources de lecture, de création, de modification et de désactivation.**

Le tableau suivant décrit le comportement de l’interface utilisateur en fonction de différentes combinaisons de ces autorisations :

| Niveau d&#39;autorisation | Description |
| ---- | ----|
| **Sources**  activées | Accordez un accès en lecture seule aux sources dans chaque type de source dans l’onglet *Catalogue* , ainsi qu’aux onglets *Parcourir*, *Comptes* et *Flux de données.* |
| **Gérer les sources** le | Outre les fonctions incluses dans les sources **de**, l’option *Connect Source* est accessible dans le *catalogue* et l’option *Sélectionner les données dans le de navigation.*** **Gérer les sources** vous permet également d’activer ou de désactiver *les flux* de données et de modifier leurs planifications. |
| **Sources**  désactivées et **gestion des sources** désactivées | Révoquez tous les accès aux sources. |

Pour plus d&#39;informations sur les autorisations disponibles accordées par le biais de la Console d&#39;administration, y compris ces quatre sources, consultez la présentation [du](../access-control/home.md).
