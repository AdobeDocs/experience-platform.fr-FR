---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;appareil;type de données;type de données;type de données;devise;
solution: Experience Platform
title: Type de données de devise
description: En savoir plus sur le type de données XDM par devise.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
TQID: https://experienceleague.adobe.com/SRDNwAGpkD5T6kIDBUijO07vfyk8-CRf1ASBXVCdKoE
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 123
ht-degree: 5%

---

# Type de données [!UICONTROL Currency]

[!UICONTROL Devise] est un type de données XDM standard qui décrit un montant de devise, y compris le type de devise et la date de conversion.

![](../images/data-types/currency.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `amount` | Double | Montant de la devise tel que défini par le `currencyCode`. |
| `conversionDate` | DateTime | Date et heure du moment où la conversion monétaire a été effectuée. |
| `currencyCode` | Chaîne | Code ISO 4217 indiquant le type de devise que `amount` représente. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
