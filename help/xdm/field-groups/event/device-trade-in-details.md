---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;ExperienceEvent;champs;schémas;Schémas;Conception de schéma;groupe de champs;groupe de champs;appareil;reprise;reprise;reprise;
solution: Experience Platform
title: Groupe De Champs De Schéma Détails D’Échange D’Appareil
description: Découvrez le groupe de champs de schéma Détails d’échange de l’appareil.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
TQID: https://experienceleague.adobe.com/NhBB-oG1xiDvcoAfUTHkiGS9Pl0pozOdWMUsD7e67pc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 192
ht-degree: 14%

---

# [!UICONTROL Détails d’échange de l’appareil] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Device Trade-In Details] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il fournit un champ unique (`deviceTradeInDetails`) qui décrit une transaction d’échange d’appareil, y compris la valeur d’échange, l’identifiant d’appareil d’origine et le nouvel identifiant d’appareil.

![Structure des détails de reprise d’appareil](../../images/field-groups/device-trade-in-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `tradeInValue` | [Devise](../../data-types/currency.md) | Valeur de l’appareil échangé. |
| `newDeviceID` | Chaîne | Identifiant du nouvel appareil échangé. |
| `originalDeviceID` | Chaîne | Identifiant de l’appareil échangé. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
