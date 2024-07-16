---
title: Groupe de champs de schéma de détails de mise à niveau
description: Découvrez le groupe de champs Détails de la mise à niveau .
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# Groupe de champs de schéma [!UICONTROL Détails de la mise à niveau]

[!UICONTROL Détails de la mise à niveau] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisée pour capturer des informations concernant un événement marketing de mise à niveau, y compris des détails sur la transaction et les différentes manières dont l’offre s’affichait pour un client.

Le groupe de champs fournit un seul champ de type objet, `upgrades`. Les propriétés contenues dans cet objet sont expliquées ci-dessous.

![Structure des détails de la mise à niveau](../../images/field-groups/upgrade-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `upgradeImpressions` | Tableau de [Impressions](../../data-types/impressions.md) | Tableau qui répertorie les impressions enregistrées (vues numériques ou engagements avec l’offre de mise à niveau) pour le client. |
| `upgradeTransaction` | [Transaction](../../data-types/transaction.md) | Décrit la transaction de devise pour la mise à niveau. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
