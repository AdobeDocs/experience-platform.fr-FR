---
title: Groupe de champs de schéma des transferts de solde
description: Ce document présente la vue d'ensemble du groupe de champs du schéma Transferts de solde .
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 7%

---

# [!UICONTROL Transferts de solde] groupe de champs de schéma

[!UICONTROL Transferts de solde] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Le groupe de champs fournit une `personalFinances.balanceTransfers` à un schéma, qui capture les détails d’un transfert de solde financier entre des comptes.

![](../../images/field-groups/balance-transfers.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier à partir duquel le solde est transféré. |
| `accountTo` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier vers lequel le solde est transféré. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Décrit la transaction financière associée au transfert du solde. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
