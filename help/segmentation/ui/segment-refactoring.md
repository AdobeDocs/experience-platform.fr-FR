---
solution: Experience Platform
title: Guide de l’interface utilisateur des contraintes de temps de la segmentation refactorisées
description: Le créateur de segments offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 100%

---

# Refactorisation des contraintes de temps

La version d’octobre 2020 d’Adobe Experience Platform a introduit des modifications de performances dans Adobe Experience Platform Segmentation Service, qui ajoutent de nouvelles restrictions à l’utilisation des opérateurs logiques OR et AND. Ces modifications concerneront les segments nouvellement créés ou modifiés à l’aide de l’interface utilisateur du créateur de segments. Ce guide explique comment atténuer ces modifications.

Avant la version d’octobre 2020, toutes les contraintes de temps au niveau des règles, des groupes et des événements faisaient référence de manière redondante à la même date et heure. Afin de clarifier l’utilisation des contraintes de temps, les contraintes de temps au niveau des règles et des groupes ont été supprimées. Pour tenir compte de ce changement, toutes les contraintes de temps doivent être réécrites en tant que contraintes de temps au niveau des événements.

Auparavant, un événement individuel pouvait être associé à plusieurs règles de contrainte de temps.

![L’ancien style des contraintes de temps est mis en surbrillance dans le créateur de segments.](../images/ui/segment-refactoring/former-time-constraint.png)

Comme vous pouvez le constater, ce segment présente deux contraintes au niveau de la règle : Un pour « [!UICONTROL Aujourd’hui] » et l’autre pour « [!UICONTROL Hier] ».

Le segment précédent est équivalent au segment suivant : les deux contraintes de temps au niveau de l’événement ont été connectées à l’aide d’un opérateur AND. La première contrainte de temps au niveau de l’événement fait référence à un événement de clic dont le nom est « Training » et qui se produit aujourd’hui, tandis que la deuxième contrainte de temps au niveau de l’événement fait référence à un événement de clic dont le nom est « Pets » et qui s’est produit hier.

![Le nouveau style des contraintes de temps est mis en surbrillance dans le créateur de segments.](../images/ui/segment-refactoring/time-constraint-1.png) ![Le nouveau style des contraintes de temps est mis en surbrillance dans le créateur de segments.](../images/ui/segment-refactoring/time-constraint-2.png)

Cette refactorisation des contraintes de temps affecte également les contraintes de temps qui sont connectées à l’aide d’un opérateur OR.
