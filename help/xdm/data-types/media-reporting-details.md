---
title: Type de données de détails des rapports multimédia
description: Découvrez le type de données Modèle de données d’expérience (XDM) des détails des rapports multimédia.
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
TQID: https://experienceleague.adobe.com/MLC4d9PHdRwITgKnKdm3SUl6PaCNwwY56cvaZN2pNbc
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 455
ht-degree: 1%

---

# Type de données [!UICONTROL Media Reporting Details]

>[!NOTE]
>
>Les champs de collecte de médias capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs de collecte multimédia envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures d’utilisateur spécifiques, sont calculées et font l’objet de rapports.

[!UICONTROL Media Reporting Details] est un type de données standard du modèle de données d’expérience (XDM) qui capture les détails essentiels sur les événements de lecture multimédia. Utilisez le type de données [!UICONTROL Media Reporting Details] pour capturer des détails tels que la position de la tête de lecture dans le contenu, les identifiants de session uniques et diverses propriétés imbriquées liées à la session, entre autres. Ce type de données fournit une vue d’ensemble complète de l’expérience de lecture qui permet le suivi et l’analyse des modèles de consommation multimédia et des événements associés pendant les sessions de lecture.

>[!NOTE]
>
>Les champs mentionnés ci-dessous ne sont pas directement utilisés pour créer des requêtes. Au lieu de cela, la collecte des champs envoyés à Adobe Experience Platform ou Adobe Analytics est assemblée à partir des données de votre requête, et les mesures sont ensuite intégrées ou traitées par l’infrastructure du serveur. Alors qu’Experience Platform collecte différents types d’événements utilisateur, les rapports qui vous sont renvoyés se concentrent sur des événements spécifiques, tels que `media.sessionStart`, `media.adStart` et `media.sessionComplete`. Cela signifie que bien que vous transmettiez 12 types d’événements au cours de la collecte, vos rapports ne présenteront que des répartitions basées sur les cinq événements répertoriés ci-dessous.

+++Sélectionnez cette option pour afficher un diagramme du type de données [!UICONTROL Media Reporting Details].
![Diagramme du type de données [!UICONTROL Media Reporting Details].](../images/data-types/media-reporting-details.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Advertising Details] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Les détails d’Advertising font référence à des informations spécifiques relatives aux activités publicitaires au cours de l’événement d’expérience. Cela inclut les métadonnées de publicité, les caractéristiques de ciblage et les mesures de performances. |
| [!UICONTROL Advertising Pod Details] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Les détails des pods Advertising contiennent des informations sur les pods publicitaires au sein de l’événement d’expérience. Il fournit des informations sur la séquence publicitaire, le contenu et les mesures d’engagement. |
| [!UICONTROL Chapter Details] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Détails du chapitre capture les données relatives aux chapitres ou aux parties segmentées du contenu. Il fournit des informations sur les marqueurs de chapitre, les chronologies et les métadonnées associées. |
| [!UICONTROL List Of States] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | La propriété States est un tableau qui capture différents états tout au long de l’événement d’expérience. Cette propriété fournit des données séquentielles sur la lecture, les actions de l’utilisateur ou les modifications de contenu. |
| [!UICONTROL Qoe Data Details] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | Les détails des données QoE (qualité de l’expérience) capturent les mesures liées aux performances et les données d’expérience utilisateur. Il fournit des informations sur la qualité, la réactivité et les interactions utilisateur. |
| [!UICONTROL Session Details] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Les détails de session englobent des informations complètes associées à l’événement d’expérience, offrant des informations sur les interactions utilisateur, la durée et les données contextuelles pertinentes pour la session de lecture. |
| [!UICONTROL The Custom Metadata] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Les métadonnées personnalisées contiennent des métadonnées définies par l’utilisateur ou des métadonnées supplémentaires associées à l’événement d’expérience. Ces métadonnées permettent d’inclure des données personnalisées ou spécifiques dans le contexte de l’événement. |
| [!UICONTROL Playhead] | `playhead` | entier | Le curseur de lecture représente la position de lecture actuelle dans le contenu multimédia. Pour le contenu en direct, il indique la seconde actuelle de la journée (0 &lt;= curseur de lecture &lt; 86400). Pour le contenu enregistré, il reflète la seconde actuelle de la durée du contenu (0 &lt;= tête de lecture &lt; longueur du contenu). |

{style="table-layout:auto"}
