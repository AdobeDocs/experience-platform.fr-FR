---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; ExperienceEvent ; champs ; schémas ; Schémas ; Schéma design ; mixin ; mixin ; environnement ; détails environnement ;
solution: Experience Platform
title: Mélange des détails de l'Environnement
topic-legacy: overview
description: Ce document présente un aperçu du mixin Détails de l’Environnement ExperienceEvent.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 4%

---

# [!UICONTROL Environnement ] Detailsmixin

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document [Mises à jour du nom de mixin](../name-updates.md).

[!UICONTROL Les ] détails de l’Environnement sont un mixin standard pour la  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) classe utilisée pour capturer des informations concernant les détails de l’environnement liés à un Événement d’expérience, tels que les détails du périphérique, les informations du navigateur, l’heure locale et d’autres informations géographiques.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `device` | [Appareil](../../data-types/device.md) | Décrit une instance de navigateur de périphérique, d’application ou de périphérique identifiée qui peut faire l’objet d’un suivi entre les sessions, généralement par des cookies. |
| `environment` | [Environnement](../../data-types/environment.md) | Décrit des informations sur le contexte situationnel de l&#39;observation du événement, notamment des informations transitoires telles que les versions du réseau ou des logiciels. |
| `placeContext` | [Contexte de l’emplacement](../../data-types/place-context.md) | Décrit les circonstances transitoires liées à l&#39;observation du événement. Les exemples incluent des informations spécifiques aux paramètres régionaux telles que la météo, l’heure locale, le trafic, le jour de la semaine, le jour de travail par rapport aux jours fériés et les heures de travail. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
