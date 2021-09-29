---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: b616a0c0d49d980644f82bc3af5995b3b17b4c80
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 59%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 29 septembre 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [Sources](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des flux de données en continu | Vous pouvez désormais utiliser des fonctions de prétraitement de données lors de la création d’un flux de données en continu pour [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] et [!DNL Google PubSub]. Pour plus d’informations, consultez le tutoriel sur la [création d’un flux de données en continu pour les sources de stockage dans le cloud](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) . |

Pour en savoir plus sur [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Data Landing Zone] | Vous pouvez désormais créer une connexion source [!DNL Data Landing Zone] à l’aide de l’[[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) ou de l’[interface utilisateur](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] est une interface de  [!DNL Azure Blob] stockage configurée par Platform, qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour ingérer et extraire des fichiers dans et hors de Platform. Pour de plus amples informations, rendez-vous sur la [[!DNL Data Landing Zone]  d’aperçu](../../sources/connectors/cloud-storage/data-landing-zone.md). |
| [!DNL Snowflake] | Vous pouvez désormais créer une connexion source [!DNL Snowflake] à l’aide de l’[[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) ou de l’[interface utilisateur](../../sources/tutorials/ui/create/databases/snowflake.md) pour importer les données de votre base de données [!DNL Snowflake] vers Platform. Pour de plus amples informations, rendez-vous sur la [[!DNL Snowflake]  d’aperçu](../../sources/connectors/databases/snowflake.md). |
| [!DNL SFTP] améliorations de la source | Vous pouvez définir manuellement un numéro de port personnalisé lors de la création d’une connexion source [!DNL SFTP]. Pour de plus amples informations, rendez-vous sur la [[!DNL SFTP]  d’aperçu](../../sources/connectors/cloud-storage/sftp.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
