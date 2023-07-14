---
description: Pour utiliser Destination SDK, une société partenaire doit remplir les conditions préalables répertoriées dans ce document.
title: Conditions préalables à l’intégration
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---

# Conditions préalables à l’intégration

Pour utiliser Destination SDK, veillez à respecter les conditions préalables techniques et de partenariat répertoriées dans les sections ci-dessous.

## Conditions préalables techniques/API pour les destinations de diffusion en continu {#streaming-prerequisites}

1. Vous disposez d’un point de terminaison d’API REST pour que Adobe Experience Platform puisse fournir les types de données suivants à :
   * Informations sur l’appartenance à une audience ;
   * Informations sur l’identité du profil ;
   * (Facultatif) Attributs supplémentaires pour l’enrichissement du profil.
2. Votre point d’entrée API REST prend en charge les protocoles d’authentification de base, de support ou OAuth 2.0.
3. (Facultatif) Vous disposez d’une API de création, de mise à jour et de suppression d’audience ou d’un point de terminaison d’API pour la gestion programmatique des métadonnées.

## Conditions préalables techniques pour les destinations par lots {#batch-prerequisites}

1. Vous disposez d’un emplacement de destination hébergé sur [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud], ou un [!DNL Data Landing Zone], où vous pouvez recevoir les fichiers exportés hors d’Experience Platform.
2. Votre plateforme de destination peut ingérer des fichiers au format configuré via le [options de formatage de fichier](functionality/destination-server/file-formatting.md) en Destination SDK pour les destinations par lots.
3. (Facultatif) Vous avez une audience à créer/récupérer/mettre à jour/supprimer ([!DNL CRUD]) API ou point d’entrée API pour la gestion programmatique des métadonnées.

## Conditions préalables du partenariat {#partnership-prerequisites}

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) qui souhaite utiliser Destination SDK, lisez les exigences de partenariat pour les ISV et les SI dans la [section accès](overview.md#get-access).
