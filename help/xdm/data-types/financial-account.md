---
title: Type de données du compte financier
description: Ce document présente un aperçu du type de données XDM du compte financier.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 10%

---

# [!UICONTROL Compte financier] type de données

[!UICONTROL Compte financier] est un type de données XDM standard qui décrit les détails d’un compte financier, y compris son type, son propriétaire et son solde actuel.

![](../images/data-types/financial-account.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Devise]](./currency.md) | Solde actuel du compte. |
| `financialAccountId` | [!UICONTROL Chaîne] | Identifiant unique du compte. |
| `financialAccountName` | [!UICONTROL Chaîne] | Nom attribué au compte. |
| `financialAccountType` | [!UICONTROL Chaîne] | Type de compte financier, tel que le contrôle, l’épargne ou la retraite. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
