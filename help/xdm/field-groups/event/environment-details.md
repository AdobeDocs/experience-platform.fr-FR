---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; ExperienceEvent ; champs ; schémas ; Schémas ; conception de Schéma ; groupe de champs ; environnement ; détails de l'environnement ;
solution: Experience Platform
title: Groupe de champs Détails de l'Environnement
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs Détails de l’Environnement ExperienceEvent.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 3%

---


# [!UICONTROL Groupe de champs ] Détails de l&#39;Environnement

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mise à jour du nom du groupe de champs](../name-updates.md).

[!UICONTROL Les ] détails de l’Environnement constituent un groupe de champs de schéma standard pour la  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) classe afin de capturer des informations concernant les détails d’environnement liés à un Événement d’expérience, tels que les détails du périphérique, les informations du navigateur, l’heure locale et d’autres informations géographiques.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `device` | [Appareil](../../data-types/device.md) | Décrit une instance de navigateur de périphérique, d’application ou de périphérique identifiée qui peut faire l’objet d’un suivi entre les sessions, généralement par des cookies. |
| `environment` | [Environnement](../../data-types/environment.md) | Décrit des informations sur le contexte situationnel de l&#39;observation du événement, notamment des informations transitoires telles que les versions du réseau ou des logiciels. |
| `placeContext` | [Contexte de l’emplacement](../../data-types/place-context.md) | Décrit les circonstances transitoires liées à l&#39;observation du événement. Les exemples incluent des informations spécifiques aux paramètres régionaux telles que la météo, l’heure locale, le trafic, le jour de la semaine, le jour de travail par rapport aux jours fériés et les heures de travail. |

Pour plus d&#39;informations sur le groupe de champs, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
