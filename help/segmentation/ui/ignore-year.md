---
solution: Experience Platform
title: Ignorer la mise à jour de la contrainte de temps d'année
description: Découvrez comment résoudre un problème lié à la contrainte de temps Ignorer l’année .
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
TQID: https://experienceleague.adobe.com/YlDmagm4R89atrkwq3vq7zlAdZztLrWub63akfpa-uo
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: dc8284dbcac9762b1513a50bb759f537f828d617
workflow-type: tm+mt
source-wordcount: 246
ht-degree: 8%

---

# Mise à jour de la contrainte temporelle Ignorer l’année {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Mise à jour de Ignorer l’année"
>abstract="La contrainte temporelle Ignorer l’année a été mise à jour. Réenregistrez votre audience."

>[!IMPORTANT]
>
>Vous pouvez uniquement utiliser la contrainte de temps « ignorer l’année » dans une définition de segment évaluée à l’aide de la **segmentation par lots**. L’ajout de la contrainte de temps « ignorer l’année » à votre définition de segment rendra l’audience obtenue **inéligible** pour la segmentation en flux continu ou Edge.

La version de février 2024 de Adobe Experience Platform a introduit des modifications dans Adobe Experience Platform Segmentation Service qui résout un problème avec l’option « ignorer l’année » dans la création et l’évaluation d’audiences.

L’option « ignorer l’année » est conçue pour ignorer le composant d’année d’une date lors de l’exécution des évaluations d’audience. Vous pouvez utiliser cette option dans les situations où la relation temporelle entre différents événements est importante, mais où l’année spécifique n’est pas importante, comme un champ de date de naissance.

Cependant, au cours des années bissextiles comme 2024, le système sous-jacent n’a pas géré correctement cette option, ce qui a entraîné des évaluations d’audience inexactes. Par conséquent, si l’option « ignorer l’année » est activée au cours d’une année bissextile, l’évaluation de l’audience manquerait un jour.

Si vous avez créé une audience avant la publication de ce correctif, il vous suffit de réenregistrer l’audience dans le créateur de segments pour appliquer le correctif. Si vous ne savez pas si votre audience est affectée par cette résolution, le créateur de segments demandera à l’utilisateur si l’audience existante est affectée par ce problème.
