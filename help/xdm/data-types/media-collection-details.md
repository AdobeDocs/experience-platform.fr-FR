---
title: Type de données Détails de la collection multimédia
description: Découvrez le type de données XDM (Media Collection Details Experience Data Model).
exl-id: 1faf60f7-6afb-4ce2-b50d-967776a57715
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Type de données [!UICONTROL Media Collection Details]

[!UICONTROL Media Collection Details] est un type de données XDM (modèle de données d’expérience) standard qui capture les détails essentiels sur les événements de lecture multimédia. Utilisez le type de données [!UICONTROL Détails de la collection multimédia] pour capturer des détails tels que la position du curseur de lecture dans le contenu, les identifiants de session uniques et diverses propriétés imbriquées liées à la session, entre autres. Ce type de données fournit un aperçu complet de l’expérience de lecture qui permet le suivi et l’analyse des schémas de consommation multimédia et des événements associés pendant les sessions de lecture.

>[!NOTE]
>
>Les champs Media Collection capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs Media Collection envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures utilisateur spécifiques, sont calculées et font l’objet de rapports.

+++Sélectionnez cette option pour afficher un diagramme du type de données [!UICONTROL Media Collection details].
![&#x200B; Diagramme du type de données [!UICONTROL Media Collection details information].](../images/data-types/media-collection-details.png)
+++

| Nom d’affichage | Propriété | Événements requis pour | Type de données | Description |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Détails Advertising] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Collection](./advertising-details-collection.md) | Advertising Détails se rapporte à des informations spécifiques relatives aux activités publicitaires au cours de l’événement d’expérience. Cela inclut les métadonnées de publicité, les détails de ciblage et les mesures de performances. |
| [!UICONTROL Détails de la capsule Advertising] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Collection](./advertising-pod-details-collection.md) | Les détails de la capsule Advertising contiennent des informations sur les capsules publicitaires dans l’événement d’expérience. Il fournit des informations sur la séquence publicitaire, le contenu et les mesures d’engagement. |
| [!UICONTROL Détails du chapitre] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Collection](./chapter-details-collection.md) | Les détails du chapitre capturent les données liées aux chapitres ou aux parties segmentées du contenu. Il fournit des informations sur les marqueurs de chapitre, les chronologies et les métadonnées associées. |
| [!UICONTROL Détails de l’erreur] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Collection](./error-details-collection.md) | Les détails de l’erreur contiennent des informations relatives aux erreurs survenues pendant l’événement d’expérience. Cela inclut les codes d’erreur, les descriptions, les horodatages et les données contextuelles pertinentes. |
| [!UICONTROL Fin De Liste Des États] | `statesEnd` | Utilisé dans `statesUpdate` | [[!UICONTROL statesEnd] - Collection](./list-of-states-end-collection.md) | La fin des états fournit un tableau qui répertorie les états à la fin de l’événement d’expérience. Il contient des détails sur les états de lecture finaux ou l’état du contenu. |
| [!UICONTROL Liste Des États Début] | `statesStart` | Utilisé dans `statesUpdate` | [[!UICONTROL statesStart] - Collection](./list-of-states-start-collection.md) | La section Début des états fournit un tableau qui répertorie les états au début de l’événement d’expérience. Il contient des données relatives à la lecture, aux actions de l’utilisateur ou aux détails du contenu. |
| [!UICONTROL Détails des données Qoe] | `qoeDataDetails` | Facultatif pour tous | [[!UICONTROL qoeDataDetails] - Collection](./qoe-data-details-collection.md) | Les détails de la qualité de l’expérience capturent des mesures liées aux performances et des données d’expérience utilisateur. Il fournit des informations sur la qualité, la réactivité et les interactions utilisateur. |
| [!UICONTROL Détails de la session] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Collection](./session-details-collection.md) | Les détails de la session englobent des informations complètes associées à l’événement d’expérience, et offrent des informations sur les interactions utilisateur, la durée et les données contextuelles pertinentes pour la session de lecture. |
| [!UICONTROL Métadonnées personnalisées] | `customMetadata` | Facultatif pour `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Collection](./custom-metadata-details-collection.md) | Les métadonnées personnalisées contiennent des métadonnées définies par l’utilisateur ou des métadonnées supplémentaires associées à l’événement d’expérience. Ces métadonnées permettent d’inclure des données personnalisées ou spécifiques dans le contexte de l’événement. |
| [!UICONTROL ID de session multimédia] | `sessionID` | Tous les événements **à l&#39;exception de** `sessionStart` et le contenu téléchargé. | Chaîne | L’ID de session multimédia identifie de manière unique une instance d’un flux de contenu au cours d’une session de lecture individuelle. Il sert d’identifiant distinct pour le suivi et la gestion de l’expérience de lecture spécifique associée à un utilisateur ou une visionneuse.<br><em>Remarque : <em>`sessionId` est envoyé sur tous les événements, à l’exception de `sessionStart` et de tous les événements téléchargés. |
| [!UICONTROL Playhead] | `playhead` | Tous les événements | Entier | Le curseur de lecture représente la position de lecture actuelle dans le contenu multimédia. Pour le contenu en direct, il indique la seconde de la journée en cours (0 &lt;= playhead &lt; 86400). Pour le contenu enregistré, il reflète la seconde actuelle de la durée du contenu (0 &lt;= curseur de lecture &lt; longueur du contenu). |

{style="table-layout:auto"}
