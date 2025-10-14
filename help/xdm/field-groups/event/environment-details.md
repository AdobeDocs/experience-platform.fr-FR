---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;ExperienceEvent;champs;schémas;Schémas;Conception de schéma;groupe de champs;groupe de champs;environnement;détails de l’environnement;
solution: Experience Platform
title: Groupe De Champs De Schéma Des Détails De L’Environnement
description: Découvrez le groupe de champs de schéma Détails de l’environnement ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 13%

---


# Groupe de champs de schéma [!UICONTROL Détails de l’environnement]

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails de l’environnement] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisé pour capturer des informations concernant les détails de l’environnement liés à un événement d’expérience, tels que des détails de l’appareil, des informations du navigateur, l’heure locale et d’autres informations géographiques.

![](../../images/field-groups/environment-details.png){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `device` | [Appareil](../../data-types/device.md) | Décrit une instance de navigateur d’appareil, d’application ou d’appareil identifiée pouvant être suivie entre les sessions, normalement par des cookies. |
| `environment` | [Environnement](../../data-types/environment.md) | Décrit les informations sur le contexte situationnel de l’observation de l’événement, en détaillant spécifiquement les informations éphémères telles que les versions logicielles ou réseau. |
| `placeContext` | [Contexte du lieu](../../data-types/place-context.md) | Décrit les circonstances transitoires liées à l’observation de l’événement. Par exemple, des informations spécifiques aux paramètres régionaux telles que la météo, l’heure locale, le trafic, le jour de la semaine, la distinction jours de travail/vacances et les heures de travail. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
