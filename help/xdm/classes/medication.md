---
title: Classe de médicaments
description: Découvrez la classe de médicaments dans le modèle de données d’expérience (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# Classe [!UICONTROL Medication]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Medication] capture l’ensemble minimal de propriétés qui définissent une substance utilisée pour le traitement médical, en particulier un médicament ou un médicament.

![Structure de classe](../images/classes/medication.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Comme ce champ est généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `medicationId` | [!UICONTROL Chaîne] | Identifiant unique du médicament. |
| `medicationName` | [!UICONTROL Chaîne] | Nom du médicament. |

{style="table-layout:auto"}

La classe peut être étendue avec le groupe de champs [[!UICONTROL Healthcare médication]](../field-groups/medication/healthcare-medication.md) pour décrire plus de détails sur le médicament ou le médicament.
