---
title: Type de données de compte financier
description: Découvrez le type de données XDM du compte financier.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
TQID: https://experienceleague.adobe.com/0875971XiCjyzYMWUQR6m5eWRB4yKjaW2aJPKVep7EE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 100
ht-degree: 8%

---

# Type de données [!UICONTROL Compte financier]

[!UICONTROL Compte financier] est un type de données XDM standard qui décrit les détails d’un compte financier, notamment son type, son propriétaire et son solde actuel.

![](../images/data-types/financial-account.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Devise]](./currency.md) | Solde actuel du compte. |
| `financialAccountId` | [!UICONTROL Chaîne] | ID unique du compte. |
| `financialAccountName` | [!UICONTROL Chaîne] | Nom attribué au compte. |
| `financialAccountType` | [!UICONTROL Chaîne] | Type de compte financier, tel que compte chèques, compte d’épargne ou compte de retraite. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
