---
title: Type de données Détails de la collecte de médias
description: Découvrez le type de données Modèle de données d’expérience (XDM) des détails de collecte de médias.
exl-id: 1faf60f7-6afb-4ce2-b50d-967776a57715
TQID: https://experienceleague.adobe.com/q-4VpUsYBDB8i-RmaDywDWCB1BMSsSO78O8qUwK-SbI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 529
ht-degree: 3%

---

# Type de données [!UICONTROL Media Collection Details]

[!UICONTROL Media Collection Details] est un type de données standard du modèle de données d’expérience (XDM) qui capture les détails essentiels sur les événements de lecture multimédia. Utilisez le type de données [!UICONTROL Media Collection Details] pour capturer des détails tels que la position de la tête de lecture dans le contenu, les identifiants de session uniques et diverses propriétés imbriquées liées à la session, entre autres. Ce type de données fournit une vue d’ensemble complète de l’expérience de lecture qui permet le suivi et l’analyse des modèles de consommation multimédia et des événements associés pendant les sessions de lecture.

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaCollection`, c’est-à-dire aux champs que votre implémentation envoie au serveur principal des médias en flux continu. Adobe traite ces données de collecte et génère des champs de schéma `mediaReporting`, qui sont ingérés dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations sur ce flux de données.

+++Sélectionnez cette option pour afficher un diagramme du type de données [!UICONTROL Media Collection details].
![Diagramme du type de données [!UICONTROL Media Collection details information].](../images/data-types/media-collection-details.png)
+++

| Nom d’affichage | Propriété | Événements requis pour | Type de données | Description |
|---|---|---|---|---|
| [!UICONTROL Advertising Details] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Collection](./advertising-details-collection.md) | Les détails d’Advertising font référence à des informations spécifiques relatives aux activités publicitaires au cours de l’événement d’expérience. Cela inclut les métadonnées de publicité, les caractéristiques de ciblage et les mesures de performances. |
| [!UICONTROL Advertising Pod Details] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Collection](./advertising-pod-details-collection.md) | Les détails des pods Advertising contiennent des informations sur les pods publicitaires au sein de l’événement d’expérience. Il fournit des informations sur la séquence publicitaire, le contenu et les mesures d’engagement. |
| [!UICONTROL Chapter Details] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Collection](./chapter-details-collection.md) | Détails du chapitre capture les données relatives aux chapitres ou aux parties segmentées du contenu. Il fournit des informations sur les marqueurs de chapitre, les chronologies et les métadonnées associées. |
| [!UICONTROL Error Details] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Collection](./error-details-collection.md) | Les Détails de l’erreur contiennent des informations relatives aux erreurs rencontrées lors de l’événement d’expérience. Cela inclut les codes d’erreur, les descriptions, les horodatages et les données contextuelles pertinentes. |
| [!UICONTROL List Of States End] | `statesEnd` | Utilisé dans `statesUpdate` | [[!UICONTROL statesEnd] - Collection](./list-of-states-end-collection.md) | La fin des états fournit un tableau pour répertorier les états à la fin de l’événement d’expérience. Il contient des détails sur les états de lecture finaux ou le statut du contenu. |
| [!UICONTROL List Of States Start] | `statesStart` | Utilisé dans `statesUpdate` | [[!UICONTROL statesStart] - Collection](./list-of-states-start-collection.md) | Le Début des états fournit un tableau pour répertorier les états au début de l’événement d’expérience. Il contient des données relatives à la lecture, aux actions des utilisateurs ou à des caractéristiques spécifiques au contenu. |
| [!UICONTROL Qoe Data Details] | `qoeDataDetails` | Facultatif pour tous | [[!UICONTROL qoeDataDetails] - Collection](./qoe-data-details-collection.md) | Les détails des données QoE (qualité de l’expérience) capturent les mesures liées aux performances et les données d’expérience utilisateur. Il fournit des informations sur la qualité, la réactivité et les interactions utilisateur. |
| [!UICONTROL Session Details] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Collection](./session-details-collection.md) | Les détails de session englobent des informations complètes associées à l’événement d’expérience, offrant des informations sur les interactions utilisateur, la durée et les données contextuelles pertinentes pour la session de lecture. |
| [!UICONTROL The Custom Metadata] | `customMetadata` | Facultatif pour `sessionStart`, `adStart`, `chapterStart` | [[!UICONTROL customMetadataDetails] - Collection](./custom-metadata-details-collection.md) | Les métadonnées personnalisées contiennent des métadonnées définies par l’utilisateur ou des métadonnées supplémentaires associées à l’événement d’expérience. Ces métadonnées permettent d’inclure des données personnalisées ou spécifiques dans le contexte de l’événement. |
| [!UICONTROL Media Session ID] | `sessionID` | Tous les événements **sauf** contenu `sessionStart` et téléchargé. | chaîne | L’ID de session multimédia identifie de manière unique une instance d’un flux de contenu au cours d’une session de lecture individuelle. Il sert d’identifiant distinct pour le suivi et la gestion de l’expérience de lecture spécifique associée à un utilisateur ou à une visionneuse.<br><em>Remarque :<em>`sessionId` est envoyé sur tous les événements, à l’exception des `sessionStart` et de tous les événements téléchargés. |
| [!UICONTROL Playhead] | `playhead` | Tous les événements | entier | Le curseur de lecture représente la position de lecture actuelle dans le contenu multimédia. Pour le contenu en direct, il indique la seconde actuelle de la journée (0 &lt;= curseur de lecture &lt; 86400). Pour le contenu enregistré, il reflète la seconde actuelle de la durée du contenu (0 &lt;= tête de lecture &lt; longueur du contenu). |

Voir [mediadetails.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) dans le référentiel XDM public pour la définition complète du schéma.
