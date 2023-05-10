---
title: Utilisation de l’attribut XDM de l’heure de dernière qualification dans les nouvelles destinations de stockage dans le cloud bêta
description: Découvrez comment utiliser l’attribut XDM de l’heure de la dernière qualification dans les nouvelles destinations de stockage dans le cloud bêta
hidefromtoc: y
hide: y
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 8%

---

# Utilisation de l’attribut XDM de l’heure de dernière qualification dans les nouvelles destinations de stockage dans le cloud bêta {#last-qualification-time}

>[!IMPORTANT]
> 
>Cette page décrit les fonctionnalités en version bêta. Les fonctionnalités et la documentation sont susceptibles d’être modifiées. Contactez votre représentant Adobe ou l’assistance clientèle si vous souhaitez accéder à ce programme bêta.

## Conditions préalables {#prerequisites}

Pour utiliser l’heure de la dernière qualification (`lastQualificationTime`) de l’attribut XDM, vous devez être inscrit dans la variable [programme bêta](/help/release-notes/2022/october-2022.md#destinations) pour utiliser la fonctionnalité améliorée d’exportation de fichiers et exporter des données vers l’un des six [destinations de stockage dans le cloud bêta](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)). Vous êtes inscrit si vous pouvez voir les nouvelles cartes bêta pour les destinations de stockage dans le cloud dans le catalogue, comme illustré ci-dessous pour [!DNL Amazon S3].

![Image montrant la nouvelle carte bêta d’Amazon S3](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## Utilisation de l’attribut XDM de l’heure de la dernière qualification {#how-to-use}

Si vous utilisez l’un des six nouveaux connecteurs bêta de stockage dans le cloud, vous pouvez utiliser l’attribut XDM de l’heure de dernière qualification dans la variable [étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) du workflow d’activation afin de créer une colonne dans le fichier exporté avec l’horodatage le plus récent du moment où un profil est qualifié pour un segment. Cela peut vous aider pour certains cas d’utilisation des mesures ou analyses et vous donner une meilleure idée du moment où activer certaines audiences.

Notez que pour ajouter `lastQualificationTime` à vos exportations de fichiers, vous devez actuellement insérer manuellement la valeur `xdm: segmentMembership.ups.seg_id.lastQualificationTime` dans le champ source, comme illustré ci-dessous. Vous pouvez également modifier le champ cible en `lastQualificationTime` ou toute autre valeur que vous souhaitez attribuer au nom de cette colonne. Comme il s’agit d’une fonctionnalité bêta, la syntaxe de la variable `xdm: segmentMembership.ups.seg_id.lastQualificationTime` peut changer à l’avenir.

![Enregistrement de l’écran affichant l’heure de dernière qualification que l’attribut XDM colle dans l’étape de mappage](/help/destinations/ui/last-qualification-time.gif)

## Informations supplémentaires {#more-information}

Pour obtenir des informations détaillées sur l’activation des données vers des destinations basées sur des fichiers, notamment toutes les étapes du workflow et les autorisations nécessaires, consultez la section [tutoriel sur l’activation des destinations basées sur des fichiers](/help/destinations/ui/activate-batch-profile-destinations.md).
