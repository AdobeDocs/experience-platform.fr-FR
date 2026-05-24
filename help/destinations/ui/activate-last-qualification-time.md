---
title: Utilisez l’attribut XDM de la dernière qualification dans les nouvelles destinations bêta de stockage dans le cloud
description: Découvrez comment utiliser l’attribut XDM de la dernière qualification dans les nouvelles destinations bêta de stockage dans le cloud
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
TQID: https://experienceleague.adobe.com/owwch5kzbI5Md9T0lgj4GAtgTq9LO6ncHTmSjyuQNkI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 287
ht-degree: 10%

---

# Utilisez l’attribut XDM de la dernière qualification dans les nouvelles destinations bêta de stockage dans le cloud {#last-qualification-time}

>[!IMPORTANT]
>
>Cette page décrit les fonctionnalités de la version bêta. Les fonctionnalités et la documentation sont susceptibles d’être modifiées. Contactez votre représentant ou représentante Adobe ou l’assistance clientèle si vous souhaitez accéder à ce programme Beta.

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

>[!NOTE]
>
>Pour ajouter des `lastQualificationTime` à vos exportations de fichiers, vous devez actuellement insérer manuellement la valeur `xdm: segmentMembership.ups.seg_id.lastQualificationTime` dans le champ source, comme illustré ci-dessous. Vous pouvez également modifier le champ cible en `lastQualificationTime` ou toute autre valeur que vous souhaitez attribuer à cette colonne. Puisqu’il s’agit d’une fonctionnalité en version Beta, la syntaxe de la valeur `xdm: segmentMembership.ups.seg_id.lastQualificationTime` peut changer à l’avenir.

![Enregistrement de l’écran affichant l’attribut XDM de la dernière qualification collé dans l’étape de mappage](/help/destinations/ui/last-qualification-time.gif)

## Informations supplémentaires {#more-information}

Pour obtenir des informations détaillées sur l’activation des données vers les destinations basées sur des fichiers, y compris toutes les étapes du workflow et les autorisations nécessaires, consultez le tutoriel [activation des destinations basées sur des fichiers](/help/destinations/ui/activate-batch-profile-destinations.md).
