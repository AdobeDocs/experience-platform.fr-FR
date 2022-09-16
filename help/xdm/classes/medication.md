---
title: Classe de médicaments
description: Ce document présente la classe de médicaments dans le modèle de données d’expérience (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---

# [!UICONTROL Médicaments] class

Dans le modèle de données d’expérience (XDM), la variable [!UICONTROL Médicaments] La classe capture l&#39;ensemble minimal de propriétés qui définissent une substance utilisée pour un traitement médical, en particulier un médicament ou un médicament.

![Structure de classe](../images/classes/medication.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `medicationId` | [!UICONTROL Chaîne] | Identifiant unique du médicament. |
| `medicationName` | [!UICONTROL Chaîne] | Nom du médicament. |

{style=&quot;table-layout:auto&quot;}

La classe peut être étendue à l’aide de la fonction [[!UICONTROL Médicaments de santé] groupe de champs](../field-groups/medication/healthcare-medication.md) pour décrire plus en détail le médicament ou le médicament.
