---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;emailAddress;xdm:emailAddress;email;adresse électronique;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de l’adresse électronique
description: Découvrez le type de données XDM Adresse électronique.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Type de données [!UICONTROL Email address]

[!UICONTROL Email address] est un type de données XDM (Experience Data Model) standard qui décrit les détails d’une adresse électronique.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propriété | Description |
| --- | --- |
| `address` | Adresse technique de l’email telle que généralement définie dans la norme RFC2822 et les normes ultérieures (par exemple, `name@domain.com`).<br><br>Dans XDM, les adresses électroniques doivent contenir un domaine de niveau supérieur valide pour passer la validation. Reportez-vous au [document](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) suivant pour obtenir la liste complète des domaines de niveau supérieur valides tels que définis par l’Internet Assigned Numbers Authority (IANA). |
| `label` | Informations d’affichage supplémentaires qui peuvent être disponibles. Par exemple, si un email a un affichage d’adresse enrichie Microsoft Outlook de `John Smith smithjr@company.uk`, `John Smith` sera placé dans ce champ. |
| `primary` | Indique s’il s’agit de l’adresse électronique principale de l’individu. Un profil ne peut avoir qu’une seule adresse électronique `primary` à un moment donné. |
| `status` | Indique si l’adresse électronique peut être actuellement utilisée. |
| `statusReason` | Description du `status` actif. |
| `type` | La façon dont le compte se rapporte à la personne (par exemple `work` ou `personal`). |

{style="table-layout:auto"}


Pour plus d’informations sur le type de données de l’adresse électronique, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
