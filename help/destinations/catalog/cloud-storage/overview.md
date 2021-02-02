---
keywords: destination de l’enregistrement cloud ; enregistrement cloud
title: Destinations de stockage dans le cloud
seo-title: Destinations de stockage dans le cloud
description: Platform peut diffuser vos segments sous forme de fichiers de données vers vos emplacements d’enregistrement cloud Amazon S3, AWS Kinesis, Azure Événement Hubs ou SFTP.
seo-description: Platform peut diffuser vos segments sous forme de fichiers de données vers vos emplacements d’enregistrement cloud Amazon S3, AWS Kinesis, Azure Événement Hubs ou SFTP.
translation-type: tm+mt
source-git-commit: b348a5493b13112291dd8e9234d457ff8c694147
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 32%

---


# Destinations de stockage dans le cloud {#cloud-storage-destinations}

Adobe Experience Platform peut distribuer vos segments sous forme de fichiers de données vers vos emplacements d’enregistrement Cloud. Vous pouvez ainsi envoyer des audiences et leurs attributs de profil à vos systèmes internes, au moyen de fichiers CSV ou délimités par des tabulations pour [!DNL Amazon S3] et SFTP. Pour les destinations [!DNL AWS Kinesis] et [!DNL Azure Event Hubs], les données sont diffusées en flux continu en dehors de l’Experience Platform au format JSON.

![Destinations des enregistrements de cloud d’Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Pour plus d’informations sur la connexion aux destinations de stockage dans le cloud, voir [Processus de création de destinations de stockage dans le cloud](./workflow.md).

## Type d’exportation de données

**Exportation basée sur les profils** : vous exportez des détails sur les individus de l’audience. Ces détails sont nécessaires à la personnalisation et peuvent inclure des attributs, des événements, des appartenances à des segments, etc.

## Destinations d’enregistrement de cloud disponibles

- [Destination Amazon S3](./amazon-s3.md)
- [Destination de l&#39;objet blob Azure](./azure-blob.md)
- [Destination SFTP](./sftp.md)

## Destinations de diffusion en continu de l’enregistrement cloud disponibles

- [Destination Amazon](./amazon-kinesis.md)
- [Destination des centres de Événement Azure](./azure-event-hubs.md)