---
title: Notes de mise à jour d’Adobe Experience Platform - Septembre 2021
description: Les notes de mise à jour de septembre 2021 pour Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 64%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 29 septembre 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Ingestion de données](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Sources](#sources)

## Ingestion de données {#ingestion}

L’ingestion des données Adobe Experience Platform représente les différentes méthodes par lesquelles Experience Platform ingère des données provenant de diverses sources, ainsi que la manière dont ces données sont conservées dans le lac de données pour être utilisées par les services Experience Platform en aval.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Mise à jour upsert ou correction des enregistrements de profil à l’aide de l’ingestion par lots | Le profil client en temps réel permet désormais de mettre à jour les attributs de profil dans les données d’enregistrements de profils individuels via l’ingestion par lots. Pour en savoir plus, consultez le [Guide du développeur de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md). |

Pour en savoir plus sur l’ingestion de données dans Experience Platform, consultez la [documentation sur l’ingestion de données](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des flux de données en continu | Vous pouvez désormais utiliser les fonctions de préparation de données lors de la création d’un flux de données en continu pour [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] et [!DNL Google PubSub]. Pour plus d’informations, consultez le tutoriel sur la [création d’un flux de données en continu pour des sources de stockage cloud](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md). |

Pour en savoir plus sur [!DNL Data Prep], consultez la présentation de [[!DNL Data Prep] &#x200B;](../../data-prep/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Data Landing Zone] | Vous pouvez désormais créer une connexion source [!DNL Data Landing Zone] à l’aide de l’API [[!DNL Flow Service] &#x200B;](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) ou de l’[interface utilisateur](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] est une interface de stockage [!DNL Azure Blob] fournie par Experience Platform. Elle vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour importer des fichiers dans Experience Platform. Pour plus d’informations, consultez la [[!DNL Data Landing Zone] présentation](../../sources/connectors/cloud-storage/data-landing-zone.md).  |
| [!DNL Snowflake] | Vous pouvez désormais créer une connexion source [!DNL Snowflake] à l’aide de l’API [&#128279;](../../sources/tutorials/api/create/databases/snowflake.md) [!DNL Flow Service]  ou de l’interface utilisateur [&#128279;](../../sources/tutorials/ui/create/databases/snowflake.md)  pour importer les données de votre base de données [!DNL Snowflake] vers Experience Platform. Pour plus d’informations, consultez la [[!DNL Snowflake] présentation](../../sources/connectors/databases/snowflake.md). |
| Améliorations de la source [!DNL SFTP] | Vous pouvez définir manuellement un numéro de port personnalisé lors de la création d’une connexion source [!DNL SFTP]. Pour plus d’informations, consultez la [[!DNL SFTP] présentation](../../sources/connectors/cloud-storage/sftp.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
