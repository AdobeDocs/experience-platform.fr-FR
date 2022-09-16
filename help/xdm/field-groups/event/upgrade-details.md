---
title: Groupe de champs de schéma de détails de mise à niveau
description: Ce document présente un aperçu du groupe de champs de schéma Détails de la mise à niveau .
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 5%

---

# [!UICONTROL Détails de la mise à niveau] groupe de champs de schéma

[!UICONTROL Détails de la mise à niveau] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) utilisé pour capturer des informations concernant un événement marketing de mise à niveau, notamment des détails sur la transaction et les différentes manières dont l’offre s’affichait pour un client.

Le groupe de champs fournit un champ de type objet unique, `upgrades`. Les propriétés contenues dans cet objet sont expliquées ci-dessous.

![Structure des détails de la mise à niveau](../../images/field-groups/upgrade-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `upgradeImpressions` | Tableau de [Impressions](../../data-types/impressions.md) | Tableau qui répertorie les impressions enregistrées (vues numériques ou engagements avec l’offre de mise à niveau) pour le client. |
| `upgradeTransaction` | [Transaction](../../data-types/transaction.md) | Décrit la transaction de devise pour la mise à niveau. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
