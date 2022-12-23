---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;créateur de segments;créateur de segments
solution: Experience Platform
title: Guide de l’interface utilisateur des contraintes de temps de segmentation restructurée
topic-legacy: ui guide
description: Le créateur de segments offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 681418b4198c2b1303fda937c3ffc60dad21b672
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 11%

---

# Refactorisation des contraintes de temps

La version d’octobre 2020 pour Adobe Experience Platform a introduit des modifications de performances dans Adobe Experience Platform Segmentation Service, qui ajoutent de nouvelles restrictions à l’utilisation des opérateurs logiques OR et AND. Ces modifications concerneront les segments nouvellement créés ou modifiés effectués à l’aide de l’interface utilisateur du créateur de segments. Ce guide explique comment atténuer ces modifications.

Avant la version d’octobre 2020, toutes les contraintes temporelles au niveau des règles, des groupes et des événements faisaient référence de manière redondante au même horodatage. Afin de clarifier l’utilisation des contraintes de temps, les contraintes de temps au niveau de la règle et au niveau du groupe ont été supprimées. Pour tenir compte de cette modification, toutes les contraintes de temps doivent être réécrites en tant que contraintes de temps au niveau de l’événement.

Auparavant, plusieurs règles de contrainte temporelle pouvaient être associées à un événement individuel.

![L’ancien style des contraintes temporelles est mis en surbrillance dans le créateur de segments.](../images/ui/segment-refactoring/former-time-constraint.png)

Comme vous pouvez le constater, ce segment présente deux contraintes au niveau de la règle : Un pour &quot;[!UICONTROL Aujourd&#39;hui]&quot; et l’autre pour &quot;[!UICONTROL Hier]&quot;.

Le segment précédent est équivalent au segment suivant : les deux contraintes de temps au niveau de l’événement ont été connectées à l’aide d’un opérateur AND. La première contrainte temporelle de niveau événement fait référence à un événement de clic dont le nom est égal à &quot;Formation&quot; et se produit aujourd’hui, tandis que la seconde contrainte temporelle de niveau événement fait référence à un événement de clic dont le nom est égal à &quot;Animaux&quot; et qui s’est produit hier.

![Le nouveau style des contraintes temporelles est mis en surbrillance dans le créateur de segments.](../images/ui/segment-refactoring/time-constraint-1.png) ![Le nouveau style des contraintes temporelles est mis en surbrillance dans le créateur de segments.](../images/ui/segment-refactoring/time-constraint-2.png)

Cette refactorisation des contraintes de temps affecte également les contraintes de temps qui sont connectées à l’aide d’un opérateur OU.
