---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;appareil;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données marketing
description: En savoir plus sur le type de données XDM marketing.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
TQID: https://experienceleague.adobe.com/9U00ZEnrtu9MlcZ1C510WkJhWtm9H5SQVndRUgKDtvU
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 135
ht-degree: 5%

---

# Type de données [!UICONTROL Marketing]

[!UICONTROL Marketing] est un type de données XDM standard qui décrit les activités marketing actives avec un point de contact particulier.

![](../images/data-types/marketing.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignGroup` | Chaîne | Nom du groupe de campagnes (dans les cas où plusieurs campagnes sont regroupées comme `50%_DISCOUNT`). |
| `campaignName` | Chaîne | Nom de la campagne marketing, tel que `50%_DISCOUNT_USA` ou `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Chaîne | Code de suivi qui peut être utilisé pour identifier la campagne marketing à laquelle l’événement est associé. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
