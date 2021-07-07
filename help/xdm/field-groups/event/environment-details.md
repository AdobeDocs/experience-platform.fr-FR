---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;environnement;détails de l’environnement;
solution: Experience Platform
title: Groupe de champs de schéma Détails de l’environnement
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs Détails de l’environnement ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 5%

---


# [!UICONTROL Groupe de champs ] Détails de l’environnement

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../name-updates.md) .

[!UICONTROL Détails de l’environnement ] Groupe de champs de schéma standard pour la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe afin de capturer des informations concernant les détails d’environnement liés à un événement d’expérience, tels que les détails du périphérique, les informations du navigateur, l’heure locale et d’autres informations géographiques.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `device` | [Appareil](../../data-types/device.md) | Describes an identified device, application or device browser instance that is trackable across sessions, normally by cookies. |
| `environment` | [Environnement](../../data-types/environment.md) | Describes information about the situational context of the event observation, specifically detailing transitory information such as the network or software versions. |
| `placeContext` | [Contexte de l’emplacement](../../data-types/place-context.md) | Décrit les circonstances transitoires liées à l’observation de l’événement. Par exemple, des informations spécifiques à un paramètre régional telles que la météo, l’heure locale, le trafic, le jour de la semaine, le jour de travail par rapport aux jours fériés et les heures de travail. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
