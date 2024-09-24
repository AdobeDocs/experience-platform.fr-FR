---
title: Exploration du mode Query Pro
description: Découvrez comment naviguer de n’importe quel graphique vers un nouveau tableau de bord pour explorer vos données à l’aide de l’analyse.
source-git-commit: d851f7b1ac9b2fda5297cf752013c2ffb775e33d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Exploration {#drill-through}

Les analyses avancées facilitent l’analyse de données à plusieurs niveaux en facilitant la navigation entre n’importe quel graphique et un nouveau tableau de bord. Grâce à cette fonctionnalité, vous pouvez facilement passer d’aperçus de haut niveau à des rapports détaillés lors de l’étude des tendances, du comportement des clients, des indicateurs opérationnels, etc., en vous assurant que vous disposez toujours du contexte dont vous avez besoin.

Le système garantit que l’analyse que vous commencez se poursuit en toute transparence tout au long de l’expérience d’analyse approfondie en transmettant automatiquement les filtres globaux et les filtres de période depuis les tableaux de bord sources vers les tableaux de bord cibles. Pour faciliter la navigation entre les différentes couches de l’étude, le système permet des explorations à plusieurs niveaux.

## Création d’une analyse {#create-drill-through}

Pour créer une analyse, commencez par sélectionner **[!UICONTROL Modifier]** dans la vue de votre tableau de bord.

![Tableau de bord personnalisé avec modification mise en surbrillance.](../../images/query-pro-mode/drill-through.png)

Sélectionnez les points de suspension dans le graphique que vous souhaitez parcourir, puis sélectionnez **[!UICONTROL Modifier]**.

![Graphique montrant le menu de points de suspension avec l’option Modifier mise en surbrillance.](../../images/query-pro-mode/drill-through-chart-edit.png)

Dans le panneau [!UICONTROL Propriétés], activez l’option **[!UICONTROL pour activer l’analyse]**, puis utilisez la liste déroulante pour sélectionner le **[!UICONTROL tableau de bord Target]**. Assurez-vous que le bouton bascule de **[!UICONTROL Filtrer le pass-through]** est activé, puis sélectionnez **[!UICONTROL Enregistrer et fermer]**.

![ Panneau des propriétés de graphique avec l’option Autoriser l’analyse, le tableau de bord de la cible et la fonction Filtrer mise en surbrillance.](../../images/query-pro-mode/drill-through-chart-properties.png)

>[!INFO]
>
>Répétez les étapes indiquées ci-dessus pour que le tableau de bord cible configure une analyse à plusieurs niveaux.

## Affichage d’une analyse {#view-drill-through}

Pour afficher une analyse, sélectionnez des points de suspension dans le graphique dans la vue de votre tableau de bord, puis sélectionnez **[!UICONTROL Exploration]**.

![Graphique montrant le menu de points de suspension avec l’option Exploration mise en surbrillance.](../../images/query-pro-mode/drill-through-chart-view.png)

Le tableau de bord de l’analyse de la cible s’affiche. Vous pouvez répéter cette étape si vous effectuez des explorations à plusieurs niveaux.

![Le tableau de bord de la cible s’affiche avec l’analyse en surbrillance.](../../images/query-pro-mode/drill-through-target-dashboard.png)

>[!NOTE]
>
>Tous les filtres appliqués dans le tableau de bord source sont transmis au tableau de bord cible. Toutefois, les filtres de date et globaux sont désactivés sur les tableaux de bord enfants.

## Suppression d’une analyse {#remove-drill-through}

Pour supprimer une analyse, commencez par sélectionner **[!UICONTROL Modifier]** dans la vue de votre tableau de bord.

![Tableau de bord personnalisé avec modification mise en surbrillance.](../../images/query-pro-mode/drill-through.png)

Sélectionnez les points de suspension dans le graphique que vous souhaitez supprimer d’une analyse, puis sélectionnez **[!UICONTROL Modifier]**.

![Graphique montrant le menu de points de suspension avec l’option Modifier mise en surbrillance.](../../images/query-pro-mode/drill-through-chart-edit.png)

Dans le panneau [!UICONTROL Propriétés], sélectionnez le bouton d’activation/désactivation de **[!UICONTROL Activer l’analyse]**, puis sélectionnez **[!UICONTROL Enregistrer et fermer]**.

![Panneau des propriétés de graphique avec bouton d’activation/désactivation désactivé pour [!UICONTROL Activer l’analyse ] mise en surbrillance.](../../images/query-pro-mode/drill-through-disable.png)

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment créer une analyse pour votre tableau de bord. Vous pouvez également apprendre à générer des graphiques à partir de modèles de données existants dans l’interface utilisateur de Adobe Experience Platform avec le [guide de mode de conception guidé](../../user-defined-dashboards.md).
