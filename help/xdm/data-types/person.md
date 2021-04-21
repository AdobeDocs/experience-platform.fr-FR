---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; personne ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données de personne
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Person Experience Data Model).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 16%

---

# [!UICONTROL Type ] de données personnelles

 Personis est un type de données XDM (Experience Data Model) standard qui décrit une personne. Ce type de données peut représenter une personne agissant dans divers rôles, tel qu’un client, un contact ou un propriétaire.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `name` | [[!UICONTROL Nom de la personne]](./person-name.md) | Décrit des détails sur le nom complet de la personne. |
| `birthDate` | Date | Date de naissance complète d’une personne. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `birthDayAndMonth` | Chaîne | Jour et mois de naissance d’une personne, au format MM-JJ. Ce champ doit être utilisé lorsque le jour et le mois de naissance d’une personne sont connus, mais pas l’année. Le format de cette propriété doit être conforme à cette expression régulière `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Entier | L&#39;année de naissance d&#39;une personne, y compris le siècle (par exemple, `1983`). Ce champ doit être utilisé lorsque seul l&#39;âge de la personne est connu et non la date de naissance complète. Cette valeur doit être comprise entre 1 et 32767. |
| `gender` | Chaîne | L&#39;identité de genre de la personne. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> La valeur par défaut est `not_specified`. |
| `maritalStatus` | Chaîne | Décrit la relation d&#39;une personne avec une autre personne importante. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération suivantes. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> La valeur par défaut est `not_specified`. |
| `nationality` | Chaîne | La relation juridique entre une personne et son État représentée à l&#39;aide du code ISO 3166-1 Alpha-2. Le format de cette propriété doit être conforme à cette expression régulière `^[A-Z]{2}$`. |
| `taxId` | Chaîne | ID fiscal ou fiscal de la personne, tel que le Numéro d&#39;identification du contribuable (TIN) aux États-Unis ou le Certificado de Identificación Fiscal (CIF/NIF) en Espagne. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
