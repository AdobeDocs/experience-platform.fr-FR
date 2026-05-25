---
title: Exploration en amont du mode Query Pro
description: Découvrez comment accéder à un nouveau tableau de bord à partir de n’importe quel graphique pour explorer vos données à l’aide de l’exploration amont.
exl-id: d38550ba-1c56-4b6b-bf96-f21da232ba34
TQID: https://experienceleague.adobe.com/fGS2i8Zv1Cjod23K71Ylx7A3D-UrgadQrf5xgACZoYM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 417
ht-degree: 0%

---

# Analyser en amont {#drill-through}

L’exploration en amont facilite l’analyse des données à plusieurs couches en facilitant la navigation de n’importe quel graphique vers un nouveau tableau de bord. Cette fonctionnalité facilite la transition de présentations de haut niveau vers des rapports détaillés lors de l’étude des tendances, du comportement des clients et clientes, des indicateurs opérationnels, etc., en vous assurant de toujours disposer du contexte dont vous avez besoin.

Le système garantit que l’analyse que vous commencez se poursuit de manière transparente tout au long de l’expérience d’exploration complète en transmettant automatiquement les filtres globaux et les filtres de période des tableaux de bord sources aux tableaux de bord cibles. Pour faciliter la navigation entre les différentes couches de l&#39;étude, le système permet des forages à plusieurs niveaux.

## Créer une exploration amont {#create-drill-through}

Pour créer une exploration, commencez par sélectionner **[!UICONTROL Edit]** dans la vue de votre tableau de bord.

![Tableau de bord personnalisé avec l’option Modifier mise en surbrillance.](../images/sql-insights-query-pro-mode/drill-through.png)

Sélectionnez les points de suspension dans le graphique que vous souhaitez analyser, puis sélectionnez **[!UICONTROL Edit]**.

![Graphique affichant le menu représentant des points de suspension avec l’option Modifier mise en surbrillance.](../images/sql-insights-query-pro-mode/drill-through-chart-edit.png)

Dans le panneau [!UICONTROL Properties], utilisez le bouton (bascule) pour activer le **[!UICONTROL Enable drill through]**, puis utilisez la liste déroulante pour sélectionner le **[!UICONTROL Target dashboard]**. Assurez-vous que le bouton (bascule) correspondant à **[!UICONTROL Filter pass-through]** est activé, puis sélectionnez **[!UICONTROL Save and close]**.

![Panneau des propriétés du graphique avec les options Activer l’exploration amont, Tableau de bord cible et Transmission du filtre mises en surbrillance.](../images/sql-insights-query-pro-mode/drill-through-chart-properties.png)

>[!INFO]
>
>Répétez les étapes mises en évidence ci-dessus pour que le tableau de bord cible configure une exploration amont à plusieurs niveaux.

## Affichage d’une exploration {#view-drill-through}

Pour afficher une exploration en amont, sélectionnez des points de suspension dans le graphique depuis la vue de votre tableau de bord, puis sélectionnez **[!UICONTROL Drill through]**.

![Graphique affichant le menu représentant des points de suspension avec l’option Exploration amont mise en surbrillance.](../images/sql-insights-query-pro-mode/drill-through-chart-view.png)

Le tableau de bord d&#39;exploration en amont de la cible s&#39;affiche. Vous pouvez répéter cette étape si vous disposez d&#39;une analyse à plusieurs niveaux.

![Tableau de bord cible affiché avec l’exploration en surbrillance.](../images/sql-insights-query-pro-mode/drill-through-target-dashboard.png)

>[!NOTE]
>
>Tous les filtres appliqués dans le tableau de bord source sont transmis au tableau de bord cible. Toutefois, les filtres de date et les filtres globaux sont désactivés sur les tableaux de bord enfants.

## Supprimer une exploration amont {#remove-drill-through}

Pour supprimer une exploration en amont, sélectionnez d’abord **[!UICONTROL Edit]** dans la vue de votre tableau de bord.

![Tableau de bord personnalisé avec l’option Modifier mise en surbrillance.](../images/sql-insights-query-pro-mode/drill-through.png)

Dans le graphique, sélectionnez les points de suspension dont vous souhaitez supprimer une analyse, puis sélectionnez **[!UICONTROL Edit]**.

![Graphique affichant le menu représentant des points de suspension avec l’option Modifier mise en surbrillance.](../images/sql-insights-query-pro-mode/drill-through-chart-edit.png)

Dans le panneau de [!UICONTROL Properties], sélectionnez le bouton (bascule) pour désactiver le **[!UICONTROL Enable drill through]**, puis sélectionnez **[!UICONTROL Save and close]**.

![Panneau Propriétés du graphique avec le bouton (bascule) désactivé pour les [!UICONTROL Enable drill through] en surbrillance.](../images/sql-insights-query-pro-mode/drill-through-disable.png)

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment créer une exploration en amont pour votre tableau de bord. Vous pouvez également apprendre à générer des graphiques à partir de modèles de données existants dans l’interface utilisateur de Adobe Experience Platform à l’aide du [&#x200B; guide du mode de conception guidé &#x200B;](../standard-dashboards.md).
