---
title: Type de données de paires clé-valeur
description: Découvrez le type de données XDM (Key Value Pair Experience Data Model).
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 88%

---

# Type de données des [!UICONTROL Paires clé-valeur]

Une [!UICONTROL paire clé-valeur] est un type de données standard des modèles de données d’expérience (XDM) qui capture les détails d’une paire clé-valeur générique. Ce type de données est utilisé dans le groupe de champs de l’[[!UICONTROL Extension complète Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md) pour décrire les éléments du tableau d’une variable de liste.

![Structure de paire clé-valeur](../images/data-types/key-value-pair.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `key` | Chaîne | Clé (nom) d’une variable ou valeur générique. |
| `value` | Chaîne | Valeur de la variable. |

{style="table-layout:auto"}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
