---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;emailAddress;xdm:emailAddress;email;adresse électronique;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de l’adresse électronique
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM Adresse électronique.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# [!UICONTROL Type de données ] d’adresse électronique

[!UICONTROL L’] adresse électronique est un type de données XDM standard qui décrit les détails d’une adresse électronique.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propriété | Description |
| --- | --- |
| `address` | Adresse technique de l’email telle que définie couramment dans la norme RFC2822 et les normes ultérieures (par exemple, `name@domain.com`). |
| `label` | Informations d’affichage supplémentaires qui peuvent être disponibles. Par exemple, si un email comporte un affichage d’adresse enrichie Microsoft Outlook de `John Smith smithjr@company.uk`, `John Smith` est placé dans ce champ. |
| `primary` | Indique s’il s’agit de l’adresse électronique Principale de l’individu. Un profil ne peut avoir qu’une seule `primary` adresse électronique à un moment donné. |
| `status` | Indique si l’adresse électronique peut être actuellement utilisée. |
| `statusReason` | Description de la balise `status` actuelle. |
| `type` | La façon dont le compte est associé à la personne (par exemple, `work` ou `personal`). |

{style=&quot;table-layout:auto&quot;}


Pour plus d’informations sur le type de données de l’adresse électronique, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)
