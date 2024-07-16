---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma Détails du canal
description: Découvrez le groupe de champs Détails du canal .
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 20%

---

# [!UICONTROL Détails du canal] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails du canal] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilisé pour décrire les informations de canal telles que l’identifiant, le type de canal, le type de média et le type d’emplacement.

![](../../images/field-groups/channel-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `channel` | [Canal d’expérience](../../data-types/experience-channel.md) | Objet décrivant les retours de produits, l’enregistrement de la garantie et les processus du panier/de la commande. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
