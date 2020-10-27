---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: Mélangeur Détails de l’ID utilisateur final
topic: overview
description: Ce document présente un aperçu du mixin Détails de l’ID d’utilisateur final.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 6%

---


# [!UICONTROL Mélange des détails] d’ID d’utilisateur final

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document sur les mises à jour [des noms de](../name-updates.md) mixin.

[!UICONTROL Les détails] d&#39;identification de l&#39;utilisateur final sont un mélange standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), utilisé pour décrire les informations d&#39;identité d&#39;une personne dans plusieurs applications d&#39;Adobe. Le mixin fournit un objet de niveau racine, qui contient lui-même un `endUserIDs` `_experience` champ en lecture seule dont les valeurs sont automatiquement mises à jour au fur et à mesure de l’assimilation des données.

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
