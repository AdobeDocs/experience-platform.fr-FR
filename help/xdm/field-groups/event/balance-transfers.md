---
title: Groupe de champs de schéma Transferts de solde
description: Découvrez le groupe de champs du schéma Transferts de solde.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
TQID: https://experienceleague.adobe.com/lDicLKYOQvOOPKBURFIUm5267guI6HuDijYuFflMoUs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 116
ht-degree: 3%

---

# [!UICONTROL Transferts de solde] groupe de champs de schéma

[!UICONTROL Transferts de solde] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un seul objet `personalFinances.balanceTransfers` à un schéma, qui capture les détails d’un transfert de solde financier entre les comptes.

![](../../images/field-groups/balance-transfers.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier à partir duquel le solde est transféré. |
| `accountTo` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier vers lequel le solde est transféré. |
| `transaction` | [[!UICONTROL &#x200B; Transaction &#x200B;]](../../data-types/transaction.md) | Décrit la transaction financière associée au transfert de solde. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
