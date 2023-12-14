---
title: Type de données des détails du média
description: Découvrez le type de données XDM (Media Details Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 2%

---

# [!UICONTROL Informations détaillées sur le média] type de données

[!UICONTROL Informations détaillées sur le média] est un type de données XDM (Experience Data Model) standard qui capture les détails essentiels des événements de lecture multimédia. Utilisez la variable [!UICONTROL Informations détaillées sur le média] type de données pour capturer des détails tels que la position du curseur de lecture dans le contenu, les identifiants de session uniques et diverses propriétés imbriquées liées à la session, entre autres. Ce type de données fournit un aperçu complet de l’expérience de lecture, qui permet le suivi et l’analyse des schémas de consommation multimédia et des événements associés pendant les sessions de lecture.

+++Sélectionnez cette option pour afficher un diagramme du [!UICONTROL Informations détaillées sur le média] type de données.
![Un diagramme de [!UICONTROL Informations détaillées sur le média] type de données.](../images/data-types/media-details-information.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Curseur de lecture] | `playhead` | nombre entier | Le curseur de lecture représente la position de lecture actuelle dans le contenu multimédia. Pour le contenu en direct, il indique la seconde de la journée en cours (0 &lt;= playhead &lt; 86400). Pour le contenu enregistré, il reflète la seconde actuelle de la durée du contenu (0 &lt;= curseur de lecture &lt; longueur du contenu). |
| [!UICONTROL ID de session multimédia] | `sessionID` | chaîne | L’ID de session multimédia identifie de manière unique une instance d’un flux de contenu au cours d’une session de lecture individuelle. Il sert d’identifiant distinct pour le suivi et la gestion de l’expérience de lecture spécifique associée à un utilisateur ou une visionneuse. |
| [!UICONTROL Détails de la session] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | Les détails de la session englobent des informations complètes associées à l’événement d’expérience, et offrent des informations sur les interactions utilisateur, la durée et les données contextuelles pertinentes pour la session de lecture. |
| [!UICONTROL Détails de la publicité] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | Détails de la publicité fait référence à des informations spécifiques relatives aux activités publicitaires au cours de l’événement d’expérience. Cela inclut les métadonnées de publicité, les détails de ciblage et les mesures de performances. |
| [!UICONTROL Détails de la capsule publicitaire] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | Les détails de la capsule publicitaire contiennent des informations sur les capsules publicitaires dans l’événement d’expérience. Il fournit des informations sur la séquence publicitaire, le contenu et les mesures d’engagement. |
| [!UICONTROL Détails du chapitre] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | Les détails du chapitre capturent les données liées aux chapitres ou aux parties segmentées du contenu. Il fournit des informations sur les marqueurs de chapitre, les chronologies et les métadonnées associées. |
| [!UICONTROL Détails de l’erreur] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | Les détails de l’erreur contiennent des informations relatives aux erreurs survenues pendant l’événement d’expérience. Cela inclut les codes d’erreur, les descriptions, les horodatages et les données contextuelles pertinentes. |
| [!UICONTROL Détails des données Qo] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | Les détails de la qualité de l’expérience capturent des mesures liées aux performances et des données d’expérience utilisateur. Il fournit des informations sur la qualité, la réactivité et les interactions utilisateur. |
| [!UICONTROL Liste des états Début] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | La section Début des états fournit un tableau qui répertorie les états au début de l’événement d’expérience. Il contient des données relatives à la lecture, aux actions de l’utilisateur ou aux détails du contenu. |
| [!UICONTROL Fin de la liste des états] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | La fin des états fournit un tableau qui répertorie les états à la fin de l’événement d’expérience. Il contient des détails sur les états de lecture finaux ou l’état du contenu. |
| [!UICONTROL Liste des États] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | La propriété States est un tableau qui capture différents états tout au long de l’événement d’expérience. Cette propriété fournit des données séquentielles sur la lecture, les actions de l’utilisateur ou les modifications de contenu. |
| [!UICONTROL Métadonnées personnalisées] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | Les métadonnées personnalisées contiennent des métadonnées définies par l’utilisateur ou des métadonnées supplémentaires associées à l’événement d’expérience. Ces métadonnées permettent d’inclure des données personnalisées ou spécifiques dans le contexte de l’événement. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
