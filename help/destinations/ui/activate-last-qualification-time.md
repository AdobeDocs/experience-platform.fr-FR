---
title: Utilisation de l’attribut XDM de l’heure de dernière qualification dans les nouvelles destinations de stockage dans le cloud bêta
description: Découvrez comment utiliser l’attribut XDM de l’heure de la dernière qualification dans les nouvelles destinations de stockage dans le cloud bêta
badgeBeta: label="Version bêta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 7130ac46a7768ea6e71bf73eb970bf2890323d0f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 10%

---

# Utilisation de l’attribut XDM de l’heure de dernière qualification dans les nouvelles destinations de stockage dans le cloud bêta {#last-qualification-time}

>[!IMPORTANT]
> 
>Cette page décrit les fonctionnalités en version bêta. Les fonctionnalités et la documentation sont susceptibles d’être modifiées. Contactez votre représentant Adobe ou l’assistance clientèle si vous souhaitez accéder à ce programme bêta.

## Conditions préalables {#prerequisites}

Pour utiliser l’attribut XDM de l’heure de dernière qualification (`lastQualificationTime`), vous devez exporter des données vers l’une des six destinations de stockage dans le cloud répertoriées ci-dessous :

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Utilisation de l’attribut XDM de l’heure de la dernière qualification {#how-to-use}

Si vous utilisez l’un des six connecteurs de stockage dans le cloud répertoriés ci-dessus, vous pouvez utiliser l’attribut XDM de l’heure de dernière qualification dans l’ [étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) du workflow d’activation pour créer une colonne dans le fichier exporté avec l’horodatage le plus récent du moment où un profil est qualifié pour un segment. Cela peut vous aider pour certains cas d’utilisation des mesures ou analyses et vous donner une meilleure idée du moment où activer certaines audiences.

Notez que pour ajouter `lastQualificationTime` à vos exportations de fichiers, vous devez actuellement insérer manuellement la valeur `xdm: segmentMembership.ups.seg_id.lastQualificationTime` dans le champ source, comme illustré ci-dessous. Vous pouvez également modifier le champ cible en `lastQualificationTime` ou toute autre valeur que vous souhaitez nommer cette colonne. Comme il s’agit d’une fonctionnalité bêta, la syntaxe de la valeur `xdm: segmentMembership.ups.seg_id.lastQualificationTime` risque de changer à l’avenir.

![Enregistrement de l’écran montrant le collage de l’attribut XDM de l’heure de la dernière qualification dans l’étape de mappage](/help/destinations/ui/last-qualification-time.gif)

## Informations supplémentaires {#more-information}

Pour plus d’informations sur l’activation des données vers des destinations basées sur des fichiers, y compris toutes les étapes du workflow et les autorisations nécessaires, consultez le [tutoriel d’activation des destinations basées sur des fichiers](/help/destinations/ui/activate-batch-profile-destinations.md).
