---
description: Pour utiliser Destination SDK, une société partenaire doit remplir les conditions préalables répertoriées dans ce document.
title: Conditions préalables à l’intégration
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d7c9623619e989a59d72aba74903ffc0e64e7d3c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# Conditions préalables à l’intégration

Pour utiliser Destination SDK, veillez à respecter les conditions préalables techniques et de partenariat répertoriées dans les sections ci-dessous.

## Conditions préalables techniques/API pour les destinations de diffusion en continu {#streaming-prerequisites}

1. Vous disposez d’un point de terminaison d’API REST pour que Adobe Experience Platform puisse fournir les types de données suivants à :
   * Informations sur l’appartenance à un segment ;
   * Informations sur l’identité du profil ;
   * (Facultatif) Attributs supplémentaires pour l’enrichissement du profil.
2. Votre point de terminaison API REST prend en charge l’authentification du porteur de jeton API ou le protocole d’authentification OAuth 2.0.
3. (Facultatif) Vous disposez d’une API de création/mise à jour/suppression de segment ou d’un point de terminaison d’API pour la gestion programmatique des métadonnées.

## Conditions préalables techniques pour les destinations par lots {#batch-prerequisites}

1. Vous disposez d’un emplacement de destination hébergé sur [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], SFTP, [!DNL Google Cloud], ou un [!DNL Data Landing Zone], où vous pouvez recevoir les fichiers exportés hors d’Experience Platform.
2. Votre plateforme de destination peut ingérer des fichiers au format configuré via le [options de formatage de fichier](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) en Destination SDK pour les destinations par lots.
3. (Facultatif) Vous disposez d’une API CRUD (création/récupération/mise à jour/suppression) de segment ou d’un point de terminaison d’API pour la gestion programmatique des métadonnées.

## Conditions préalables du partenariat {#partnership-prerequisites}

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) qui souhaite utiliser Destination SDK, lisez les exigences de partenariat pour les ISV et les SI dans la [section accès](./overview.md#get-access).
