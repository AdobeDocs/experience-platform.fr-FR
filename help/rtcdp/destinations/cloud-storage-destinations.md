---
title: Destinations de stockage dans le cloud
seo-title: Destinations de stockage dans le cloud
description: Adobe Le CDP en temps réel peut fournir vos segments sous forme de fichiers de données à vos emplacements d’enregistrement cloud Amazon S3, AWS Kinesis, Azure Événement Hubs ou SFTP.
seo-description: Adobe Le CDP en temps réel peut fournir vos segments sous forme de fichiers de données à vos emplacements d’enregistrement cloud Amazon S3, AWS Kinesis, Azure Événement Hubs ou SFTP.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 35%

---


# Destinations de stockage dans le cloud {#cloud-storage-destinations}

Adobe Le CDP en temps réel peut fournir vos segments sous forme de fichiers de données à vos emplacements d’enregistrement Cloud. This enables you to send audiences and their profile attributes to your internal systems, via CSV or tab-delimited files for [!DNL Amazon S3] and SFTP. Pour [!DNL AWS Kinesis] et [!DNL Azure Event Hubs] les destinations, les données sont diffusées en flux continu hors de l’Experience Platform au format JSON.

![ Destinations de stockage dans Adobe Cloud](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Pour plus d’informations sur la connexion aux destinations de stockage dans le cloud, voir [Processus de création de destinations de stockage dans le cloud](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

## Type d’exportation de données

**Exportation basée sur les profils** : vous exportez des détails sur les individus de l’audience. Ces détails sont nécessaires à la personnalisation et peuvent inclure des attributs, des événements, des appartenances à des segments, etc.

## Destinations d’enregistrement Cloud disponibles

* [Destination Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md)
* [Destination SFTP](/help/rtcdp/destinations/sftp-destination.md)

## Destinations de diffusion en continu de l’enregistrement Cloud disponibles

* [Destination Amazon](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Destination des centres de Événement Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)