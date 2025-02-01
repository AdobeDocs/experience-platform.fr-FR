---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;ExperienceEvent;champs;schémas;Schémas;Conception de schéma;groupe de champs;groupe de champs;enduserids;utilisateur final;utilisateur final;id;
solution: Experience Platform
title: Groupe de champs de schéma Détails de l’ID de l’utilisateur final
description: Découvrez le groupe de champs de schéma Détails de l’ID de l’utilisateur final .
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 15%

---


# [!UICONTROL Détails de l’ID de l’utilisateur final] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails de l’ID de l’utilisateur final] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilisé pour décrire les informations d’identité d’un individu dans plusieurs applications d’Adobe. Le groupe de champs fournit un objet `endUserIDs` de niveau racine, qui contient lui-même un champ de `_experience` en lecture seule dont les valeurs sont automatiquement mises à jour lors de l’ingestion des données.

![](../../images/field-groups/enduserids.png){width=700}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `aacustomid` | [Identité](../../data-types/identity.md) | ID d’utilisateurs finaux personnalisés pour Adobe Analytics Cloud. |
| `aaid` | [Identité](../../data-types/identity.md) | ID d’utilisateurs finaux pour Adobe Analytics Cloud. |
| `acid` | [Identité](../../data-types/identity.md) | ID des utilisateurs finaux pour Adobe Campaign. |
| `adcloud` | [Identité](../../data-types/identity.md) | ID d’utilisateurs finaux pour Adobe Advertising Cloud. |
| `emailid` | [Identité](../../data-types/identity.md) | ID des adresses e-mail. |
| `mcid` | [Identité](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). Le MCID est désormais connu sous le nom d’identifiant Experience Cloud (ECID). |
| `phonenumberid` | [Identité](../../data-types/identity.md) | ID des numéros de téléphone. |
| `tntid` | [Identité](../../data-types/identity.md) | ID des utilisateurs finaux pour Adobe Target. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
