---
title: Classe Plan
description: Découvrez la classe Plan dans le modèle de données d’expérience (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# Classe [!UICONTROL Plan]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Plan] capture l’ensemble minimal de propriétés qui définissent un plan, comme un plan d’assurance ou un plan d’assurance.

![Structure de classe](../images/classes/plan.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Comme ce champ est généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `planId` | [!UICONTROL Chaîne] | Identifiant unique du plan. |
| `planName` | [!UICONTROL Chaîne] | Nom du plan. |

{style="table-layout:auto"}

La classe peut être étendue avec le groupe de champs [[!UICONTROL Détails du plan de santé]](../field-groups/plan/healthcare-plan-details.md) pour décrire plus de détails sur un plan d’assurance maladie.
