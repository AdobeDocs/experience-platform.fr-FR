---
title: Groupe de champs de schéma Détails du dépôt
description: Découvrez le groupe de champs de schéma Détails du dépôt .
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 4%

---

# [!UICONTROL Détails du dépôt] groupe de champs de schéma

[!UICONTROL Deposit Details] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un champ `personalFinances.deposits` unique à un schéma, qui capture les détails sur un dépôt financier.

![](../../images/field-groups/deposit-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `account` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier associé au dépôt. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Décrit la transaction financière associée au dépôt. |
| `mobileDeposit` | [!UICONTROL Booléen] | Indique si le dépôt a été effectué via une plateforme mobile. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
