---
title: Journalisation côté serveur des données A4T dans Experience Platform Web SDK
description: Découvrez comment activer la journalisation côté serveur pour Adobe Analytics for Target (A4T) à l’aide d’Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;journalisation;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# Journalisation côté serveur des données A4T dans Experience Platform Web SDK

Adobe Experience Platform Web SDK vous permet de mettre en œuvre la fonctionnalité Adobe Analytics for Target (A4T) sur Experience Platform Edge Network. Lorsque la journalisation côté serveur est activée, tous les accès Analytics envoyés par l’intermédiaire d’Edge Network sont complétés avec les détails de Target côté serveur, sans avoir à passer par le processus d’assemblage des accès.

La journalisation côté serveur pour Analytics est activée lorsqu’Analytics est activé dans la configuration du flux de données :

![Configuration de train de données Analytics activée](../assets/enable-analytics-datastream.png)

Le diagramme suivant montre le flux de données dans le système lorsque la journalisation Analytics côté serveur est activée :

![Flux de journalisation côté serveur](../assets/analytics-server-side-logging.png)

## Étapes suivantes

Ce guide couvrait la journalisation côté serveur pour les données A4T dans le Web SDK. Pour plus d’informations sur la gestion des données A4T côté client[&#128279;](./client-side.md) consultez le guide sur la  journalisation côté client .
