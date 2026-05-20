---
title: Segmentation d’entités multiples avec segmentation B2B
description: Découvrez comment créer une audience évaluée à l’aide de la segmentation en flux continu qui contient une entité B2B.
source-git-commit: eafbf2180f1cbf5db932d0f4dfaa21a4276098ab
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# Segmentation par flux continu d’entités multiples

La segmentation d’entités multiples vous permet de faire référence à des entités B2B dans votre définition d’audience. Auparavant, vous pouviez combiner les deux entités B2B avec des événements de diffusion en continu dans une seule audience.

Par exemple, la création d’une audience telle que la suivante, qui comporte **à la fois** un attribut B2B et un événement de diffusion en continu dans une seule audience n’est **pas prise en charge**.

![Définition de segment non valide qui combine une entité B2B avec un événement de diffusion en continu.](/help/rtcdp/assets/segmentation/multi-entity/invalid.png)

Pour combiner des entités B2B avec des événements de diffusion en continu, vous devez créer **trois** audiences et effectuer une segmentation en flux continu d’entités multiples : l’une contenant la logique de segmentation en flux continu, l’autre contenant l’entité B2B et l’autre qui combine les deux audiences.

Un exemple d’audience de diffusion en continu d’entités multiples serait une audience qui recherche toutes les personnes-comptes du secteur de la santé pour avoir une page vue au cours du dernier jour.

L’audience qui contient l’entité B2B se présenterait comme suit, avec **uniquement** l’attribut B2B dans la définition. Cette audience est évaluée à l’aide de la segmentation **par lots**.

![Audience qui contient uniquement l’entité B2B.](/help/rtcdp/assets/segmentation/multi-entity/attribute.png)

L’audience qui contient l’événement de diffusion en continu se présenterait comme suit, avec **uniquement** un événement de diffusion en continu dans la définition. Cette audience est évaluée à l’aide de la segmentation **streaming**.

![Audience qui contient uniquement l’événement de diffusion en continu.](/help/rtcdp/assets/segmentation/multi-entity/event.png)

Après avoir créé les deux audiences de composant, vous devez créer une audience qui **inclut** les deux audiences constitutives. Cette audience combinée est évaluée à l’aide de la segmentation **en flux continu**.

![Audience qui combine à la fois l’audience de l’entité B2B et l’audience de l’événement de streaming.](/help/rtcdp/assets/segmentation/multi-entity/combined.png)
