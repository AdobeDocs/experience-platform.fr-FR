---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: mixin EndUserIDs d’ExperienceEvent
topic: overview
description: Ce document présente un aperçu du mixin EndUserIDs d’ExperienceEvent.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 8%

---


# [!UICONTROL Mélange des identifiantsutilisateur] de l’événement ExperienceEvent

[!UICONTROL ExperienceEvent EndUserIDs] est un mixin standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), utilisé pour décrire les informations d&#39;identité d&#39;une personne dans plusieurs applications d&#39;Adobe. Le mixin fournit un objet de niveau racine, qui contient lui-même un `endUserIDs` `_experience` champ en lecture seule dont les valeurs sont automatiquement mises à jour au fur et à mesure de l’assimilation des données.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `aacustomid` | [Identité](../../data-types/identity.md) | Identifiants d’utilisateur final personnalisés pour Adobe Analytics Cloud. |
| `aaid` | [Identité](../../data-types/identity.md) | ID d’utilisateur final pour Adobe Analytics Cloud. |
| `acid` | [Identité](../../data-types/identity.md) | ID d’utilisateur final pour Adobe Campaign. |
| `adcloud` | [Identité](../../data-types/identity.md) | ID d’utilisateur final pour Adobe Advertising Cloud. |
| `emailid` | [Identité](../../data-types/identity.md) | ID d’adresse électronique. |
| `mcid` | [Identité](../../data-types/identity.md) | ID Adobe Marketing Cloud. |
| `phonenumberid` | [Identité](../../data-types/identity.md) | ID de numéro de téléphone. |
| `tntid` | [Identité](../../data-types/identity.md) | ID d’utilisateur final pour Adobe Target. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
