---
keywords: destination de stockage dans le cloud;espace de stockage dans le cloud
title: Présentation des destinations de stockage dans le cloud
description: Adobe Experience Platform peut diffuser vos segments sous forme de fichiers de données vers vos emplacements de stockage dans le cloud Amazon S3, AWS Kinesis, Azure Event Hubs ou SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 4a4c82cc4528fe07bbdb75ae9f795bdbab48c089
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 11%

---

# Présentation des destinations de stockage dans le cloud {#cloud-storage-destinations}

## Présentation {#overview}

Adobe Experience Platform peut fournir vos segments sous forme de fichiers de données aux emplacements de stockage dans le cloud. Vous pouvez ainsi envoyer des audiences et leurs attributs de profil à vos systèmes internes au moyen de fichiers CSV pour [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage]et SFTP. Pour [!DNL Amazon Kinesis] et [!DNL Azure Event Hubs] destinations, les données sont diffusées en continu hors de l’Experience Platform dans [!DNL JSON] format.

![Destinations de stockage dans le cloud Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinations de stockage dans le cloud prises en charge {#supported-destinations}

Adobe Experience Platform prend en charge les destinations de stockage dans le cloud suivantes :

* [Connexion à Amazon Kinesis](amazon-kinesis.md)
* [Connexion Amazon S3](amazon-s3.md)
* [Connexion Azure Blob](azure-blob.md)
* [(Version bêta) Azure Data Lake Storage Gen2](adls-gen2.md)
* [Connexion à Azure Event Hubs](azure-event-hubs.md)
* [(Version bêta) Zone d’entrée des données](data-landing-zone.md)
* [(Version bêta) Stockage dans le cloud Google](google-cloud-storage.md)
* [Connexion SFTP](sftp.md)

## Connexion à une nouvelle destination de stockage dans le cloud {#connect-destination}

Pour envoyer des segments aux destinations de stockage dans le cloud pour vos campagnes, Platform doit d’abord se connecter à la destination. Voir le [tutoriel sur la création de destinations](../../ui/connect-destination.md) pour des informations détaillées sur la configuration d’une nouvelle destination.


## Utilisez les macros pour créer un dossier à l’emplacement de stockage {#use-macros}

>[!NOTE]
>
> Les fonctionnalités décrites dans cette section sont actuellement disponibles pour les [Amazon S3](amazon-s3.md) destinations uniquement.

Pour créer un dossier personnalisé par fichier de segment à l’emplacement de stockage, vous pouvez utiliser des macros dans le champ d’entrée Chemin du dossier. Insérez les macros à la fin du champ de saisie, comme illustré ci-dessous.

![Utilisation des macros pour créer un dossier dans votre stockage](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Les exemples ci-dessous référencent un exemple de segment. `Luxury Audience` avec ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

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

Prise en charge des destinations de stockage dans le cloud **Exportation basée sur les profils**. Cela signifie que vous exportez des détails sur les individus de l’audience. Ces détails sont nécessaires à la personnalisation et peuvent inclure des attributs, des événements, des appartenances à des segments, etc.