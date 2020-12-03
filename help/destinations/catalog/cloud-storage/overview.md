---
keywords: cloud storage destination;cloud storage
title: Destinations de stockage dans le cloud
seo-title: Destinations de stockage dans le cloud
description: Le CDP en temps réel peut fournir vos segments sous forme de fichiers de données à vos emplacements d’enregistrement cloud Amazon S3, AWS Kinesis, Azure Événement Hubs ou SFTP.
seo-description: Le CDP en temps réel peut fournir vos segments sous forme de fichiers de données à vos emplacements d’enregistrement cloud Amazon S3, AWS Kinesis, Azure Événement Hubs ou SFTP.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 36%

---


# Destinations de stockage dans le cloud {#cloud-storage-destinations}

Le CDP en temps réel peut fournir vos segments sous forme de fichiers de données à vos emplacements d’enregistrement Cloud. This enables you to send audiences and their profile attributes to your internal systems, via CSV or tab-delimited files for [!DNL Amazon S3] and SFTP. Pour [!DNL AWS Kinesis] et [!DNL Azure Event Hubs] les destinations, les données sont diffusées en flux continu hors de l’Experience Platform au format JSON.

![ Destinations de stockage dans Adobe Cloud](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Pour plus d’informations sur la connexion aux destinations de stockage dans le cloud, voir [Processus de création de destinations de stockage dans le cloud](./workflow.md).

## Type d’exportation de données

**Exportation basée sur les profils** : vous exportez des détails sur les individus de l’audience. Ces détails sont nécessaires à la personnalisation et peuvent inclure des attributs, des événements, des appartenances à des segments, etc.

## Destinations d’enregistrement Cloud disponibles

- [Destination Amazon S3](./amazon-s3.md)
- [Destination SFTP](./sftp.md)

## Destinations de diffusion en continu de l’enregistrement Cloud disponibles

- [Destination Amazon](./amazon-kinesis.md)
- [Destination des centres de Événement Azure](./azure-event-hubs.md)