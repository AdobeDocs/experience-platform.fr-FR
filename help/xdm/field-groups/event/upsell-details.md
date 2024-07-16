---
title: Groupe de champs de schéma de détails de mise à niveau
description: Découvrez le groupe de champs Détails de la mise à niveau .
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Groupe de champs de schéma Détails de mise à niveau]

[!UICONTROL Détails de la mise à niveau] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisée pour capturer des informations concernant un événement marketing de mise à niveau, y compris des détails sur la transaction et les différentes manières dont l’offre s’affichait pour un client.

Le groupe de champs fournit un seul champ de type objet, `upsells`. Les propriétés contenues dans cet objet sont expliquées ci-dessous.

![Structure des détails de mise à niveau](../../images/field-groups/upsell-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `upsellImpressions` | Tableau de [Impressions](../../data-types/impressions.md) | Tableau qui répertorie les impressions enregistrées (vues numériques ou engagements avec l’offre de vente incitative) pour le client. |
| `upsellTransaction` | [Transaction](../../data-types/transaction.md) | Décrit la transaction de devise pour la vente incitative. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
