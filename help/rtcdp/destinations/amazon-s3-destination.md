---
title: Destination Amazon S3
seo-title: Destination Amazon S3
description: Créez une connexion sortante en direct vers votre AWS (AWS) S3  Amazon Web Services (AWS) pour exporter régulièrement des fichiers de données CSV ou délimités par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
seo-description: Créez une connexion sortante en direct vers votre AWS (AWS) S3  Amazon Web Services (AWS) pour exporter régulièrement des fichiers de données CSV ou délimités par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
translation-type: tm+mt
source-git-commit: f3c6c27b7ad07ada0df18aabe0e8503253b38342

---


# Destination Amazon S3

## Présentation

Créez une connexion sortante en direct vers votre AWS (AWS) S3  Amazon Web Services (AWS) pour exporter régulièrement des fichiers de données CSV ou délimités par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.

## Se connecter à la destination {#connect-destination}

Reportez-vous à [Cloud  flux de travaux  destinations de ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)pour savoir comment vous connecter à vos destinations de de cloud, y compris Amazon S3.

Pour les destinations Amazon S3, saisissez les informations suivantes dans le processus de création de destination :

* **Clé d’accès Amazon S3 et clé** secrète Amazon S3 : Dans Amazon S3, générez une clé d’accès - paire de clés d’accès secrètes pour accorder l’accès CDP Adobe en temps réel à votre compte Amazon S3.



>[!IMPORTANT]
>
>Le CDP en temps réel d’Adobe nécessite `write` des autorisations sur l’objet de compartiment où les fichiers d’exportation seront distribués.
