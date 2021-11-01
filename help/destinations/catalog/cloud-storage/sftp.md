---
keywords: SFTP;sftp
title: Connexion SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Connexion SFTP

## Présentation {#overview}

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités de Adobe Experience Platform.

>[!IMPORTANT]
>
> Bien qu’Adobe prenne en charge les exportations de données vers les serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter des données sont les suivants : [!DNL Amazon S3] et [!DNL Azure Blob].

## Type d’exportation {#export-type}

**Basé sur les profils** - vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), selon le choix effectué dans l’écran de sélection des attributs de la variable [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md).

![Type d’exportation SFTP basé sur un profil](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **Hôte**: Adresse de l’emplacement de stockage de votre SFTP
* **Nom d’utilisateur**: Nom d’utilisateur pour se connecter à l’emplacement de stockage SFTP
* **Mot de passe**: Mot de passe pour se connecter à l’emplacement de stockage SFTP
* **[!UICONTROL Nom]**: saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]**: saisissez une description de cette destination.
* **[!UICONTROL Chemin du dossier]**: saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.

## Données exportées {#exported-data}

Pour [!DNL SFTP] destinations, Platform crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation des segments.

## LISTE AUTORISÉE d’adresses IP

Voir [LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud](ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à une liste autorisée.
