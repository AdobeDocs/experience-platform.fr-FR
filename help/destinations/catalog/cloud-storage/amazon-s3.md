---
keywords: Amazon S3;destination S3;s3;amazon s3
title: Connexion à Amazon S3
description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 9%

---

# [!DNL Amazon S3] connection {#s3-connection}

## Présentation {#overview}

Créez une connexion sortante active à votre stockage [!DNL Amazon Web Services] (AWS) S3 pour exporter périodiquement des fichiers de données CSV ou séparés par des tabulations de Adobe Experience Platform vers vos propres compartiments S3.

## Type d&#39;export {#export-type}

**Basé sur un profil**  : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse email, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs du workflow d’activation de  [destination](../../ui/activate-segment-streaming-destinations.md#mapping).

![Type d’exportation basé sur les profils Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!DNL Amazon S3]clé** d’accès et clé  **[!DNL Amazon S3]secrète** : Dans  [!DNL Amazon S3], générez une  `access key - secret access key` paire pour accorder l’accès à Platform à votre  [!DNL Amazon S3] compte. Pour en savoir plus, consultez la [documentation des services Web Amazon](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Nom]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]** : saisissez une description de cette destination.
* **[!UICONTROL Nom du compartiment]** : saisissez le nom du  [!DNL Amazon S3] compartiment à utiliser par cette destination.
* **[!UICONTROL Chemin du dossier]** : saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que chaîne codée [!DNL Base64].

>[!TIP]
>
>Dans le workflow de connexion à la destination, vous pouvez créer un dossier personnalisé dans le stockage Amazon S3 par fichier de segment exporté. Lisez [Utilisez les macros pour créer un dossier à l’emplacement de stockage](overview.md#use-macros) pour obtenir des instructions.

### Autorisations [!DNL Amazon S3] requises {#required-s3-permission}

Pour connecter et exporter des données vers votre emplacement de stockage [!DNL Amazon S3], créez un utilisateur de gestion des identités et des accès (IAM) pour [!DNL Platform] dans [!DNL Amazon S3] et attribuez des autorisations pour les actions suivantes :

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de profil de lot](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Pour les destinations [!DNL Amazon S3], [!DNL Platform] crée un fichier `.csv` délimité par des tabulations dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activation des données d’audience vers les destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation des segments.
