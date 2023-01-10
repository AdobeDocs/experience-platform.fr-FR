---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;emailAddress;xdm:emailAddress;email;adresse électronique;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de l’adresse électronique
description: Ce document fournit un aperçu du type de données XDM Adresse électronique.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# [!UICONTROL Adresse électronique] type de données

[!UICONTROL Adresse électronique] est un type de données XDM (Experience Data Model) standard qui décrit les détails d’une adresse électronique.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propriété | Description |
| --- | --- |
| `address` | Adresse technique de l’email telle que généralement définie dans la norme RFC2822 et les normes ultérieures (par exemple : `name@domain.com`).<br><br>Dans XDM, les adresses électroniques doivent contenir un domaine de niveau supérieur valide pour passer la validation. Reportez-vous aux [document](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) pour obtenir une liste complète des domaines de niveau supérieur valides tels que définis par l’Internet Assigned Numbers Authority (IANA). |
| `label` | Informations d’affichage supplémentaires qui peuvent être disponibles. Par exemple, si un courrier électronique contient une adresse Microsoft Outlook enrichie de `John Smith smithjr@company.uk`, `John Smith` serait placé dans ce champ. |
| `primary` | Indique s’il s’agit de l’adresse électronique Principale de l’individu. Un profil ne peut avoir qu’un seul `primary` adresse électronique à un moment donné. |
| `status` | Indique si l’adresse électronique peut être actuellement utilisée. |
| `statusReason` | Description de la variable active `status`. |
| `type` | La façon dont le compte est associé à la personne (par exemple `work` ou `personal`). |

{style=&quot;table-layout:auto&quot;}


Pour plus d’informations sur le type de données de l’adresse électronique, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
