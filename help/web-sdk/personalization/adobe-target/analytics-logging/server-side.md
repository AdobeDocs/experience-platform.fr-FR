---
title: Journalisation côté serveur des données A4T dans le SDK Web Platform
description: Découvrez comment activer la journalisation côté serveur pour Adobe Analytics for Target (A4T) à l’aide du SDK Web Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;plateforme;journalisation
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 1%

---

# Journalisation côté serveur des données A4T dans le SDK Web Platform

Le SDK Web de Adobe Experience Platform vous permet de mettre en oeuvre la fonctionnalité Adobe Analytics for Target (A4T) sur Platform Edge Network. Lorsque la journalisation côté serveur est activée, tous les accès Analytics envoyés par l’intermédiaire de l’Edge Network sont augmentés avec les détails de Target côté serveur, sans avoir à passer par le processus d’assemblage d’accès.

La journalisation côté serveur d’Analytics est activée lorsque Analytics est activé dans la configuration de la chaîne de données :

![Configuration du flux de données Analytics activée](../assets/enable-analytics-datastream.png)

Le diagramme suivant montre comment les données transitent par le système lorsque la journalisation Analytics côté serveur est activée :

![Flux de journalisation côté serveur](../assets/analytics-server-side-logging.png)

## Étapes suivantes

Ce guide décrit la journalisation côté serveur des données A4T dans le SDK Web. Pour plus d’informations sur la gestion des données A4T côté client, consultez le guide sur la [journalisation côté client](./client-side.md) .
