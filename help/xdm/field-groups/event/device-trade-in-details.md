---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;appareil;commerce;échange;échange
solution: Experience Platform
title: Groupe de champs de schéma Détails sur l’entrée du périphérique
description: Découvrez le groupe de champs Détails sur le commerce de l’appareil .
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 18%

---

# [!UICONTROL  Groupe de champs de schéma Détails sur le commerce d’appareil ]

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Device Trade-In Details] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il fournit un champ unique (`deviceTradeInDetails`) qui décrit une transaction d’échange d’appareils, y compris la valeur d’échange, l’identifiant d’appareil d’origine et le nouvel identifiant d’appareil.

![ Structure Détails de l’entrée de l’appareil ](../../images/field-groups/device-trade-in-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `tradeInValue` | [Devise](../../data-types/currency.md) | La valeur de l’appareil qui fait l’objet d’un échange. |
| `newDeviceID` | Chaîne | L’identifiant du nouvel appareil pour lequel le commerce a lieu. |
| `originalDeviceID` | Chaîne | L’identifiant de l’appareil qui fait l’objet du commerce. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
