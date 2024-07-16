---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;appareil;type de données;type de données;type de données;devise;
solution: Experience Platform
title: Type de données de devise
description: Découvrez le type de données XDM de devise.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 6%

---

# Type de données [!UICONTROL Currency]

[!UICONTROL Currency] est un type de données XDM standard qui décrit une quantité de devise, y compris le type de devise et la date de conversion.

![](../images/data-types/currency.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `amount` | Double | Montant de la devise définie par le `currencyCode`. |
| `conversionDate` | DateTime | Horodatage du moment où la conversion de devise a été effectuée. |
| `currencyCode` | Chaîne | Un code ISO 4217 indiquant le type de devise représenté par `amount`. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
