---
title: Tendances des audiences
description: Découvrez comment suivre et analyser les mesures d’audience au fil du temps à l’aide du tableau de bord Tendances de l’audience. Définissez des filtres d’audience, analysez les tendances de taille et d’identité et exportez des informations pour les décisions pilotées par les données.
exl-id: 8b2bc53a-0855-4a75-9149-79410543b4b0
TQID: https://experienceleague.adobe.com/ikabMqQViECGuHaA0DlXuOdsjEK7xeOOJq6vbvWYmyM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
subfeature_v2:
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
  - id: f6ac78a3-5b59-40f5-a37d-45df5303d3a3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 581
ht-degree: 1%

---

# Tendances des audiences

Analysez l’évolution de vos audiences au fil du temps avec des visualisations des mesures d’audience clés sur le tableau de bord [!UICONTROL Audience Trends]. Ce tableau de bord vous aide à suivre les tendances telles que la croissance de l’audience, le nombre d’identités et le nombre de profils d’identité uniques, et vous permet de prendre des décisions pilotées par les données. En analysant ces mesures, les spécialistes marketing peuvent optimiser les stratégies de ciblage, améliorer l’engagement de l’audience et affiner leurs efforts de segmentation pour rendre les campagnes plus efficaces.

## Filtrer des audiences {#filter-audiences}

Pour commencer votre analyse, utilisez le filtre global pour sélectionner les audiences spécifiques et la période que vous souhaitez analyser. Sélectionnez l’icône de filtre (![L’icône de filtre.](../../../images/icons/filter-icon-white.png)). pour ouvrir la boîte de dialogue **[!UICONTROL Filter]**, où vous pouvez :

1. **Sélectionner une audience** : choisissez l&#39;audience que vous souhaitez analyser (dans l&#39;exemple de capture d&#39;écran, l&#39;audience **Amoxicillin** a été sélectionnée).
1. **Définir une période** : sélectionnez une période prédéfinie dans le menu déroulant ou sélectionnez manuellement les dates de début et de fin à l’aide des champs de calendrier.

![Boîte de dialogue Filtres dans le tableau de bord Tendances de l’audience.](../../images/sql-insights-query-pro-mode/templates/audience-trends-filters.png)

Une fois vos filtres définis, sélectionnez **[!UICONTROL Apply]** pour mettre à jour le tableau de bord. Les filtres que vous avez choisis sont appliqués et des informations ciblées sur les audiences sélectionnées au cours d’une période donnée s’affichent. Vos filtres personnalisés garantissent que les données sont pertinentes par rapport aux objectifs de votre analyse.

![Tableau de bord Tendances de l’audience avec le filtre Segment Amoxicilin appliqué et mis en surbrillance.](../../images/sql-insights-query-pro-mode/templates/audience-trends-applied-filters.png)

## Graphiques de tendance d’audience disponibles {#available-charts}

Il existe trois graphiques principaux pour vous aider à comprendre les mesures d’audience au fil du temps. Pour chaque graphique, vous pouvez sélectionner l’ellipse (`...`) en haut à droite, suivie de [!UICONTROL View more] pour afficher un formulaire tabulé des résultats ou télécharger les données sous la forme d’un fichier CSV à afficher dans une feuille de calcul. Pour plus d’informations, consultez le guide [Afficher plus](../view-more.md).

>[!TIP]
>
>Vous pouvez pointer sur une date spécifique dans n’importe quel graphique pour afficher le nombre de profils individuels dans une boîte de dialogue.

### Tendances de la taille de l’audience {#audience-size-trends}

Le graphique **[!UICONTROL Audience size trends]** affiche le nombre de profils au sein de l’audience sélectionnée au fil du temps. Cela permet de suivre la croissance ou la réduction de l’audience. Vous pouvez utiliser ce graphique pour surveiller l’efficacité de l’engagement et comprendre les modifications de la taille de l’audience.

![Graphique des tendances de la taille des audiences.](../../images/sql-insights-query-pro-mode/templates/audience-size-trends-chart.png)

### Tendances des identités d’audience {#audience-identities-trends}

Le graphique **[!UICONTROL Audience identities trends]** fournit des informations sur le nombre total d’identités dans le segment d’audience. Utilisez ce graphique pour comprendre comment les identités uniques contribuent à la taille globale de l’audience. Cela fournit une indication de la stabilité et de l’engagement de l’audience.

![Graphique de tendance des identités d’audience.](../../images/sql-insights-query-pro-mode/templates/audience-identities-trends.png)

### Tendances De Taille D’Audience D’Identité Unique {#single-identity-audience-size-trends}

Le graphique **[!UICONTROL Single identity audience size trends]** indique le nombre de membres de l’audience ne disposant que d’une seule identité. Cette mesure est utile pour comprendre la composition de votre audience, en particulier en termes d’unicité des identités, et permet d’évaluer l’efficacité des efforts de combinaison d’identités.

![Graphique des tendances de la taille de l’audience à identité unique.](../../images/sql-insights-query-pro-mode/templates/single-identity-audience-size-trends.png)

## Export Insights {#export-insights}

Après avoir analysé les mesures et appliqué les filtres pertinents, vous pouvez exporter les données à des fins d’analyse hors ligne ou de création de rapports supplémentaires. Pour ce faire, sélectionnez **[!UICONTROL Export]** en haut à droite du tableau. La boîte de dialogue d’impression de PDF s’affiche. Dans cette boîte de dialogue, vous pouvez enregistrer les données visualisées sous la forme d’un PDF ou les imprimer.

![Tableau de bord Tendances de l’audience avec l’option Exporter mise en surbrillance.](../../images/sql-insights-query-pro-mode/templates/audience-trends-export.png)

## Étapes suivantes

Après lecture de ce document, vous avez appris à obtenir des informations précieuses sur le comportement de l’audience au fil du temps à partir du tableau de bord **Tendances de l’audience**. Pour en savoir plus sur les autres modèles de Distiller de données qui peuvent vous aider à prendre des décisions éclairées, à optimiser la segmentation et à améliorer les stratégies d’engagement, reportez-vous aux guides d’interface utilisateur [Comparaison d’audiences](./comparison.md), [Chevauchements d’identités d’audience](./identity-overlaps.md) et [Chevauchements d’audience avancés](./overlaps.md).
