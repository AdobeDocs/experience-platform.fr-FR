---
solution: Experience Platform
title: Ignorer la mise à jour des contraintes de temps de l’année
description: Découvrez comment résoudre un problème avec la contrainte d’année ignorée.
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
source-git-commit: 006950092f69d378b064c795b117166343e5d8f2
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 8%

---

# Mise à jour de la contrainte temporelle Ignorer l’année {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Mise à jour de Ignorer l’année"
>abstract="La contrainte temporelle Ignorer l’année a été mise à jour. Réenregistrez votre audience."

>[!IMPORTANT]
>
>Vous pouvez uniquement utiliser la contrainte temporelle &quot;ignorer l’année&quot; dans une définition de segment évaluée à l’aide de la **segmentation par lots**. L’ajout de la contrainte temporelle &quot;ignorer l’année&quot; à votre définition de segment rendra l’audience résultante **inéligible** pour la segmentation par flux ou en périphérie.

La version de février 2024 pour Adobe Experience Platform a introduit des modifications dans le service de segmentation Adobe Experience Platform, qui résout un problème lié à l’option &quot;ignorer l’année&quot; dans la création et l’évaluation d’audiences.

L’option &quot;ignorer l’année&quot; est conçue pour ignorer le composant Année d’une date lors de l’évaluation de l’audience. Vous pouvez utiliser cette option dans les cas où la relation temporelle entre différents événements est importante, mais que l’année spécifique n’est pas importante, par exemple dans un champ de date de naissance.

Cependant, au cours des années bissextiles telles que 2024, le système sous-jacent n’a pas géré correctement cette option, ce qui a entraîné des évaluations d’audience inexactes. Par conséquent, si l’option &quot;ignorer l’année&quot; est activée dans une année bissextile, l’évaluation de l’audience échoue un jour.

Si vous avez créé une audience avant la publication de ce correctif, vous devez simplement la réenregistrer dans le créateur de segments pour appliquer le correctif. Si vous ne savez pas si votre audience est affectée par cette résolution, le créateur de segments invite l’utilisateur si l’audience existante est affectée par ce problème.
