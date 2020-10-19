---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data type;
solution: Experience Platform
title: Type de données d'adresse électronique
topic: overview
description: Ce document présente un aperçu du type de données XDM d'adresse électronique.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---


# [!UICONTROL Type de données d&#39;adresse] de courriel

[!UICONTROL L’adresse] électronique est un type de données XDM standard qui décrit les détails d’une adresse électronique.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propriété | Description |
| --- | --- |
| `address` | Adresse technique du courrier électronique, définie couramment dans la norme RFC2822 et les normes suivantes (par exemple, `name@domain.com`). |
| `label` | Informations supplémentaires sur l’affichage disponibles. Par exemple, si un courrier électronique comporte un écran d&#39;adresse riche Microsoft Outlook `John Smith smithjr@company.uk`, `John Smith` il sera placé dans ce champ. |
| `primary` | Indique s’il s’agit de l’Principale adresse électronique de l’individu. Un profil ne peut avoir qu’une seule `primary` adresse électronique à un moment donné. |
| `status` | Indique si l’adresse électronique peut être actuellement utilisée. |
| `statusReason` | A description of the current `status`. |
| `type` | La façon dont le compte se rapporte à la personne (telle que `work` ou `personal`). |


Pour plus d&#39;informations sur le type de données d&#39;adresse électronique, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)