---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Connexion Amazon S3
description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '223'
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

>[!IMPORTANT]
>
>La plate-forme a besoin d&#39;autorisations `write` sur l&#39;objet de compartiment où les fichiers d&#39;exportation seront distribués.

## Données exportées {#exported-data}

Pour les destinations [!DNL Amazon S3], Platform crée un fichier délimité par des tabulations `.txt` ou `.csv` à l&#39;emplacement de l&#39;enregistrement que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Destinations du marketing par courriel et Destinations de l’enregistrement Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) dans le didacticiel sur l’activation des segments.
