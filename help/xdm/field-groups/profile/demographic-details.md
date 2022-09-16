---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schéma;conception de schéma;groupe de champs;groupe de champs;personne;détails de personne de profil;personne;personne
solution: Experience Platform
title: Groupe de champs de schéma de détails démographiques
topic-legacy: overview
description: Ce document fournit un aperçu du groupe de champs de schéma Détails démographiques .
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 26%

---


# [!UICONTROL Détails démographiques] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails démographiques] est un groupe de champs de schéma standard pour la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Le groupe de champs fournit un niveau racine `person` dont les sous-champs décrivent les informations sur une personne.

![](../../images/field-groups/demographic-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `person.name` | [Nom de la personne](../../data-types/person-name.md) | Objet dont les sous-champs décrivent les différents éléments du nom d’une personne. |
| `person.birthDate` | Date | Date complète à laquelle une personne est née, sous la forme d’un horodatage ISO 8601. |
| `person.birthDayAndMonth` | Chaîne | Jour et mois de naissance d’une personne, au format MM-JJ. Ce champ doit être utilisé lorsque le jour et le mois de naissance d’une personne sont connus, mais pas l’année. |
| `person.birthYear` | Nombre entier | L’année de naissance d’une personne, y compris le siècle (comme 1989). Ce champ doit être utilisé lorsque seul l’âge de la personne est connu, pas sa date de naissance complète. |
| `person.gender` | Chaîne | Identité de genre de la personne. |
| `person.martialStatus` | Chaîne | Décrit la relation d’une personne avec une autre significative. |
| `person.nationality` | Chaîne | La relation juridique entre une personne et son état représentée à l’aide du code ISO 3166-1 Alpha-2. |
| `person.taxId` | Chaîne | ID fiscal de la personne, comme le TIN aux États-Unis ou le CIF/NIF en Espagne. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)