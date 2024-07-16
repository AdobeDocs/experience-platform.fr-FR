---
solution: Experience Platform
title: Guide de l’interface utilisateur des contraintes de temps de la segmentation refactorisées
description: Le créateur de segments offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 665bbd1904e857336a4fb677230389d7977f6b60
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 26%

---

# Refactorisation des contraintes de temps {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Refactorisation des contraintes de temps"
>abstract="Les contraintes de temps au niveau de la règle et au niveau du groupe ont été supprimées afin de clarifier l’utilisation des contraintes de temps. Réécrivez votre contrainte en tant que contrainte de temps au niveau de la zone de travail ou de la carte."

La version de janvier 2024 de Adobe Experience Platform a introduit des modifications dans le service de segmentation de Adobe Experience Platform qui ajoutent de nouvelles restrictions aux endroits où des contraintes de temps peuvent être définies. Ces modifications affectent les segments nouvellement créés ou modifiés effectués à l’aide de l’interface utilisateur du créateur de segments. Ce guide explique comment atténuer ces modifications.

Avant la version de janvier 2024, toutes les contraintes temporelles de niveau règle, de niveau groupe et de niveau canevas faisaient référence de manière redondante au même horodatage. Afin de clarifier l’utilisation des contraintes de temps, les contraintes de temps au niveau des règles et des groupes ont été supprimées. Pour tenir compte de cette modification, toutes les contraintes de temps **doivent** être réécrites en tant que contraintes de temps **canvas-level** ou **card-level**.

Auparavant, plusieurs règles de contrainte temporelle pouvaient être associées à un événement individuel. Avec cette mise à jour récente, la tentative d’ajout d’une contrainte temporelle à une règle entraînera désormais une **erreur**.

![La contrainte temporelle au niveau de la règle est mise en surbrillance. L’erreur qui se produit par la suite est également mise en surbrillance. ](../images/ui/segment-refactoring/rule-time-constraint.png)

Les contraintes de temps ne peuvent désormais être appliquées qu’au niveau de la zone de travail ou de la carte.

Lors de l’application d’une contrainte temporelle au niveau de la zone de travail, vous pouvez toujours sélectionner toutes les contraintes temporelles disponibles.

>[!NOTE]
>
>S’il n’y a que **une** carte sur la zone de travail, appliquer la contrainte de temps à la carte est **équivalent** pour appliquer la contrainte de temps au niveau de la zone de travail.
>
>S’il existe **cartes** sur la zone de travail, l’application de la contrainte temporelle au niveau de la zone de travail applique cette contrainte temporelle à toutes les **cartes sur la zone de travail.**

![La contrainte temporelle au niveau de la zone de travail est mise en surbrillance.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Pour appliquer une contrainte temporelle au niveau de la carte, sélectionnez la carte spécifique à laquelle vous souhaitez appliquer la contrainte temporelle. Le conteneur **[!UICONTROL Règles d’événement]** s’affiche. Vous pouvez maintenant sélectionner la contrainte temporelle à appliquer à la carte.

![La contrainte temporelle au niveau de la carte est mise en surbrillance.](../images/ui/segment-refactoring/card-time-constraint.png)
