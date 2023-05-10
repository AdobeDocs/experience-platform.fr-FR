---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;appareil;commerce;échange;échange
solution: Experience Platform
title: Groupe de champs de schéma Détails sur l’entrée du périphérique
description: Ce document fournit une vue d’ensemble du groupe de champs Détails du commerce d’appareil.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 15%

---

# [!UICONTROL Détails sur l’entrée des appareils] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails sur l’entrée des appareils] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Il fournit un champ unique (`deviceTradeInDetails`) qui décrit une transaction d’échange d’appareils, y compris la valeur d’échange, l’identifiant d’appareil d’origine et le nouvel identifiant d’appareil.

![Structure Détails de l’entrée de l’appareil](../../images/field-groups/device-trade-in-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `tradeInValue` | [Devise](../../data-types/currency.md) | La valeur de l’appareil qui fait l’objet d’un échange. |
| `newDeviceID` | Chaîne | L’identifiant du nouvel appareil pour lequel le commerce a lieu. |
| `originalDeviceID` | Chaîne | L’identifiant de l’appareil qui fait l’objet du commerce. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
