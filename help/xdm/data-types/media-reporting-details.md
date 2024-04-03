---
title: Type de données Détails des rapports multimédia
description: Découvrez le type de données XDM (Media Reporting Details) du modèle de données d’expérience (XDM).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 2%

---

# [!UICONTROL Détails sur les rapports multimédia] type de données

>[!NOTE]
>
>Les champs Media Collection capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs Media Collection envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures utilisateur spécifiques, sont calculées et font l’objet de rapports.

[!UICONTROL Détails sur les rapports multimédia] est un type de données XDM (Experience Data Model) standard qui capture les détails essentiels des événements de lecture multimédia. Utilisez la variable [!UICONTROL Détails sur les rapports multimédia] type de données pour capturer des détails tels que la position du curseur de lecture dans le contenu, les identifiants de session uniques et diverses propriétés imbriquées liées à la session, entre autres. Ce type de données fournit un aperçu complet de l’expérience de lecture qui permet le suivi et l’analyse des schémas de consommation multimédia et des événements associés pendant les sessions de lecture.

>[!NOTE]
>
>Les champs mentionnés ci-dessous ne sont pas directement utilisés pour créer des requêtes. Au lieu de cela, la collecte des champs envoyés à Adobe Experience Platform ou Adobe Analytics est assemblée à partir des données de votre requête, et les mesures sont ensuite incorporées ou traitées par l’infrastructure du serveur. Bien que Platform collecte divers types d’événements utilisateur, les rapports qui vous sont renvoyés portent sur des événements spécifiques, tels que `media.sessionStart`, `media.adStart`, et `media.sessionComplete`. En d’autres termes, bien que vous transmettiez 12 types d’événements au cours de la collecte, vos rapports ne contiendront que des ventilations basées sur les cinq événements répertoriés ci-dessous.

+++Sélectionnez cette option pour afficher un diagramme du [!UICONTROL Détails sur les rapports multimédia] type de données.
![Un diagramme de [!UICONTROL Détails sur les rapports multimédia] type de données.](../images/data-types/media-reporting-details.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Détails de la publicité] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Détails de la publicité fait référence à des informations spécifiques relatives aux activités publicitaires au cours de l’événement d’expérience. Cela inclut les métadonnées de publicité, les détails de ciblage et les mesures de performances. |
| [!UICONTROL Détails de la capsule publicitaire] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Les détails de la capsule publicitaire contiennent des informations sur les capsules publicitaires dans l’événement d’expérience. Il fournit des informations sur la séquence publicitaire, le contenu et les mesures d’engagement. |
| [!UICONTROL Détails du chapitre] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Les détails du chapitre capturent les données liées aux chapitres ou aux parties segmentées du contenu. Il fournit des informations sur les marqueurs de chapitre, les chronologies et les métadonnées associées. |
| [!UICONTROL Liste des États] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | La propriété States est un tableau qui capture différents états tout au long de l’événement d’expérience. Cette propriété fournit des données séquentielles sur la lecture, les actions de l’utilisateur ou les modifications de contenu. |
| [!UICONTROL Détails des données Qo] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | Les détails de la qualité de l’expérience capturent des mesures liées aux performances et des données d’expérience utilisateur. Il fournit des informations sur la qualité, la réactivité et les interactions utilisateur. |
| [!UICONTROL Détails de la session] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Les détails de la session englobent des informations complètes associées à l’événement d’expérience, et offrent des informations sur les interactions utilisateur, la durée et les données contextuelles pertinentes pour la session de lecture. |
| [!UICONTROL Métadonnées personnalisées] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Les métadonnées personnalisées contiennent des métadonnées définies par l’utilisateur ou des métadonnées supplémentaires associées à l’événement d’expérience. Ces métadonnées permettent d’inclure des données personnalisées ou spécifiques dans le contexte de l’événement. |
| [!UICONTROL Curseur de lecture] | `playhead` | Entier | Le curseur de lecture représente la position de lecture actuelle dans le contenu multimédia. Pour le contenu en direct, il indique la seconde de la journée en cours (0 &lt;= playhead &lt; 86400). Pour le contenu enregistré, il reflète la seconde actuelle de la durée du contenu (0 &lt;= curseur de lecture &lt; longueur du contenu). |

{style="table-layout:auto"}
