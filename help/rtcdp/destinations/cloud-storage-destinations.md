---
title: Destinations de stockage dans le cloud
seo-title: Destinations de stockage dans le cloud
description: Adobe Real-time CDP peut diffuser vos segments sous forme de fichiers de données vers vos emplacements d’enregistrement cloud Amazon S3, AWS Kinesis, Azure Événement Hubs ou SFTP.
seo-description: Adobe Real-time CDP peut diffuser vos segments sous forme de fichiers de données vers vos emplacements d’enregistrement cloud Amazon S3, AWS Kinesis, Azure Événement Hubs ou SFTP.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 34%

---


# Destinations de stockage dans le cloud {#cloud-storage-destinations}

Adobe Real-time CDP peut diffuser vos segments sous forme de fichiers de données vers vos emplacements d’enregistrement Cloud. Cela vous permet d’envoyer des audiences et leurs attributs de profil à vos systèmes internes, au moyen de fichiers CSV ou délimités par des tabulations pour Amazon S3 et SFTP. Pour les destinations AWS Kinesis et Azure Événement Hubs, les données sont extraites en flux continu de la plate-forme Experience au format JSON.

![ Destinations de stockage dans Adobe Cloud](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Pour plus d’informations sur la connexion aux destinations de stockage dans le cloud, voir [Processus de création de destinations de stockage dans le cloud](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

## Type d’exportation de données

**Exportation basée sur les profils** : vous exportez des détails sur les individus de l’audience. Ces détails sont nécessaires à la personnalisation et peuvent inclure des attributs, des événements, des appartenances à des segments, etc.

## Destinations d’enregistrement Cloud disponibles

* [Destination Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md)
* [Destination SFTP](/help/rtcdp/destinations/sftp-destination.md)

## Destinations de diffusion en continu de l’enregistrement Cloud disponibles

* [Destination Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Destination Azure EventHubs](/help/rtcdp/destinations/azure-event-hubs-destination.md)