---
title: Groupe de champs de schéma des détails du dépôt
description: Découvrez le groupe de champs de schéma Détails du dépôt .
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
TQID: https://experienceleague.adobe.com/th7pPsJEEuH5ZzBw89JUgxQ05BeEGTRIN9S1CvqcIPI
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 109
ht-degree: 3%

---

# [!UICONTROL Détails du dépôt] groupe de champs de schéma

[!UICONTROL Détails du dépôt] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un champ de `personalFinances.deposits` unique à un schéma, qui capture les détails d’un dépôt financier.

![](../../images/field-groups/deposit-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `account` | [[!UICONTROL Compte financier]](../../data-types/financial-account.md) | Décrit le compte financier associé au dépôt. |
| `transaction` | [[!UICONTROL  Transaction ]](../../data-types/transaction.md) | Décrit la transaction financière associée au dépôt. |
| `mobileDeposit` | [!UICONTROL booléen] | Indique si le dépôt a été effectué via une plateforme mobile. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
