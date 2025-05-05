---
title: Journalisation d’Adobe Analytics for Target (A4T) dans Experience Platform Web SDK
description: Découvrez comment contrôler la collecte des données Adobe Analytics for Target (A4T) à l’aide de la SDK Web d’Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;journalisation;analytics;sdk;sdk web;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# Connexion à Adobe Analytics for Target (A4T) dans Experience Platform Web SDK

Lorsque vous utilisez Adobe Target pour la personnalisation, vous pouvez choisir le système à utiliser pour la mesure des performances. Chaque [activité Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=fr) vous permet de choisir entre les rapports Target et les rapports Adobe Analytics.

Si vous utilisez la création de rapports Analytics, Adobe Target doit communiquer les informations suivantes à Analytics :

* Quelle activité Adobe Target vos visiteurs ont-ils saisie ?
* Quelle expérience ont-ils vécue ?
* Quelle conversion a été atteinte

Adobe Experience Platform Web SDK prend en charge deux types de journalisation Analytics pour les cas d’utilisation Analytics for Target (A4T) :

| Méthode de consignation | Description |
| --- | --- |
| Journalisation d’Analytics côté serveur | Tous les accès Analytics envoyés par l’intermédiaire d’Edge Network sont complétés avec les détails de Target côté serveur, sans avoir à passer par le processus d’assemblage des accès. |
| Journalisation d’Analytics côté client | Les données de la cible sont renvoyées côté client, ce qui vous permet d’augmenter et d’envoyer manuellement des données à Analytics à l’aide de l’[API Data Insertion](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=fr). |

La méthode de journalisation est déterminée par le fait qu’Adobe Analytics soit ou non activé sur le [flux de données](../../../../datastreams/overview.md) que vous avez configuré :

![Flux de décision de la méthode de journalisation](../assets/analytics-logging.png)

## Étapes suivantes

Ce document présente brièvement les différentes méthodes de journalisation des données A4T dans le SDK Web. Pour plus d’informations sur chacune de ces méthodes, consultez la documentation suivante :

* [Journalisation côté serveur des données A4T dans Experience Platform Web SDK](./server-side.md)
* [Journalisation côté client pour les données A4T dans Experience Platform Web SDK](./client-side.md)
