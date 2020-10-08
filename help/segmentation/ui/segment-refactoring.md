---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment builder;Segment builder
solution: Experience Platform
title: Guide de modification du créateur de segments de service de segmentation
topic: ui guide
description: 'Le créateur de segments offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données. '
translation-type: tm+mt
source-git-commit: beacce03136e1620ff57fb549f335d2199bb6001
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 13%

---


# Réfactorisation des contraintes de temps

La version d’octobre 2020 pour Adobe Experience Platform a introduit des modifications de performances dans Adobe Experience Platform Segmentation Service, qui ajoutent de nouvelles restrictions à l’utilisation des opérateurs logiques OU et ET. Ces modifications affecteront les segments nouvellement créés ou modifiés créés à l’aide de l’interface utilisateur du créateur de segments. Ce guide explique comment atténuer ces changements.

Avant la version d’octobre 2020, toutes les contraintes de temps au niveau des règles, des groupes et des événements faisaient référence de manière redondante au même horodatage. Afin de clarifier l&#39;utilisation des contraintes de temps, les contraintes de temps au niveau des règles et au niveau des groupes ont été supprimées. Pour tenir compte de ce changement, toutes les contraintes de temps doivent être réécrites en contraintes de temps au niveau du événement.

Auparavant, plusieurs règles de contrainte de temps pouvaient être associées à un événement individuel.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Comme vous pouvez le constater, ce segment présente deux contraintes au niveau des règles : L&#39;un pour &quot;[!UICONTROL Aujourd&#39;hui]&quot; et l&#39;autre pour &quot;[!UICONTROL Hier]&quot;.

Le segment précédent est équivalent au segment suivant : les deux contraintes de temps au niveau du événement ont été connectées à l’aide d’un opérateur ET. La première contrainte de temps de niveau événement fait référence à un événement de clics dont le nom est égal à &quot;Formation&quot; et se produit aujourd’hui, tandis que la seconde contrainte de temps de niveau événement fait référence à un événement de clics dont le nom est égal à &quot;Animaux de compagnie&quot; et qui s’est produite hier.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Cette refactorisation des contraintes de temps affecte également les contraintes de temps qui sont connectées à l’aide d’un opérateur OU.