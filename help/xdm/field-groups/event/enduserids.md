---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;endserids;utilisateur final;id;
solution: Experience Platform
title: Groupe de champs de schéma Détails de l’ID utilisateur final
description: Découvrez le groupe de champs Détails de l’ID de l’utilisateur final.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 16%

---


# [!UICONTROL Détails de l’identifiant utilisateur final] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails de l’identifiant utilisateur final] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilisé pour décrire les informations d’identité d’une personne dans plusieurs applications d’Adobe. Le groupe de champs fournit un objet `endUserIDs` de niveau racine, qui contient lui-même un champ `_experience` en lecture seule dont les valeurs sont automatiquement mises à jour lors de l’ingestion des données.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `aacustomid` | [Identité](../../data-types/identity.md) | Identifiants utilisateur final personnalisés pour Adobe Analytics Cloud. |
| `aaid` | [Identité](../../data-types/identity.md) | ID utilisateur final pour Adobe Analytics Cloud. |
| `acid` | [Identité](../../data-types/identity.md) | ID utilisateur final pour Adobe Campaign. |
| `adcloud` | [Identité](../../data-types/identity.md) | ID utilisateur final pour Adobe Advertising Cloud. |
| `emailid` | [Identité](../../data-types/identity.md) | ID d’adresse électronique. |
| `mcid` | [Identité](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `phonenumberid` | [Identité](../../data-types/identity.md) | ID de numéro de téléphone. |
| `tntid` | [Identité](../../data-types/identity.md) | ID utilisateur final pour Adobe Target. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
