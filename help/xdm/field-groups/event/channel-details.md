---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;ExperienceEvent;champs;schémas;Schémas;Conception de schéma;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma des détails du canal
description: Découvrez le groupe de champs de schéma Détails du canal .
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
TQID: https://experienceleague.adobe.com/XdT9A0-YF5x0k-XPjmN5kABrIBqao1gOcLbIKcujues
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 140
ht-degree: 17%

---

# [!UICONTROL Channel Details] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Channel Details] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisé pour décrire les informations sur le canal telles que l’identifiant, le type de canal, le type de média et le type d’emplacement.

![](../../images/field-groups/channel-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `channel` | [Canal Experience](../../data-types/experience-channel.md) | Objet décrivant les retours de produits, l’enregistrement de la garantie et les processus de commande/panier. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
