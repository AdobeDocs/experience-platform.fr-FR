---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;appareil;type de données;type de données;type de données;devise;
solution: Experience Platform
title: Type de données de devise
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM de devise.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 5e92b288bb8c996cfcf343d8ac1ab1665b0d3ad0
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 7%

---

# [!UICONTROL Devise] type de données

[!UICONTROL Devise] est un type de données XDM standard qui décrit une quantité de devise, y compris le type de devise et la date de conversion.

![](../images/data-types/currency.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `amount` | Double | Le montant de la devise tel que défini par la variable `currencyCode`. |
| `conversionDate` | DateTime | Horodatage du moment où la conversion de devise a été effectuée. |
| `currencyCode` | Chaîne | Un code ISO 4217 indiquant le type de devise qui `amount` représente . |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
