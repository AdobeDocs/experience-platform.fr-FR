---
keywords: destination de stockage dans le cloud;espace de stockage dans le cloud
title: Présentation des destinations de stockage dans le cloud
description: Adobe Experience Platform peut fournir vos audiences sous forme de fichiers de données à vos emplacements de stockage dans le cloud Amazon S3, AWS Kinesis, Azure Event Hubs ou SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 2e21e62de624c5e7e9fac4d36dbf41b46198062a
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 38%

---

# Présentation des destinations de stockage dans le cloud {#cloud-storage-destinations}

## Présentation {#overview}

Adobe Experience Platform peut fournir vos audiences sous forme de fichiers de données aux emplacements de stockage dans le cloud. Vous pouvez ainsi envoyer des audiences et leurs attributs de profils à vos systèmes internes au moyen de fichiers CSV pour [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage], et SFTP. Pour les destinations [!DNL Amazon Kinesis] et [!DNL Azure Event Hubs], les données sont diffusées en continu hors Experience Platform au format [!DNL JSON].

![Destinations de stockage dans le cloud Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinations de stockage dans le cloud prises en charge {#supported-destinations}

Adobe Experience Platform prend en charge les exportations de données vers les destinations de stockage dans le cloud suivantes :

* [Connexion Amazon Kinesis](amazon-kinesis.md)
* [Connexion Amazon S3](amazon-s3.md)
* [Connexion Azure Blob](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Connexion Azure Event Hubs](azure-event-hubs.md)
* [Zone d’atterrissage des données](data-landing-zone.md)
* [Google Cloud Storage](google-cloud-storage.md)
* [Connexion SFTP](sftp.md)

## Se connecter à une nouvelle destination de stockage dans le cloud {#connect-destination}

Pour envoyer des audiences vers des destinations de stockage dans le cloud pour vos campagnes, Platform doit d’abord se connecter à la destination. Voir le [tutoriel sur la création de destinations](../../ui/connect-destination.md) pour des informations détaillées sur la configuration d’une nouvelle destination.


## Utiliser les macros pour créer un dossier à votre emplacement de stockage {#use-macros}

>[!NOTE]
>
> Les fonctionnalités décrites dans cette section sont disponibles pour toutes les destinations de stockage dans le cloud. Cependant, la destination [Amazon S3](amazon-s3.md) ne prend actuellement en charge que les macros `%SEGMENT_ID%` et `%SEGMENT_NAME%`.

Pour créer un dossier personnalisé par fichier d’audience à l’emplacement de stockage, vous pouvez utiliser des macros dans le champ d’entrée Chemin du dossier. Insérez les macros à la fin du champ de saisie, comme illustré ci-dessous.

![Utiliser des macros pour créer un dossier dans votre espace de stockage](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Les exemples ci-dessous font référence à un exemple d’audience `Luxury Audience` avec l’ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1 :`%SEGMENT_NAME%`**

Entrée : `acme/campaigns/2021/%SEGMENT_NAME%`
Chemin du dossier dans votre emplacement de stockage : `acme/campaigns/2021/Luxury Audience`

**Macro 2 :`%SEGMENT_ID%`**

Entrée : `acme/campaigns/2021/%SEGMENT_ID%`
Chemin du dossier dans votre emplacement de stockage : `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3 :`%SEGMENT_NAME%/%SEGMENT_ID%`**

Entrée : `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Chemin du dossier dans votre emplacement de stockage : `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**Autres macros**

Comme dans les exemples ci-dessus, vous pouvez utiliser d’autres macros pour créer une structure de dossiers personnalisée dans l’emplacement de votre dossier :

* `%DATETIME%` ou `%TIMESTAMP%` pour ajouter un nom de dossier personnalisé en fonction de l’heure d’exportation des fichiers. Le format de la première macro est `MMDDYYYY_HHMMSS` et le format UNIX 10 chiffres de la seconde macro.
* `%DESTINATION_NAME%` pour ajouter un dossier personnalisé en fonction du nom du flux de données de destination.

## Type d’exportation de données {#export-type}

Les destinations de stockage dans le cloud prennent en charge les types d’exportation suivants :
* **Exportation basée sur un profil**. Cela signifie que vous exportez des détails sur les individus dans l’audience. Ces détails sont nécessaires à la personnalisation et peuvent inclure des attributs, des événements, des appartenances à l’audience, etc.
* **Exportation du jeu de données**. Cette fonctionnalité vous permet d’exporter des jeux de données entiers vers des destinations de stockage dans le cloud. [En savoir plus](/help/destinations/ui/export-datasets.md) sur la fonctionnalité.

## Étapes suivantes {#next-steps}

Après avoir sélectionné l’une des [ destinations de cloud prises en charge](#supported-destinations) que vous souhaitez utiliser, lisez le [tutoriel de connexion aux destinations](/help/destinations/ui/connect-destination.md) pour apprendre à établir une connexion à la destination. Lisez ensuite le tutoriel sur l’activation des destinations basées sur des fichiers pour savoir comment commencer à [exporter](/help/destinations/ui/activate-batch-profile-destinations.md) des données vers votre destination de stockage dans le cloud.
