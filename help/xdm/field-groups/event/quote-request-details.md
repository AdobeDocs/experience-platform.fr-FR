---
title: Groupe de champs de schéma des détails de demande de devis
description: Découvrez le groupe de champs de schéma Détails de la demande de devis.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
TQID: https://experienceleague.adobe.com/etiH-gznPetXYziBrel1CnXhINKNsCbCZQicBz7eKVE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 137
ht-degree: 2%

---

# [!UICONTROL Quote Request Details] groupe de champs de schéma

[!UICONTROL Quote Request Details] groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un seul objet `quotes` à un schéma, qui capture les détails du processus de demande pour divers types de devis, y compris les polices d&#39;assurance, les soins de santé, les ordres de fabrication et les commandes high-tech.

![](../../images/field-groups/quote-request-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `discount` | [[!UICONTROL Currency]](../../data-types/currency.md) | Montant de la remise pour un devis présenté à un visiteur ou une visiteuse. |
| `premium` | [[!UICONTROL Currency]](../../data-types/currency.md) | Montant de la prime d’un devis présenté à un visiteur ou une visiteuse. |
| `location` | [!UICONTROL String] | Code postal utilisé pour rechercher des revendeurs à proximité de la position du visiteur. |
| `requestID` | [!UICONTROL String] | Identifiant unique de la demande de devis. |
| `selectedRetailer` | [!UICONTROL String] | Retailer sélectionnée pour la demande de devis, le cas échéant. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
