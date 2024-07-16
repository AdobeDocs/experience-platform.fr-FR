---
title: Type de données du compte financier
description: Découvrez le type de données XDM du compte financier.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 8%

---

# Type de données [!UICONTROL Compte financier]

[!UICONTROL Compte financier] est un type de données XDM standard qui décrit les détails d’un compte financier, y compris son type, son propriétaire et son solde actuel.

![](../images/data-types/financial-account.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Devise]](./currency.md) | Solde actuel du compte. |
| `financialAccountId` | [!UICONTROL Chaîne] | Identifiant unique du compte. |
| `financialAccountName` | [!UICONTROL Chaîne] | Nom attribué au compte. |
| `financialAccountType` | [!UICONTROL Chaîne] | Type de compte financier, tel que le contrôle, l’épargne ou la retraite. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
