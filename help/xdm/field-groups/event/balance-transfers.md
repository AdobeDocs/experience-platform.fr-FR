---
title: Groupe de champs de schéma des transferts de solde
description: Découvrez le groupe de champs de schéma Transferts de solde .
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# [!UICONTROL Transferts de solde] groupe de champs de schéma

[!UICONTROL Transferts de solde] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un seul objet `personalFinances.balanceTransfers` à un schéma, qui capture les détails d’un transfert de la balance financière entre les comptes.

![](../../images/field-groups/balance-transfers.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier à partir duquel le solde est transféré. |
| `accountTo` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier vers lequel le solde est transféré. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Décrit la transaction financière associée au transfert du solde. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
