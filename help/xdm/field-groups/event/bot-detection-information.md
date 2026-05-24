---
title: Groupe de champs de détection de robots
description: Découvrez le groupe de champs de schéma de groupe de champs de détection de robots (XDM).
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
TQID: https://experienceleague.adobe.com/Vz2-I-KoJ-hFWNKbazTS752eSJWhq4uIQLbzMlL-Glk
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 6%

---

# [!UICONTROL Bot Detection] le groupe de champs

[!UICONTROL Bot Detection] groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit des informations sur le trafic généré par les robots.

![Diagramme du groupe de champs [!UICONTROL Bot Detection].](../../images/field-groups/bot-detection-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Bot Detection] | `botDetection` | objet | Fournit des informations sur le trafic généré par les robots. |
| [!UICONTROL Score] | `score` | nombre | Score de probabilité des robots compris entre zéro et un. Un score de zéro signifie que le trafic n’est pas un robot. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
