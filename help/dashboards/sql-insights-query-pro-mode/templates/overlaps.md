---
title: Chevauchements avancés des audiences
description: Découvrez comment analyser les intersections des audiences et prendre des décisions pilotées par les données à l’aide du tableau de bord Avancé sur les chevauchements d’audiences. Filtrer les audiences, comparer les chevauchements et exporter des informations pour améliorer les stratégies de ciblage.
exl-id: 8a974b97-6fa0-4700-891c-73a72c8c84dc
TQID: https://experienceleague.adobe.com/7QEjI6rlHIf47FaN4Fst7i0Pl3G8BMRtjB2n-ZA-PpA
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773id: f6ac78a3-5b59-40f5-a37d-45df5303d3a3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: e1e0219c-f879-479f-8427-888ed2a6e9c2id: ff2b9b37-92e0-45fc-b853-379d44c08c89
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 473
ht-degree: 2%

---

# Chevauchements avancés des audiences

Obtenez des informations précieuses pour optimiser vos stratégies de ciblage et de segmentation d’audience en analysant la manière dont différents segments d’audience interagissent avec le tableau de bord [!UICONTROL Advanced Audience Overlaps]. Examinez les mesures tabulées pour identifier les chevauchements, affiner la segmentation et réduire les messages redondants. En fin de compte, vous pouvez utiliser ces informations pour créer des campagnes plus ciblées et des efforts marketing efficaces. Sur ce tableau de bord, vous pouvez examiner les intersections des audiences, appliquer des filtres et effectuer une analyse de chevauchement détaillée pour prendre des décisions basées sur les données et améliorer les résultats d’engagement.

## Filtrer les audiences {#filter-audiences}

Pour filtrer des audiences spécifiques pour l’analyse de chevauchement, sélectionnez l’icône de filtre (![L’icône de filtre.](../../../images/icons/filter-icon-white.png)) pour ouvrir la boîte de dialogue [!UICONTROL Filter]. À partir de là, vous pouvez ajouter ou supprimer des audiences du modèle de chevauchement pour affiner votre analyse.

![La vue Chevauchements d’audience avancés avec l’icône de filtre mise en surbrillance.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-filter-icon.png)

La boîte de dialogue [!UICONTROL Filters] s’affiche. Pour choisir une audience pour l’analyse de chevauchement, sélectionnez un nom d’audience dans la liste déroulante **[!UICONTROL Audience]** . Le nom de toute audience que vous ajoutez s’affiche avec une balise sous la liste déroulante. Une fois ajoutés, vous pouvez sélectionner les « X » par leur nom pour les supprimer. Pour supprimer tous les filtres appliqués, sélectionnez **[!UICONTROL Clear all]**.

## Filtres appliqués {#applied-filters}

Une fois un filtre appliqué ([!UICONTROL Amoxicilin Segment] dans l’exemple de capture d’écran), les données d’audience affichées sont réduites. Toutes les audiences supplémentaires que vous choisissez d’ajouter sont affichées à côté de la balise [!UICONTROL Filtering by] au-dessus du graphique [!UICONTROL Advanced Audience overlaps].

![Le tableau de bord Audience avancée chevauche avec Filtrage par segment Amoxicilin mis en surbrillance.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-applied-filters.png)

## Tableau Avancé De Chevauchements D’Audiences {#advanced-audience-overlaps-table}

La section principale du tableau de bord affiche le tableau de [!UICONTROL Advanced Audience Overlaps], qui fournit une comparaison détaillée des chevauchements d’audiences entre différents segments. Les colonnes du tableau sont les suivantes :

| Nom de la colonne | Description |
|------------------------------------|----------------------------------------------------------------------------------------------|
| **[!UICONTROL Source_Segment_Name]** | L’audience originale en cours d’analyse (par exemple, « Segment Amoxicilline »). |
| **[!UICONTROL Overlap_Segment_Name]** | Audience dont les chevauchements sont comparés à (par exemple, « Glucose sanguin > 100 »). |
| **[!UICONTROL Source_Segment_Audience_Count]** | Nombre total de profils de l’audience source. |
| **[!UICONTROL Overlap_Segment_Audience_Count]** | Taille de l’audience qui se chevauche, qui varie en fonction du chevauchement. |
| **[!UICONTROL Overlap_Audience_Count]** | Taille de l’audience qui se chevauche réellement entre l’audience source et l’audience qui se chevauche. |

{style="table-layout:auto"}

## Export Insights {#export-insights}

Une fois les audiences filtrées et analysées, vous pouvez exporter les données à des fins d’analyse hors ligne ou de création de rapports. Pour exporter vos informations, sélectionnez **[!UICONTROL Export]** en haut à droite du tableau. La boîte de dialogue d’impression de PDF s’affiche, vous permettant d’enregistrer les données en tant que PDF ou de les imprimer.

![La vue Chevauchement des audiences avancées avec l’option Exporter mise en surbrillance.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-export.png)

Pour revenir à l’aperçu de la [!UICONTROL Template], sélectionnez **[!UICONTROL Templates]**.

![La vue Chevauchement des audiences avancées avec les modèles mis en surbrillance.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-navigation.png)

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment analyser les intersections d’audience et prendre des décisions basées sur les données à l’aide du tableau de bord **[!UICONTROL Advanced Audience Overlaps]**. Pour optimiser davantage vos stratégies de ciblage et de segmentation d’audience, explorez d’autres modèles de Distiller de données qui fournissent des informations précieuses. Consultez les guides [Tendances d’audience](./trends.md), [Comparaison d’audience](./comparison.md) et [Chevauchements d’identités d’audience](./identity-overlaps.md) de l’interface utilisateur pour continuer à améliorer l’engagement de votre audience et vos efforts de segmentation.
