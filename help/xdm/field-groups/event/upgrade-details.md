---
title: Groupe de champs de schéma des détails de mise à niveau
description: Découvrez le groupe de champs de schéma Détails de mise à niveau .
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
TQID: https://experienceleague.adobe.com/v0SpTekNz7uk9qRdDVvATGYqcvka6YtzfGkweF4DT44
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 157
ht-degree: 2%

---

# [!UICONTROL Détails de mise à niveau] groupe de champs de schéma

[!UICONTROL Détails de la mise à niveau] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisé pour capturer des informations concernant un événement marketing de mise à niveau, y compris des détails sur la transaction et les différentes manières dont l’offre a été présentée à un client.

Le groupe de champs fournit un seul champ de type objet, `upgrades`. Les propriétés contenues dans cet objet sont expliquées ci-dessous.

![Structure des détails de la mise à niveau](../../images/field-groups/upgrade-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `upgradeImpressions` | Tableau d’[impressions](../../data-types/impressions.md) | Tableau qui répertorie les impressions enregistrées (vues numériques ou engagements avec l’offre de mise à niveau) pour le client. |
| `upgradeTransaction` | [ Transaction ](../../data-types/transaction.md) | Décrit la transaction de devise pour la mise à niveau. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
