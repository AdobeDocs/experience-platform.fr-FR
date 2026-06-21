---
title: Type de données de détails des rapports multimédia
description: Découvrez le type de données Modèle de données d’expérience (XDM) des détails des rapports multimédia.
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
TQID: https://experienceleague.adobe.com/MLC4d9PHdRwITgKnKdm3SUl6PaCNwwY56cvaZN2pNbc
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
source-wordcount: 450
ht-degree: 3%

---

# [!UICONTROL Détails du rapport multimédia] type de données

[!UICONTROL Détails de création de rapports multimédia] est un type de données standard du modèle de données d’expérience (XDM) qui capture les détails essentiels sur les événements de lecture multimédia. Utilisez le type de données [!UICONTROL Détails de création de rapports multimédia] pour capturer des détails tels que la position de la tête de lecture dans le contenu, les identifiants de session uniques et diverses propriétés imbriquées liées à la session, entre autres. Ce type de données fournit une vue d’ensemble complète de l’expérience de lecture qui permet le suivi et l’analyse des modèles de consommation multimédia et des événements associés pendant les sessions de lecture.

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaReporting` : les champs qu’Adobe calcule à partir des données `mediaCollection` envoyées par votre implémentation et ingérées dans les jeux de données Platform. Ces champs ne sont pas envoyés directement à partir de votre implémentation. Bien que votre implémentation transmette de nombreux types d’événements, Platform ingère des enregistrements pour cinq événements clés : `media.sessionStart`, `media.adStart`, `media.adComplete`, `media.chapterComplete` et `media.sessionComplete`. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

+++Sélectionnez cette option pour afficher un diagramme du type de données [!UICONTROL Détails des rapports multimédia].
![Diagramme du type de données [!UICONTROL Détails des rapports multimédia].](../images/data-types/media-reporting-details.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
|---|---|---|---|
| [!UICONTROL Détails &#x200B;] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Les détails d’Advertising font référence à des informations spécifiques relatives aux activités publicitaires au cours de l’événement d’expérience. Cela inclut les métadonnées de publicité, les caractéristiques de ciblage et les mesures de performances. |
| [!UICONTROL Détails du pod &#x200B;] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Les détails des pods Advertising contiennent des informations sur les pods publicitaires au sein de l’événement d’expérience. Il fournit des informations sur la séquence publicitaire, le contenu et les mesures d’engagement. |
| [!UICONTROL Détails du chapitre] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Détails du chapitre capture les données relatives aux chapitres ou aux parties segmentées du contenu. Il fournit des informations sur les marqueurs de chapitre, les chronologies et les métadonnées associées. |
| [!UICONTROL Liste Des Etats] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | La propriété States est un tableau qui capture différents états tout au long de l’événement d’expérience. Cette propriété fournit des données séquentielles sur la lecture, les actions de l’utilisateur ou les modifications de contenu. |
| [!UICONTROL Détails Des Données Qoe] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | Les détails des données QoE (qualité de l’expérience) capturent les mesures liées aux performances et les données d’expérience utilisateur. Il fournit des informations sur la qualité, la réactivité et les interactions utilisateur. |
| [!UICONTROL Détails de la session] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Les détails de session englobent des informations complètes associées à l’événement d’expérience, offrant des informations sur les interactions utilisateur, la durée et les données contextuelles pertinentes pour la session de lecture. |
| [!UICONTROL Métadonnées personnalisées] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Les métadonnées personnalisées contiennent des métadonnées définies par l’utilisateur ou des métadonnées supplémentaires associées à l’événement d’expérience. Ces métadonnées permettent d’inclure des données personnalisées ou spécifiques dans le contexte de l’événement. |
| [!UICONTROL Tête de lecture] | `playhead` | entier | Le curseur de lecture représente la position de lecture actuelle dans le contenu multimédia. Pour le contenu en direct, il indique la seconde actuelle de la journée (0 &lt;= curseur de lecture &lt; 86400). Pour le contenu enregistré, il reflète la seconde actuelle de la durée du contenu (0 &lt;= tête de lecture &lt; longueur du contenu). |

Voir [mediadetails.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) dans le référentiel XDM public pour la définition complète du schéma.
