---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;emailAddress;xdm:emailAddress;e-mail;adresse e-mail;type de données;type de données;
solution: Experience Platform
title: Type de données d’adresse e-mail
description: Découvrez le type de données XDM d’adresse e-mail.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# [!UICONTROL Adresse e-mail] type de données

[!UICONTROL Adresse e-mail] est un type de données standard des modèles de données d’expérience (XDM) qui décrit les détails d’une adresse e-mail.

![](../images/data-types/email-address.png){width=450}

| Propriété | Description |
| --- | --- |
| `address` | Adresse technique de l’e-mail telle qu’elle est généralement définie dans les normes RFC2822 et suivantes (par exemple, `name@domain.com`).<br><br>Dans XDM, les adresses e-mail doivent contenir un domaine de niveau supérieur valide pour réussir la validation. Reportez-vous au [document](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) suivant pour obtenir une liste complète des domaines de niveau supérieur valides tels que définis par l’Internet Assigned Numbers Authority (IANA). |
| `label` | Informations d’affichage supplémentaires éventuellement disponibles. Par exemple, si un e-mail affiche une adresse Microsoft Outlook enrichie de `John Smith smithjr@company.uk`, `John Smith` serait placé dans ce champ. |
| `primary` | Indique s’il s’agit de l’adresse e-mail principale de la personne. Un profil ne peut avoir qu’une seule adresse e-mail `primary` à un moment donné. |
| `status` | Indique si l’adresse e-mail peut être actuellement utilisée |
| `statusReason` | Description de la `status` actuelle. |
| `type` | La façon dont le compte est associé à la personne (par exemple `work` ou `personal`). |

{style="table-layout:auto"}


Pour plus d’informations sur le type de données d’adresse e-mail, reportez-vous au référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
