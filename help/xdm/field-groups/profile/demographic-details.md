---
keywords: Experience Platform ; accueil ; thèmes populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; conception de Schéma ; groupe de champs ; personne ; détails de la personne ; détails de la personne profil ; personne ;
solution: Experience Platform
title: Groupe de Schéma de données démographiques
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs du schéma Détails démographiques.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: f5beb57acf4cc1827bf08b549cd2b3a02fd82b18
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 21%

---


# [!UICONTROL Groupe de champs ] Détails démographiques

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mise à jour du nom du groupe de champs](../name-updates.md).

[!UICONTROL Données démographiques ] Détaillant un groupe de champs de schéma standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit un objet de niveau racine `person`, dont les sous-champs décrivent les informations sur une personne.

![](../../images/field-groups/demographic-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `person.name` | [Nom de la personne](../../data-types/person-name.md) | Objet dont les sous-champs décrivent divers éléments du nom d’une personne. |
| `person.birthDate` | Date | Date complète à laquelle une personne est née, sous la forme d&#39;un horodatage ISO 8601. |
| `person.birthDayAndMonth` | Chaîne | Jour et mois de naissance d’une personne, au format MM-JJ. Ce champ doit être utilisé lorsque le jour et le mois de naissance d’une personne sont connus, mais pas l’année. |
| `person.birthYear` | Entier | L&#39;année de naissance d&#39;une personne, y compris le siècle (comme 1989). Ce champ doit être utilisé lorsque seul l’âge de la personne est connu, pas sa date de naissance complète. |
| `person.gender` | Chaîne | L&#39;identité de genre de la personne. |
| `person.martialStatus` | Chaîne | Décrit la relation d&#39;une personne avec une autre personne importante. |
| `person.nationality` | Chaîne | La relation juridique entre une personne et son État représentée à l&#39;aide du code ISO 3166-1 Alpha-2. |
| `person.taxId` | Chaîne | ID fiscal de la personne, tel que le TIN aux États-Unis ou le CIF/NIF en Espagne. |

Pour plus d&#39;informations sur le groupe de champs, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)