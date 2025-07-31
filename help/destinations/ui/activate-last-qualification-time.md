---
title: Utilisez l’attribut XDM de la dernière qualification dans les nouvelles destinations bêta de stockage dans le cloud
description: Découvrez comment utiliser l’attribut XDM de la dernière qualification dans les nouvelles destinations bêta de stockage dans le cloud
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 10%

---

# Utilisez l’attribut XDM de la dernière qualification dans les nouvelles destinations bêta de stockage dans le cloud {#last-qualification-time}

>[!IMPORTANT]
> 
>Cette page décrit les fonctionnalités de la version bêta. Les fonctionnalités et la documentation sont susceptibles d’être modifiées. Contactez votre représentant Adobe ou l’assistance clientèle si vous souhaitez accéder à ce programme bêta.

## Conditions préalables {#prerequisites}

Pour utiliser l’attribut XDM Heure de la dernière qualification (`lastQualificationTime`), vous devez exporter des données vers l’une des six destinations d’espace de stockage répertoriées ci-dessous :

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zone]](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Comment utiliser l’attribut XDM de l’heure de la dernière qualification {#how-to-use}

Si vous utilisez l’un des six connecteurs d’espace de stockage répertoriés ci-dessus, vous pouvez utiliser l’attribut XDM Heure de la dernière qualification à l’étape [mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) du workflow d’activation pour créer une colonne dans le fichier exporté avec la date et l’heure les plus récentes auxquelles un profil s’est qualifié pour un segment. Cela peut vous aider dans certains cas d’utilisation de mesures ou d’analyses et vous donner une meilleure idée du moment où activer certaines audiences.

Notez que pour ajouter des `lastQualificationTime` à vos exportations de fichiers, vous devez actuellement insérer manuellement la valeur `xdm: segmentMembership.ups.seg_id.lastQualificationTime` dans le champ source, comme illustré ci-dessous. Vous pouvez également modifier le champ cible en `lastQualificationTime` ou toute autre valeur que vous souhaitez attribuer à cette colonne. Notez que puisqu’il s’agit d’une fonctionnalité bêta, la syntaxe de la valeur `xdm: segmentMembership.ups.seg_id.lastQualificationTime` peut changer à l’avenir.

![Enregistrement de l’écran affichant l’attribut XDM de la dernière qualification collé dans l’étape de mappage](/help/destinations/ui/last-qualification-time.gif)

## Informations supplémentaires {#more-information}

Pour obtenir des informations détaillées sur l’activation des données vers les destinations basées sur des fichiers, y compris toutes les étapes du workflow et les autorisations nécessaires, consultez le tutoriel [activation des destinations basées sur des fichiers](/help/destinations/ui/activate-batch-profile-destinations.md).
