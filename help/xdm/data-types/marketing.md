---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;appareil;type de données;type de données;type de données
solution: Experience Platform
title: Type de données marketing
topic-legacy: overview
description: Ce document présente un aperçu du type de données Marketing XDM.
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 7%

---


#  Type de données marketing

 Marketingest un type de données XDM standard qui décrit les activités marketing principales avec un point de contact particulier.

![](../images/data-types/marketing.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignGroup` | Chaîne | Nom du groupe de campagnes (dans les cas où plusieurs campagnes sont regroupées comme `50%_DISCOUNT`). |
| `campaignName` | Chaîne | Nom de la campagne marketing, par exemple `50%_DISCOUNT_USA` ou `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Chaîne | Code de suivi pouvant être utilisé pour identifier la campagne marketing à laquelle l’événement est associé. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
