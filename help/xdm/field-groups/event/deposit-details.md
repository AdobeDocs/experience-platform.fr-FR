---
title: Groupe de champs de schéma Détails du dépôt
description: Ce document fournit un aperçu du groupe de champs de schéma Détails du dépôt .
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 7%

---

# [!UICONTROL Détails du dépôt] groupe de champs de schéma

[!UICONTROL Détails du dépôt] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Le groupe de champs fournit une `personalFinances.deposits` à un schéma, qui capture les détails d’un dépôt financier.

![](../../images/field-groups/deposit-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `account` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier associé au dépôt. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Décrit la transaction financière associée au dépôt. |
| `mobileDeposit` | [!UICONTROL Booléen] | Indique si le dépôt a été effectué via une plateforme mobile. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
