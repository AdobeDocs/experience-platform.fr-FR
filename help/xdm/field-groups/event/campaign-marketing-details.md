---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma Détails du marketing de Campaign
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs Détails du marketing Campaign .
exl-id: be08b38b-68a0-4a74-9b8f-0344a0637395
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 5%

---

# [!UICONTROL Groupe de champs ] Détails du marketing de Campaign

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../name-updates.md) .

[!UICONTROL Les ] détails marketing d’une campagne constituent un groupe de champs de schéma standard pour la  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilisé pour décrire les informations de campagne marketing telles que le groupe de campagne, le nom et le code de suivi.

![](../../images/field-groups/campaign-marketing-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Objet qui décrit des informations sur les campagnes marketing, telles que le groupe, le nom et le code de suivi des campagnes. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
