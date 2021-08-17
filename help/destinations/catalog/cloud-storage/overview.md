---
keywords: destination de stockage dans le cloud;espace de stockage dans le cloud
title: Présentation des destinations de stockage dans le cloud
description: Adobe Experience Platform peut diffuser vos segments sous forme de fichiers de données vers vos emplacements de stockage dans le cloud Amazon S3, AWS Kinesis, Azure Event Hubs ou SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 2%

---

# Présentation des destinations de stockage dans le cloud {#cloud-storage-destinations}

## Présentation {#overview}

Adobe Experience Platform peut fournir vos segments sous forme de fichiers de données aux emplacements de stockage dans le cloud. Vous pouvez ainsi envoyer des audiences et leurs attributs de profil à vos systèmes internes par le biais de fichiers CSV ou délimités par des tabulations pour [!DNL Amazon S3], [!DNL Azure Blob] et SFTP. Pour les destinations [!DNL Amazon Kinesis] et [!DNL Azure Event Hubs], les données sont diffusées en continu hors de l’Experience Platform au format [!DNL JSON].

![Destinations de stockage dans le cloud Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinations de stockage dans le cloud prises en charge {#supported-destinations}

Adobe Experience Platform prend en charge les destinations de stockage dans le cloud suivantes :

* [Connexion à Amazon Kinesis](amazon-kinesis.md)
* [Connexion à Amazon S3](amazon-s3.md)
* [Connexion Azure Blob](azure-blob.md)
* [Connexion à Azure Event Hubs](azure-event-hubs.md)
* [Connexion SFTP](sftp.md)

## Connexion à une nouvelle destination de stockage dans le cloud {#connect-destination}

Pour envoyer des segments aux destinations de stockage dans le cloud pour vos campagnes, Platform doit d’abord se connecter à la destination. Pour plus d’informations sur la configuration d’une nouvelle destination, consultez le [tutoriel sur la création de destination](../../ui/connect-destination.md) .


## Utilisation de macros pour créer un dossier à l’emplacement de stockage {#use-macros}

>[!NOTE]
>
> Les fonctionnalités décrites dans cette section sont actuellement disponibles uniquement pour les destinations [Amazon S3](amazon-s3.md).

Pour créer un dossier personnalisé par fichier de segment à l’emplacement de stockage, vous pouvez utiliser des macros dans le champ d’entrée Chemin du dossier. Insérez les macros à la fin du champ de saisie, comme illustré ci-dessous.

![Utilisation des macros pour créer un dossier dans votre stockage](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Les exemples ci-dessous font référence à un exemple de segment `Luxury Audience` avec l’ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1 :`%SEGMENT_NAME%`**

Entrée : `acme/campaigns/2021/%SEGMENT_NAME%`
Chemin du dossier dans l’emplacement de stockage : `acme/campaigns/2021/Luxury Audience`

**Macro 2 :`%SEGMENT_ID%`**

Entrée : `acme/campaigns/2021/%SEGMENT_ID%`
Chemin du dossier dans l’emplacement de stockage : `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3 :`%SEGMENT_NAME%/%SEGMENT_ID%`**

Entrée : `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Chemin du dossier dans l’emplacement de stockage : `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Type d’exportation de données {#export-type}

Les destinations de stockage dans le cloud prennent en charge **l’exportation basée sur les profils**. Cela signifie que vous exportez des détails sur les individus de l’audience. Ces détails sont nécessaires à la personnalisation et peuvent inclure des attributs, des événements, des appartenances à des segments, etc.