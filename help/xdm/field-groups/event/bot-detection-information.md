---
title: Groupe de champs de détection de robots
description: En savoir plus sur le groupe de champs de schéma de la détection des robots (XDM).
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 8%

---

# [!UICONTROL Détection de robots] groupe de champs

[!UICONTROL La détection des robots] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit des informations sur le trafic généré par les robots.

![Schéma du groupe de champs [!UICONTROL Détection de robots].](../../images/field-groups/bot-detection-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Détection de robots] | `botDetection` | objet | Fournit des informations sur le trafic généré par les robots. |
| [!UICONTROL Score] | `score` | nombre | La probabilité des robots est comprise entre 0 et 1. Un score nul signifie que le trafic n’est pas un robot. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
