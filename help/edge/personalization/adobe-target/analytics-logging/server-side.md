---
title: Journalisation côté serveur des données A4T dans le SDK Web Platform
description: Découvrez comment activer la journalisation côté serveur pour Adobe Analytics for Target (A4T) à l’aide du SDK Web Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;plateforme;journalisation
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Journalisation côté serveur des données A4T dans le SDK Web Platform

Le SDK Web de Adobe Experience Platform vous permet de mettre en oeuvre la fonctionnalité Adobe Analytics for Target (A4T) sur Platform Edge Network. Lorsque la journalisation côté serveur est activée, tous les accès Analytics envoyés par le biais du réseau Edge sont augmentés avec les détails Target côté serveur, sans avoir à passer par le processus d’assemblage d’accès.

La journalisation côté serveur d’Analytics est activée lorsque Analytics est activé dans la configuration de la chaîne de données :

![Configuration de la banque de données Analytics activée](../assets/enable-analytics-datastream.png)

Le diagramme suivant montre comment les données transitent par le système lorsque la journalisation Analytics côté serveur est activée :

![Flux de journalisation côté serveur](../assets/analytics-server-side-logging.png)

## Étapes suivantes

Ce guide décrit la journalisation côté serveur des données A4T dans le SDK Web. Consultez le guide sur la [journalisation côté client](./client-side.md) pour plus d’informations sur la gestion des données A4T côté client.
