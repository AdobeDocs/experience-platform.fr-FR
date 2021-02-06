---
keywords: SFTP;sftp
title: Destination de la connexion SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 38%

---


# Connexion SFTP

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Experience Platform.

## Type d&#39;exportation {#export-type}

**Basé sur**  le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [ d’activation de ](../../ui/activate-destinations.md#select-attributes)destination.

![Type d’exportation par profil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Connexion à la destination {#connect-destination}

Pour obtenir des instructions pour se connecter aux destinations de stockage dans le cloud, notamment SFTP, consultez [Processus des destinations de stockage dans le cloud](./workflow.md).

Pour les destinations SFTP, saisissez les informations suivantes à l’étape **Authentification** du processus de création de destination :

* **Hôte** : Adresse de l’emplacement de votre enregistrement SFTP
* **Nom d&#39;utilisateur** : Nom d’utilisateur pour la connexion à votre emplacement d’enregistrement SFTP.
* **Mot de passe** : Mot de passe de connexion à l’emplacement de votre enregistrement SFTP

## Données exportées {#exported-data}

Pour les destinations SFTP, Platform crée un fichier délimité par des tabulations `.txt` ou `.csv` à l’emplacement de l’enregistrement que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Destinations du marketing par courriel et Destinations de l’enregistrement Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) dans le didacticiel sur l’activation des segments.