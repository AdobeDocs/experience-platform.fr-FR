---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schéma;conception de schéma;groupe de champs;groupe de champs;personne;détails de personne de profil;personne;personne
solution: Experience Platform
title: Demographic Details Schema Field Group
topic-legacy: overview
description: This document provides an overview of the Demographic Details schema field group.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 22%

---


# [!UICONTROL Groupe de champs ] Demographic Detailsschema

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../name-updates.md) .

[!UICONTROL Démographie ] Détail d’un groupe de champs de schéma standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit un objet `person` de niveau racine, dont les sous-champs décrivent les informations sur une personne.

![](../../images/field-groups/demographic-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `person.name` | [Nom de la personne](../../data-types/person-name.md) | Objet dont les sous-champs décrivent les différents éléments du nom d’une personne. |
| `person.birthDate` | Date | The full date a person was born on, in the form of an ISO 8601 timestamp. |
| `person.birthDayAndMonth` | Chaîne | Jour et mois de naissance d’une personne, au format MM-JJ. Ce champ doit être utilisé lorsque le jour et le mois de naissance d’une personne sont connus, mais pas l’année. |
| `person.birthYear` | Entier | The year a person was born, including the century (such as 1989). Ce champ doit être utilisé lorsque seul l’âge de la personne est connu, pas sa date de naissance complète. |
| `person.gender` | Chaîne | The gender identity of the person. |
| `person.martialStatus` | Chaîne | Décrit la relation d’une personne avec une autre significative. |
| `person.nationality` | Chaîne | La relation juridique entre une personne et son état représentée à l’aide du code ISO 3166-1 Alpha-2. |
| `person.taxId` | Chaîne | ID fiscal de la personne, comme le TIN aux États-Unis ou le CIF/NIF en Espagne. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)