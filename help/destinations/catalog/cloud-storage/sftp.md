---
keywords: SFTP;sftp
title: Destination SFTP
seo-title: Destination SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.
seo-description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 47%

---


# Destination SFTP

## Présentation

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.

## Type d’exportation {#export-type}

**Basé sur** le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [d’activation de](../../ui/activate-destinations.md#select-attributes)destination.

![Type d’exportation par profil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Connexion à la destination {#connect-destination}

Pour obtenir des instructions pour se connecter aux destinations de stockage dans le cloud, notamment SFTP, consultez [Processus des destinations de stockage dans le cloud](./workflow.md).

Pour les destinations SFTP, saisissez les informations suivantes à l’étape **Authentification** du processus de création de destination :

* **Hôte**: Adresse de l’emplacement de votre enregistrement SFTP
* **Nom d&#39;utilisateur**: Nom d’utilisateur pour la connexion à votre emplacement d’enregistrement SFTP.
* **Mot de passe**: Mot de passe de connexion à l’emplacement de votre enregistrement SFTP

## Données exportées {#exported-data}

For SFTP destinations, Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Pour plus d’informations sur les fichiers, reportez-vous à la section Destinations du marketing par [courrier électronique et Destinations](../../ui/activate-destinations.md#esp-and-cloud-storage) d’enregistrement Cloud dans le didacticiel sur l’activation des segments.