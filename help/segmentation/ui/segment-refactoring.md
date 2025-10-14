---
solution: Experience Platform
title: Guide de l’interface utilisateur des contraintes de temps de la segmentation refactorisées
description: Le créateur de segments offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.
hidefromtoc: true
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: c7d71113ddcef6aca8b2637814b46e589a6b7fdf
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 26%

---

# Refactorisation des contraintes de temps {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Refactorisation des contraintes de temps"
>abstract="Les contraintes de temps au niveau de la règle et au niveau du groupe ont été supprimées afin de clarifier l’utilisation des contraintes de temps. Réécrivez votre contrainte en tant que contrainte de temps au niveau de la zone de travail ou de la carte."

La version de janvier 2024 de Adobe Experience Platform a introduit des modifications dans Adobe Experience Platform Segmentation Service qui ajoutent de nouvelles restrictions aux emplacements où les contraintes de temps peuvent être définies. Ces modifications affectent les segments nouvellement créés ou modifiés à l’aide de l’interface utilisateur du créateur de segments. Ce guide explique comment atténuer ces modifications.

Avant la version de janvier 2024, toutes les contraintes de temps au niveau des règles, des groupes et de la zone de travail faisaient référence de manière redondante à la même date et heure. Afin de clarifier l’utilisation des contraintes de temps, les contraintes de temps au niveau des règles et des groupes ont été supprimées. Pour tenir compte de cette modification, toutes les contraintes de temps **doivent** doivent être réécrites sous la forme de contraintes de temps **au niveau de la zone de travail** ou **au niveau de la carte**.

Auparavant, un événement individuel pouvait être associé à plusieurs règles de contrainte de temps. Avec cette mise à jour récente, toute tentative d’ajout d’une contrainte de temps à une règle entraîne désormais une **erreur**.

![La contrainte de temps au niveau de la règle est mise en surbrillance. L’erreur qui se produit ensuite est également mise en surbrillance. &#x200B;](../images/ui/segment-refactoring/rule-time-constraint.png)

Les contraintes de temps ne peuvent désormais être appliquées qu’au niveau de la zone de travail ou de la carte.

Lors de l’application d’une contrainte de temps au niveau de la zone de travail, vous pouvez toujours sélectionner toutes les contraintes de temps disponibles.

>[!NOTE]
>
>S’il n’existe qu’une seule carte **one** sur la zone de travail, l’application de la contrainte de temps à la carte est **équivalente** à l’application de la contrainte de temps au niveau de la zone de travail.
>
>S’il y a **plusieurs** cartes sur la zone de travail, l’application de la contrainte de temps au niveau de la zone de travail appliquera cette contrainte de temps à **toutes** cartes sur la zone de travail.

![La contrainte de temps au niveau de la zone de travail est mise en surbrillance.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Pour appliquer une contrainte de temps au niveau de la carte, sélectionnez la carte spécifique à laquelle vous souhaitez appliquer la contrainte de temps. Le conteneur **[!UICONTROL Règles d’événement]** s’affiche. Vous pouvez maintenant sélectionner la contrainte de temps que vous souhaitez appliquer à la carte.

![La contrainte de temps au niveau de la carte est mise en surbrillance.](../images/ui/segment-refactoring/card-time-constraint.png)
