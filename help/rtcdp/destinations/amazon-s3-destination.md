---
title: Destination Amazon S3
seo-title: Destination Amazon S3
description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
seo-description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
translation-type: tm+mt
source-git-commit: f3c6c27b7ad07ada0df18aabe0e8503253b38342
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 82%

---


# Destination Amazon S3

## Présentation

Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.

## Connexion à la destination {#connect-destination}

Pour obtenir des instructions pour se connecter aux destinations de stockage dans le cloud, notamment Amazon S3, consultez [Processus de création des destinations de stockage dans le cloud](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

Pour les destinations Amazon S3, saisissez les informations suivantes dans le processus de création de destinations :

* **Clé d’accès Amazon S3 et clé** secrète Amazon S3 : Dans Amazon S3, générez une paire de clés d’accès secrètes pour accorder un accès CDP Adobe en temps réel à votre compte Amazon S3.



>[!IMPORTANT]
>
>La plateforme de données client en temps réel d’Adobe nécessite les autorisations `write` sur l’objet de compartiment où les fichiers d’exportation seront distribués.
