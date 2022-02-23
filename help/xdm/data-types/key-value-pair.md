---
title: Type de données de paires de valeurs clés
description: Ce document présente un aperçu du type de données XDM (Key Value Pair Experience Data Model).
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 7%

---

# [!UICONTROL Paire de valeurs clés] type de données

[!UICONTROL Paire de valeurs clés] est un type de données XDM (Experience Data Model) standard qui capture les détails d’une paire clé-valeur générique. Ce type de données est utilisé dans la variable [[!UICONTROL Extension complète Adobe Analytics ExperienceEvent] groupe de champs](../field-groups/event/analytics-full-extension.md) pour décrire les éléments de tableau d’une variable list .

![Structure de paires de valeurs clés](../images/data-types/key-value-pair.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `key` | Chaîne | Clé (nom) pour une variable ou une valeur générique. |
| `value` | Chaîne | La valeur de la variable. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous à la section [le référentiel XDM public ;](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
