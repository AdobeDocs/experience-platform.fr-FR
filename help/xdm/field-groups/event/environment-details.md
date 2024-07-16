---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;environnement;détails de l’environnement;
solution: Experience Platform
title: Groupe de champs de schéma Détails de l’environnement
description: Découvrez le groupe de champs Détails de l’environnement ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 13%

---


# [!UICONTROL Détails de l’environnement] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails de l’environnement] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisée pour capturer des informations concernant les détails de l’environnement liés à un événement d’expérience, tels que les détails de l’appareil, les informations du navigateur, l’heure locale et d’autres informations géographiques.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `device` | [Appareil](../../data-types/device.md) | Décrit un appareil, une application ou une instance de navigateur d’appareil identifié qui peut faire l’objet d’un suivi entre plusieurs sessions, généralement par des cookies. |
| `environment` | [Environnement](../../data-types/environment.md) | Décrit les informations sur le contexte situationnel de l’observation de l’événement, en particulier des informations transitoires telles que les versions du réseau ou des logiciels. |
| `placeContext` | [Placer le contexte](../../data-types/place-context.md) | Décrit les circonstances transitoires liées à l’observation de l’événement. Par exemple, des informations spécifiques à un paramètre régional telles que la météo, l’heure locale, le trafic, le jour de la semaine, le jour de travail par rapport aux jours fériés et les heures de travail. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
