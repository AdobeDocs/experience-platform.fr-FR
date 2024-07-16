---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;appareil;type de données;type de données;type de données
solution: Experience Platform
title: Type de données marketing
description: Découvrez le type de données Marketing XDM.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---

# Type de données [!UICONTROL Marketing]

[!UICONTROL Marketing] est un type de données XDM standard qui décrit les activités marketing actives avec un point de contact particulier.

![](../images/data-types/marketing.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignGroup` | Chaîne | Nom du groupe de campagnes (dans les cas où plusieurs campagnes sont regroupées comme `50%_DISCOUNT`). |
| `campaignName` | Chaîne | Nom de la campagne marketing, par exemple `50%_DISCOUNT_USA` ou `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Chaîne | Code de suivi pouvant être utilisé pour identifier la campagne marketing à laquelle l’événement est associé. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
