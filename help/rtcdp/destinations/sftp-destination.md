---
title: Destination SFTP
seo-title: Destination SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.
seo-description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 77%

---


# Destination SFTP

## Présentation

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.

Pour exporter des données, procédez comme suit :

## Connexion à la destination {#connect-destination}

Pour obtenir des instructions pour se connecter aux destinations de stockage dans le cloud, notamment SFTP, consultez [Processus des destinations de stockage dans le cloud](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

Pour les destinations SFTP, saisissez les informations suivantes à l’étape **Authentification** du processus de création de destination :

* **Hôte** : adresse de l’emplacement de stockage de votre SFTP
* **Nom d’utilisateur** : nom d’utilisateur pour se connecter à l’emplacement de stockage de votre SFTP
* **Mot de passe** : mot de passe pour se connecter à l’emplacement de stockage de votre SFTP

## Données exportées {#exported-data}

For [!SFTP] destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Pour plus d’informations sur les fichiers, reportez-vous à la section Destinations du marketing par [courrier électronique et Destinations](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) d’enregistrement Cloud dans le didacticiel sur l’activation des segments.