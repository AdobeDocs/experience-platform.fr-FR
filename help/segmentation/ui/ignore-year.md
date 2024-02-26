---
solution: Experience Platform
title: Ignorer la mise à jour des contraintes de temps de l’année
description: Découvrez comment résoudre un problème avec la contrainte d’année ignorée.
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 9%

---


# Mise à jour de la contrainte temporelle Ignorer l’année {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Mise à jour de Ignorer l’année"
>abstract="La contrainte temporelle Ignorer l’année a été mise à jour. Réenregistrez votre audience."

La version de février 2024 pour Adobe Experience Platform a introduit des modifications dans le service de segmentation Adobe Experience Platform, qui résout un problème lié à l’option &quot;ignorer l’année&quot; dans la création et l’évaluation d’audiences.

L’option &quot;ignorer l’année&quot; est conçue pour ignorer le composant Année d’une date lors de l’évaluation de l’audience. Vous pouvez utiliser cette option dans les cas où la relation temporelle entre différents événements est importante, mais que l’année spécifique n’est pas importante, par exemple dans un champ de date de naissance.

Cependant, au cours des années bissextiles telles que 2024, le système sous-jacent n’a pas géré correctement cette option, ce qui a entraîné des évaluations d’audience inexactes. Par conséquent, si l’option &quot;ignorer l’année&quot; est activée dans une année bissextile, l’évaluation de l’audience échoue un jour.

Si vous avez créé une audience avant la publication de ce correctif, vous devez simplement la réenregistrer dans le créateur de segments pour appliquer le correctif. Si vous ne savez pas si votre audience est affectée par cette résolution, le créateur de segments invite l’utilisateur si l’audience existante est affectée par ce problème.
