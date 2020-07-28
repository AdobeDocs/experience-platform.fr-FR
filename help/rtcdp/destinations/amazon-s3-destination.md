---
title: Destination Amazon S3
seo-title: Destination Amazon S3
description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
seo-description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV ou séparés par des tabulations depuis Adobe Experience Platform vers vos propres compartiments S3.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 51%

---


# [!DNL Amazon S3] destination

## Présentation

Create a live outbound connection to your [!DNL Amazon Web Services] (AWS) S3 storage to periodically export tab-delimited or CSV data files from Adobe Experience Platform into your own S3 buckets.

## Connexion à la destination {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including [!DNL Amazon S3].

For [!DNL Amazon S3] destinations, enter the following information in the create destination workflow:

* **[!DNL Amazon S3]clé d&#39;accès et clé[!DNL Amazon S3]**secrète : Dans[!DNL Amazon S3], générez une paire de clés d&#39;accès secrète pour accorder un accès CDP en temps réel à votre[!DNL Amazon S3]compte.



>[!IMPORTANT]
>
>La plateforme de données clients en temps réel d’Adobe nécessite les autorisations `write` sur l’objet de compartiment où les fichiers d’exportation seront distribués.
