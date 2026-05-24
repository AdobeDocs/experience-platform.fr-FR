---
title: Groupe de champs de schéma des détails de montée en gamme
description: Découvrez le groupe de champs de schéma Détails de la montée en gamme.
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
TQID: https://experienceleague.adobe.com/HX-YandWDKSNs-zv2vRCtzYZGZ6r6q0egjC7N2-zUNg
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 153
ht-degree: 2%

---

# [!UICONTROL Upsell Details] groupe de champs de schéma

[!UICONTROL Upsell Details] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisé pour capturer des informations concernant un événement marketing de montée en gamme, y compris des détails sur la transaction et les différentes manières dont l’offre a été présentée à un client.

Le groupe de champs fournit un seul champ de type objet, `upsells`. Les propriétés contenues dans cet objet sont expliquées ci-dessous.

![Structure des détails de la montée en gamme](../../images/field-groups/upsell-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `upsellImpressions` | Tableau d’[impressions](../../data-types/impressions.md) | Tableau qui répertorie les impressions enregistrées (vues numériques ou engagements avec l’offre de montée en gamme) pour le client. |
| `upsellTransaction` | [ Transaction ](../../data-types/transaction.md) | Décrit la transaction de devise pour la vente incitative. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
