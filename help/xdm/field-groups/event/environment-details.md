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
ht-degree: 10%

---


# [!UICONTROL Détails de l’environnement] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails de l’environnement] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) utilisé pour capturer des informations concernant les détails d’environnement liés à un événement d’expérience, comme les détails de l’appareil, les informations du navigateur, l’heure locale et d’autres informations géographiques.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `device` | [Appareil](../../data-types/device.md) | Décrit un périphérique, une application ou une instance de navigateur d’appareil identifié qui peut faire l’objet d’un suivi entre plusieurs sessions, généralement par des cookies. |
| `environment` | [Environnement](../../data-types/environment.md) | Décrit les informations sur le contexte situationnel de l’observation de l’événement, en particulier des informations transitoires telles que les versions du réseau ou des logiciels. |
| `placeContext` | [Contexte de l’emplacement](../../data-types/place-context.md) | Décrit les circonstances transitoires liées à l’observation de l’événement. Par exemple, des informations spécifiques à un paramètre régional telles que la météo, l’heure locale, le trafic, le jour de la semaine, le jour de travail par rapport aux jours fériés et les heures de travail. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
