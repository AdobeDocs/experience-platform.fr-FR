---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; ExperienceEvent ; champs ; schémas ; Schémas ; conception de Schéma ; groupe de champs ; groupe de champs ; enduserids ; utilisateur final ; ids ; id ;
solution: Experience Platform
title: Groupe de champs Détails de l'ID d'utilisateur final
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs Détails de l’ID d’utilisateur final.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 5%

---


# [!UICONTROL Groupe de champs ] Détails de l&#39;ID utilisateur final

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mise à jour du nom du groupe de champs](../name-updates.md).

[!UICONTROL ID utilisateur final ] Détail d&#39;un groupe de champs de schéma standard pour la  [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), utilisé pour décrire les informations d&#39;identité d&#39;une personne dans plusieurs applications d&#39;Adobe. Le groupe de champs fournit un objet de niveau racine `endUserIDs`, qui contient lui-même un champ `_experience` en lecture seule dont les valeurs sont automatiquement mises à jour au fur et à mesure que les données sont ingérées.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

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

Pour plus d&#39;informations sur le groupe de champs, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
