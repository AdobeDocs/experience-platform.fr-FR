---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;iab;tcf;consentement;groupe de champs;schéma;schéma;schéma;schéma;schéma;schéma;schéma;groupe de champs;iab;tcf;consentement
solution: Experience Platform
title: Groupe de champs de consentement du TCF 2.0 de l’IAB pour les schémas d’événement
description: Découvrez le groupe de champs de schéma de consentement du TCF 2.0 de l’IAB pour la classe XDM ExperienceEvent.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!UICONTROL Groupe de champs du consentement IAB TCF 2.0] pour les schémas d’événement

>[!IMPORTANT]
>
>Ce document couvre le groupe de champs de schéma [!UICONTROL Consentement IAB TCF 2.0] pour la classe XDM ExperienceEvent. Ce groupe de champs ne doit être utilisé que si vous avez l’intention de suivre les événements de changement de consentement au fil du temps.
>
>Notez que les valeurs de consentement enregistrées dans les données d’événement ne sont pas respectées dans les workflows d’application automatique. Pour que l’application automatique soit effective, les valeurs de consentement doivent être ingérées dans la classe XDM Individual Profile et activées pour Real-time Customer Profile.
>
>Pour le groupe de champs destiné à la classe XDM Individual Profile, reportez-vous au [document](../profile/iab.md) suivant à la place.

[!UICONTROL Le consentement IAB TCF 2.0] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisée pour capturer une série horodatée de chaînes de consentement IAB, afin de suivre les modèles de changement de consentement au fil du temps.

![](../../images/field-groups/iab-event.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `consentStrings` | Tableau de [Chaînes de consentement](../../data-types/consent-string.md) | Tableau de valeurs de chaîne de consentement associées à l’événement. |

{style="table-layout:auto"}

Consultez le guide sur la [prise en charge du TCF 2.0 de l’IAB dans Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) pour plus d’informations sur le cas d’utilisation de ce groupe de champs. Pour plus d’informations sur le groupe de champs lui-même, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
