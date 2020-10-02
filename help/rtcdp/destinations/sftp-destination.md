---
keywords: SFTP;sftp
title: Destination SFTP
seo-title: Destination SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.
seo-description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 60%

---


# Destination SFTP

## Présentation

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.

## Type d’exportation {#export-type}

**Exportation** de profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [d’activation de](/help/rtcdp/destinations/activate-destinations.md#select-attributes)destination.

![Type d’exportation par profil SFTP](/help/rtcdp/destinations/assets/sftp-export-type.png)

## Connexion à la destination {#connect-destination}

Pour obtenir des instructions pour se connecter aux destinations de stockage dans le cloud, notamment SFTP, consultez [Processus des destinations de stockage dans le cloud](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

Pour les destinations SFTP, saisissez les informations suivantes à l’étape **Authentification** du processus de création de destination :

* **Hôte** : adresse de l’emplacement de stockage de votre SFTP
* **Nom d’utilisateur** : nom d’utilisateur pour se connecter à l’emplacement de stockage de votre SFTP
* **Mot de passe** : mot de passe pour se connecter à l’emplacement de stockage de votre SFTP

## Données exportées {#exported-data}

For SFTP destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Pour plus d’informations sur les fichiers, reportez-vous à la section Destinations du marketing par [courrier électronique et Destinations](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) d’enregistrement Cloud dans le didacticiel sur l’activation des segments.