---
title: Groupe de champs de schéma Détails de l’interaction MediaAnalytics
description: Découvrez le groupe de champs de schéma Détails de l’interaction MediaAnalytics.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 2%

---

# Groupe de champs de schéma [!UICONTROL Détails de l’interaction MediaAnalytics]

[!UICONTROL Détails de l’interaction MediaAnalytics] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Utilisez ce groupe de champs pour capturer des champs de données enrichis qui surveillent et analysent de manière exhaustive les interactions avec le contenu multimédia sur différentes plateformes ou canaux.

![Schéma du groupe de champs de schéma [!UICONTROL Détails de l’interaction MediaAnalytics].](../../images/field-groups/mediaanalytics-interaction.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---| --- | --- | --- |
| [!UICONTROL Détails de Media Collection] | `mediaCollection` | [[!UICONTROL Détails de Media Collection]](../../data-types/media-collection-details.md) | Attributs liés à une collection d’éléments multimédias. Utilisez les champs Collection de médias pour capturer des données et les envoyer à d’autres services Adobe en vue d’un traitement ultérieur. |
| [!UICONTROL Détails des rapports multimédia] | `mediaReporting` | [[!UICONTROL Détails des rapports multimédia]](../../data-types/media-reporting-details.md) | Détails des rapports et mesures associés au contenu multimédia. * Les champs Rapport multimédia sont utilisés par les services Adobe pour analyser les champs Media Collection envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures d’utilisateur spécifiques, sont calculées et font l’objet de rapports. |
| [!UICONTROL Liste Des Événements De Contenu Téléchargés De Media Collection] | `mediaDownloadedEvents` | [!UICONTROL Tableau] de [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Événements qui effectuent le suivi du téléchargement de contenu dans la collection de médias. |

{style="table-layout:auto"}

>[!TIP]
>
>Vous pouvez masquer les champs qui ne sont pas utilisés par l’API Media Edge. Le masquage de ces champs facilite la lecture et la compréhension du schéma, mais n’est pas obligatoire. Ces champs se rapportent uniquement à ceux du groupe de champs [!UICONTROL Détails de l’interaction MediaAnalytics]. Pour améliorer la lisibilité dans l’interface utilisateur d’Experience Platform, suivez les instructions de la documentation [Media Analytics sur la masquage des champs inutilisés](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
