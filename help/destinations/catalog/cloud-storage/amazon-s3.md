---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Connexion Amazon S3
description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
translation-type: tm+mt
source-git-commit: d77cd063e61118631b757d9821267b2fd6ab0148
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 14%

---

# [!DNL Amazon S3] connexion  {#s3-connection}

## Présentation {#overview}

Créez une connexion sortante en direct à votre enregistrement S3 [!DNL Amazon Web Services] (AWS) pour exporter périodiquement des fichiers de données CSV ou délimités par des tabulations depuis Adobe Experience Platform dans vos propres compartiments S3.

## Type d&#39;exportation {#export-type}

**Basé sur**  le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [ d’activation de ](../../ui/activate-destinations.md#select-attributes)destination.

![Type d’exportation basée sur le profil Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Connexion à la destination {#connect-destination}

Voir [Flux de travaux de destination des enregistrements cloud ](./workflow.md) pour savoir comment se connecter à vos destinations d’enregistrement cloud, y compris [!DNL Amazon S3].

Pour les destinations [!DNL Amazon S3], saisissez les informations suivantes dans le processus de création de destination :

* **[!DNL Amazon S3]clé d&#39;accès et clé [!DNL Amazon S3]** secrète : Dans  [!DNL Amazon S3], générez une  `access key - secret access key` paire pour accorder l’accès à la plate-forme à votre  [!DNL Amazon S3] compte. Pour en savoir plus, consultez la [documentation Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

## Autorisations [!DNL Amazon S3] requises {#required-s3-permission}

Pour connecter et exporter des données vers votre emplacement d&#39;enregistrement [!DNL Amazon S3], créez un utilisateur IAM pour [!DNL Platform] dans [!DNL Amazon S3] et attribuez des autorisations pour les actions suivantes :

* `s3:DeleteObject`
* `s3:DeleteObjectVersion`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:GetObjectVersion`
* `s3:ListBucket`
* `s3:ListBuckets`
* `s3:PutBucketVersioning`
* `s3:PutObject`
* `s3:ReplicateObject`
* `s3:RestoreObject`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## Données exportées {#exported-data}

Pour les destinations [!DNL Amazon S3], [!DNL Platform] crée un fichier délimité par des tabulations `.txt` ou `.csv` à l&#39;emplacement d&#39;enregistrement que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Destinations du marketing par courriel et Destinations de l’enregistrement Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) dans le didacticiel sur l’activation des segments.
