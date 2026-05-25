---
title: Type de données de paires clé-valeur
description: Découvrez le type de données du modèle de données d’expérience (XDM) des paires clé-valeur.
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
TQID: https://experienceleague.adobe.com/D1O4T-bH4evkFSMsMByQ0LunEIhkN8Ho2hfNeFM--Bs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 104
ht-degree: 50%

---

# Type de données [!UICONTROL Key Value Pair]

[!UICONTROL Key Value Pair] est un type de données standard du modèle de données d’expérience (XDM) qui capture les détails d’une paire clé-valeur générique. Ce type de données est utilisé dans le groupe de champs [&#128279;](../field-groups/event/analytics-full-extension.md) pour décrire les éléments de tableau d’une variable de liste.[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]

![Structure de paire clé-valeur](../images/data-types/key-value-pair.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `key` | Chaîne | Clé (nom) d’une variable ou valeur générique. |
| `value` | Chaîne | Valeur de la variable. |

{style="table-layout:auto"}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
