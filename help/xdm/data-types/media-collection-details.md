---
title: Type de données Détails de la collection multimédia
description: Découvrez le type de données XDM (Media Collection Details Experience Data Model).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# [!UICONTROL Détails de la collection multimédia] type de données

[!UICONTROL Détails de la collection multimédia] est un type de données XDM (Experience Data Model) standard qui capture les détails essentiels des événements de lecture multimédia. Utilisez la variable [!UICONTROL Détails de la collection multimédia] type de données pour capturer des détails tels que la position du curseur de lecture dans le contenu, les identifiants de session uniques et diverses propriétés imbriquées liées à la session, entre autres. Ce type de données fournit un aperçu complet de l’expérience de lecture qui permet le suivi et l’analyse des schémas de consommation multimédia et des événements associés pendant les sessions de lecture.

>[!NOTE]
>
>Les champs Media Collection capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs Media Collection envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures utilisateur spécifiques, sont calculées et font l’objet de rapports.

+++Sélectionnez cette option pour afficher un diagramme du [!UICONTROL Détails de la collection multimédia] type de données.
![Un diagramme de [!UICONTROL Informations détaillées sur Media Collection] type de données.](../images/data-types/media-collection-details.png)
+++

| Nom d’affichage | Propriété | Événements requis pour | Type de données | Description |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Détails de la publicité] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Collection](./advertising-details-collection.md) | Détails de la publicité fait référence à des informations spécifiques relatives aux activités publicitaires au cours de l’événement d’expérience. Cela inclut les métadonnées de publicité, les détails de ciblage et les mesures de performances. |
| [!UICONTROL Détails de la capsule publicitaire] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Collection](./advertising-pod-details-collection.md) | Les détails de la capsule publicitaire contiennent des informations sur les capsules publicitaires dans l’événement d’expérience. Il fournit des informations sur la séquence publicitaire, le contenu et les mesures d’engagement. |
| [!UICONTROL Détails du chapitre] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Collection](./chapter-details-collection.md) | Les détails du chapitre capturent les données liées aux chapitres ou aux parties segmentées du contenu. Il fournit des informations sur les marqueurs de chapitre, les chronologies et les métadonnées associées. |
| [!UICONTROL Détails de l’erreur] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Collection](./error-details-collection.md) | Les détails de l’erreur contiennent des informations relatives aux erreurs survenues pendant l’événement d’expérience. Cela inclut les codes d’erreur, les descriptions, les horodatages et les données contextuelles pertinentes. |
| [!UICONTROL Fin de la liste des états] | `statesEnd` | Utilisé dans `statesUpdate` | [[!UICONTROL statesEnd] - Collection](./list-of-states-end-collection.md) | La fin des états fournit un tableau qui répertorie les états à la fin de l’événement d’expérience. Il contient des détails sur les états de lecture finaux ou l’état du contenu. |
| [!UICONTROL Liste des états Début] | `statesStart` | Utilisé dans `statesUpdate` | [[!UICONTROL statesStart] - Collection](./list-of-states-start-collection.md) | La section Début des états fournit un tableau qui répertorie les états au début de l’événement d’expérience. Il contient des données relatives à la lecture, aux actions de l’utilisateur ou aux détails du contenu. |
| [!UICONTROL Détails des données Qo] | `qoeDataDetails` | Facultatif pour tous | [[!UICONTROL qoeDataDetails] - Collection](./qoe-data-details-collection.md) | Les détails de la qualité de l’expérience capturent des mesures liées aux performances et des données d’expérience utilisateur. Il fournit des informations sur la qualité, la réactivité et les interactions utilisateur. |
| [!UICONTROL Détails de la session] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Collection](./session-details-collection.md) | Les détails de la session englobent des informations complètes associées à l’événement d’expérience, et offrent des informations sur les interactions utilisateur, la durée et les données contextuelles pertinentes pour la session de lecture. |
| [!UICONTROL Métadonnées personnalisées] | `customMetadata` | Facultatif pour `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Collection](./custom-metadata-details-collection.md) | Les métadonnées personnalisées contiennent des métadonnées définies par l’utilisateur ou des métadonnées supplémentaires associées à l’événement d’expérience. Ces métadonnées permettent d’inclure des données personnalisées ou spécifiques dans le contexte de l’événement. |
| [!UICONTROL ID de session multimédia] | `sessionID` | Tous les événements **Sauf** `sessionStart` et du contenu téléchargé. | Chaîne | L’ID de session multimédia identifie de manière unique une instance d’un flux de contenu au cours d’une session de lecture individuelle. Il sert d’identifiant distinct pour le suivi et la gestion de l’expérience de lecture spécifique associée à un utilisateur ou une visionneuse.<br><em>Remarque :<em>`sessionId` est envoyé sur tous les événements, à l’exception de `sessionStart` et pour tous les événements téléchargés. |
| [!UICONTROL Curseur de lecture] | `playhead` | Tous les événements | Entier | Le curseur de lecture représente la position de lecture actuelle dans le contenu multimédia. Pour le contenu en direct, il indique la seconde de la journée en cours (0 &lt;= playhead &lt; 86400). Pour le contenu enregistré, il reflète la seconde actuelle de la durée du contenu (0 &lt;= curseur de lecture &lt; longueur du contenu). |

{style="table-layout:auto"}
