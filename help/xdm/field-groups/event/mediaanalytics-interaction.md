---
title: Groupe de champs de schéma Détails de l’interaction MediaAnalytics
description: Découvrez le groupe de champs Détails de l’interaction MediaAnalytics .
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 5%

---

# [!UICONTROL Détails de l’interaction MediaAnalytics] groupe de champs de schéma

[!UICONTROL Détails de l’interaction MediaAnalytics] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Utilisez ce groupe de champs pour capturer des champs de données enrichis qui surveillent et analysent de manière exhaustive les interactions avec le contenu multimédia sur différentes plateformes ou différents canaux.

![Schéma du [!UICONTROL Détails de l’interaction MediaAnalytics] groupe de champs de schéma.](../../images/field-groups/mediaanalytics-interaction.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---| --- | --- | --- |
| [!UICONTROL Détails de la collection multimédia] | `mediaCollection` | [[!UICONTROL Informations détaillées sur le média]](../../data-types/media-details-information.md) | Attributs liés à une collection d’éléments multimédias. |
| [!UICONTROL Détails sur les rapports multimédia] | `mediaReporting` | [[!UICONTROL Informations détaillées sur le média]](../../data-types/media-details-information.md) | Détails des rapports et mesures associées au contenu multimédia. |
| [!UICONTROL Liste des événements de contenu téléchargé Media Collection] | `mediaDownloadedEvents` | [!UICONTROL Tableau] de [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Événements qui effectuent le suivi du téléchargement du contenu dans la collection de médias. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
