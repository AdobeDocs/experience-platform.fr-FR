---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Destination Amazon S3
seo-title: Destination Amazon S3
description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
seo-description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
translation-type: tm+mt
source-git-commit: 67a353c950bef11ccbaa52c49d213f08449baa96
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 33%

---


# [!DNL Amazon S3] destination

## Présentation

Create a live outbound connection to your [!DNL Amazon Web Services] (AWS) S3 storage to periodically export tab-delimited or CSV data files from Adobe Experience Platform into your own S3 buckets.

## Type d’exportation {#export-type}

**Basé sur** le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [d’activation de](/help/rtcdp/destinations/activate-destinations.md#select-attributes)destination.

![Type d’exportation basée sur le profil Amazon S3](/help/rtcdp/destinations/assets/aws-export-type.png)

## Connexion à la destination {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including [!DNL Amazon S3].

For [!DNL Amazon S3] destinations, enter the following information in the create destination workflow:

* **[!DNL Amazon S3]clé d&#39;accès et clé[!DNL Amazon S3]** secrète : Dans [!DNL Amazon S3], générez une `access key - secret access key` paire pour accorder un accès CDP en temps réel Adobe à votre [!DNL Amazon S3] compte. Pour en savoir plus, consultez la documentation [sur les services Web](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon.

>[!IMPORTANT]
>
>La plateforme de données clients en temps réel d’Adobe nécessite les autorisations `write` sur l’objet de compartiment où les fichiers d’exportation seront distribués.

## Données exportées {#exported-data}

For [!DNL Amazon S3] destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Pour plus d’informations sur les fichiers, reportez-vous à la section Destinations du marketing par [courrier électronique et Destinations](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) d’enregistrement Cloud dans le didacticiel sur l’activation des segments.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
