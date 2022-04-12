---
title: Journalisation d’Adobe Analytics for Target (A4T) dans le SDK Web Platform
description: Découvrez comment contrôler la collecte de données Adobe Analytics for Target (A4T) à l’aide du SDK Web Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;journalisation;analytics;sdk;sdk web;
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---


# Connexion à Adobe Analytics for Target (A4T) dans le SDK Web de Platform

Lorsque vous utilisez Adobe Target pour la personnalisation, vous pouvez choisir le système à utiliser pour la mesure des performances. Chaque [Activité Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) vous permet de choisir entre les rapports Target et Adobe Analytics.

Si vous utilisez la création de rapports Analytics, Adobe Target doit communiquer les éléments suivants à Analytics :

* Activité Adobe Target entrée par vos visiteurs
* Quelle expérience ils ont vue
* Quelle conversion a été atteinte ?

Le SDK Web de Adobe Experience Platform prend en charge deux types de journalisation Analytics pour Analytics for Target (A4T) :

| Méthode de journalisation | Description |
| --- | --- |
| Journalisation Analytics côté serveur | Tous les accès Analytics envoyés par l’intermédiaire du réseau Edge sont augmentés avec les détails de Target côté serveur, sans avoir à passer par le processus d’assemblage d’accès. |
| Journalisation des analyses côté client | Les données Target sont renvoyées côté client, ce qui vous permet d’augmenter et d’envoyer manuellement les données à Analytics à l’aide de la variable [API d’insertion de données](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

La méthode de journalisation est déterminée par l’activation ou non d’Adobe Analytics sur votre [datastream](../../../fundamentals/datastreams.md):

![Flux de décision de la méthode de journalisation](../assets/analytics-logging.png)

## Étapes suivantes

Ce document présente brièvement les différentes méthodes de journalisation des données A4T dans le SDK Web. Pour plus d’informations sur chacune de ces méthodes, consultez la documentation suivante :

* [Journalisation côté serveur des données A4T dans le SDK Web Platform](./server-side.md)
* [Journalisation côté client des données A4T dans le SDK Web Platform](./client-side.md)
