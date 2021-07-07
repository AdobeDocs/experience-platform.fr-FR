---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma Détails du canal
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs de schéma Détails du canal .
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---


# [!UICONTROL Groupe de champs ] Détails du canal

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../name-updates.md) .

[!UICONTROL Détails ] du canal : groupe de champs de schéma standard pour la  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilisé pour décrire les informations de canal telles que l’identifiant, le type de canal, le type de média et le type d’emplacement.

![](../../images/field-groups/channel-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `channel` | [Canal d’expérience](../../data-types/experience-channel.md) | Objet décrivant les retours de produits, l’enregistrement de la garantie et les processus du panier/de la commande. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
