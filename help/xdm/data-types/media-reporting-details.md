---
title: Type de données de détails des rapports multimédia
description: Découvrez le type de données Modèle de données d’expérience (XDM) des détails des rapports multimédia.
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 2%

---

# [!UICONTROL Détails du rapport multimédia] type de données

>[!NOTE]
>
>Les champs de collecte de médias capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs de collecte multimédia envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures d’utilisateur spécifiques, sont calculées et font l’objet de rapports.

[!UICONTROL Détails de création de rapports multimédia] est un type de données standard du modèle de données d’expérience (XDM) qui capture les détails essentiels sur les événements de lecture multimédia. Utilisez le type de données [!UICONTROL Détails de création de rapports multimédia] pour capturer des détails tels que la position de la tête de lecture dans le contenu, les identifiants de session uniques et diverses propriétés imbriquées liées à la session, entre autres. Ce type de données fournit une vue d’ensemble complète de l’expérience de lecture qui permet le suivi et l’analyse des modèles de consommation multimédia et des événements associés pendant les sessions de lecture.

>[!NOTE]
>
>Les champs mentionnés ci-dessous ne sont pas directement utilisés pour créer des requêtes. Au lieu de cela, la collecte des champs envoyés à Adobe Experience Platform ou Adobe Analytics est assemblée à partir des données de votre requête, et les mesures sont ensuite intégrées ou traitées par l’infrastructure du serveur. Alors qu’Experience Platform collecte différents types d’événements utilisateur, les rapports qui vous sont renvoyés se concentrent sur des événements spécifiques, tels que `media.sessionStart`, `media.adStart` et `media.sessionComplete`. Cela signifie que bien que vous transmettiez 12 types d’événements au cours de la collecte, vos rapports ne présenteront que des répartitions basées sur les cinq événements répertoriés ci-dessous.

+++Sélectionnez cette option pour afficher un diagramme du type de données [!UICONTROL Détails des rapports multimédia].
![Diagramme du type de données [!UICONTROL Détails des rapports multimédia].](../images/data-types/media-reporting-details.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Détails Advertising] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Les détails d’Advertising font référence à des informations spécifiques relatives aux activités publicitaires au cours de l’événement d’expérience. Cela inclut les métadonnées de publicité, les caractéristiques de ciblage et les mesures de performances. |
| [!UICONTROL Détails du pod Advertising] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Les détails des pods Advertising contiennent des informations sur les pods publicitaires au sein de l’événement d’expérience. Il fournit des informations sur la séquence publicitaire, le contenu et les mesures d’engagement. |
| [!UICONTROL Détails du chapitre] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Détails du chapitre capture les données relatives aux chapitres ou aux parties segmentées du contenu. Il fournit des informations sur les marqueurs de chapitre, les chronologies et les métadonnées associées. |
| [!UICONTROL Liste Des Etats] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | La propriété States est un tableau qui capture différents états tout au long de l’événement d’expérience. Cette propriété fournit des données séquentielles sur la lecture, les actions de l’utilisateur ou les modifications de contenu. |
| [!UICONTROL Détails Des Données Qoe] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | Les détails des données QoE (qualité de l’expérience) capturent les mesures liées aux performances et les données d’expérience utilisateur. Il fournit des informations sur la qualité, la réactivité et les interactions utilisateur. |
| [!UICONTROL Détails de la session] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Les détails de session englobent des informations complètes associées à l’événement d’expérience, offrant des informations sur les interactions utilisateur, la durée et les données contextuelles pertinentes pour la session de lecture. |
| [!UICONTROL Métadonnées personnalisées] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Les métadonnées personnalisées contiennent des métadonnées définies par l’utilisateur ou des métadonnées supplémentaires associées à l’événement d’expérience. Ces métadonnées permettent d’inclure des données personnalisées ou spécifiques dans le contexte de l’événement. |
| [!UICONTROL Tête de lecture] | `playhead` | Entier | Le curseur de lecture représente la position de lecture actuelle dans le contenu multimédia. Pour le contenu en direct, il indique la seconde actuelle de la journée (0 &lt;= curseur de lecture &lt; 86400). Pour le contenu enregistré, il reflète la seconde actuelle de la durée du contenu (0 &lt;= tête de lecture &lt; longueur du contenu). |

{style="table-layout:auto"}
