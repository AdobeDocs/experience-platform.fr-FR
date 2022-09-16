---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;appareil;type de données;type de données;type de données
solution: Experience Platform
title: Type de données marketing
topic-legacy: overview
description: Ce document présente un aperçu du type de données Marketing XDM.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 7%

---

# [!UICONTROL Marketing] type de données

[!UICONTROL Marketing] est un type de données XDM standard qui décrit les activités marketing principales avec un point de contact particulier.

![](../images/data-types/marketing.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignGroup` | Chaîne | Nom du groupe de campagnes (dans les cas où plusieurs campagnes sont regroupées comme `50%_DISCOUNT`). |
| `campaignName` | Chaîne | Nom de la campagne marketing, tel que `50%_DISCOUNT_USA` ou `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Chaîne | Code de suivi pouvant être utilisé pour identifier la campagne marketing à laquelle l’événement est associé. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
