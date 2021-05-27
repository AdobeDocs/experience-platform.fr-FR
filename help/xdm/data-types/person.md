---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;personne;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Personne
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Person Experience Data Model).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 17%

---

#  Type de données personnelles

 Personest un type de données XDM (Experience Data Model) standard qui décrit une personne. Ce type de données peut représenter une personne agissant dans divers rôles, tels qu’un client, un contact ou un propriétaire.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `name` | [[!UICONTROL Nom de la personne]](./person-name.md) | Décrit les détails du nom complet de la personne. |
| `birthDate` | Date | Date de naissance complète d’une personne. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `birthDayAndMonth` | Chaîne | Jour et mois de naissance d’une personne, au format MM-JJ. Ce champ doit être utilisé lorsque le jour et le mois de naissance d’une personne sont connus, mais pas l’année. Le format de cette propriété doit être conforme à cette expression régulière `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Entier | L’année de naissance d’une personne, y compris le siècle (par exemple, `1983`). Ce champ doit être utilisé lorsque seul l’âge de la personne est connu et non la date de naissance complète. Cette valeur doit être comprise entre 1 et 32767. |
| `gender` | Chaîne | Identité de genre de la personne. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> La valeur par défaut est `not_specified`. |
| `maritalStatus` | Chaîne | Décrit la relation d’une personne avec une autre significative. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération suivantes. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> La valeur par défaut est `not_specified`. |
| `nationality` | Chaîne | La relation juridique entre une personne et son état représentée à l’aide du code ISO 3166-1 Alpha-2. Le format de cette propriété doit être conforme à cette expression régulière `^[A-Z]{2}$`. |
| `taxId` | Chaîne | ID fiscal ou fiscal de la personne, comme le Numéro d&#39;identification du contribuable (TIN) aux États-Unis ou le Certificado de l&#39;identification fiscale (CIF/NIF) en Espagne. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
