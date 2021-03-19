---
keywords: SFTP;sftp
title: Connexion SFTP
description: Créez une connexion sortante en direct vers votre serveur SFTP pour exporter périodiquement des fichiers de données délimités à partir de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4f0047e7ac4c83e3e17ea0a077bbeb09c86d1db6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 7%

---


# Connexion SFTP

Créez une connexion sortante en direct vers votre serveur SFTP pour exporter périodiquement des fichiers de données délimités à partir de Adobe Experience Platform.

>[!IMPORTANT]
>
> Bien que l’Adobe prenne en charge les exportations de données vers les serveurs SFTP, les emplacements d’enregistrement de cloud recommandés pour exporter les données sont [!DNL Amazon S3] et [!DNL Azure Blob].

## Type d&#39;exportation {#export-type}

**Basé sur**  le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [ d’activation de ](../../ui/activate-destinations.md#select-attributes)destination.

![Type d’exportation par profil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Connexion à la destination {#connect-destination}

Pour obtenir des instructions sur la connexion à vos destinations d’enregistrement de cloud, y compris SFTP, consultez le [flux de travaux de destination des enregistrements de cloud ](./workflow.md).

Pour les destinations SFTP, saisissez les informations suivantes à l’étape **Authentification** du processus de création de destination :

* **Hôte** : Adresse de l’emplacement de votre enregistrement SFTP
* **Nom d&#39;utilisateur** : Nom d’utilisateur pour la connexion à votre emplacement d’enregistrement SFTP.
* **Mot de passe** : Mot de passe de connexion à l’emplacement de votre enregistrement SFTP

## Données exportées {#exported-data}

Pour les destinations SFTP, Platform crée un fichier délimité par des tabulations `.txt` ou `.csv` à l’emplacement de l’enregistrement que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Destinations du marketing par courriel et Destinations de l’enregistrement Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) dans le didacticiel sur l’activation des segments.

## LISTE AUTORISÉE d&#39;adresse IP

Reportez-vous à la [liste autorisée d&#39;adresse IP pour les destinations d&#39;enregistrement cloud](./ip-address-allow-list.md) si vous devez ajouter des adresses IP d&#39;Adobe à une liste autorisée.