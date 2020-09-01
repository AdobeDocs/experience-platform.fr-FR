---
keywords: Experience Platform;home;popular topics;Analytics Data Connector;analytics;Analytics
solution: Experience Platform
title: Connecteur de données Analytics
topic: overview
description: Ce document fournit un aperçu d’Analytics et décrit les cas d’utilisation des données Analytics.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 48%

---


# Connecteur de données Analytics

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais du connecteur de données Analytics (ADC, Analytics Data Connector). ADC diffuse les données collectées par [!DNL Analytics] vers [!DNL Platform] en temps réel, en convertissant [!DNL Analytics] des données au format SCDS dans des champs [!DNL Experience Data Model] (XDM) pour une consommation par [!DNL Platform].

This document provides an overview of [!DNL Analytics] and describes the use-cases for [!DNL Analytics] data.

## Adobe Analytics et données Analytics

[!DNL Analytics] est un moteur puissant qui vous permet d’en savoir plus sur vos clients, sur la manière dont ils interagissent avec vos propriétés web, de déterminer l’efficacité de vos dépenses en marketing numérique et d’identifier les améliorations à apporter. [!DNL Analytics] gère des milliers de milliards de transactions web par an et ADC vous permet d&#39;exploiter facilement ces riches données comportementales et de les enrichir en quelques minutes [!DNL Real-time Customer Profile] .

![](./images/analytics-data-experience-platform.png)

At a high level, [!DNL Analytics] collects data from various digital channels and multiple data centers around the world. Une fois les données collectées, les règles VISTA (architecture d’identification, de segmentation et de transformation) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être utilisées par [!DNL Real-time Customer Profile]. In a process parallel to the aforementioned, the same processed data is micro-batched and ingested into Platform datasets for consumption by [!DNL Data Science Workspace], [!DNL Query Service], and other data-discovery applications.

Voir Présentation [des règles de](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules.html) traitement pour plus d’informations sur les règles de traitement.

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes pour qu’une application puisse communiquer avec des services sur [!DNL Experience Platform].

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la [présentation du système XDM](../../../xdm/home.md).

## Comment les champs sont-ils mappés d’Adobe Analytics à XDM ?

When a source connection is established for bringing [!DNL Analytics] data into [!DNL Experience Platform] using the [!DNL Platform] user interface, data fields are automatically mapped and ingested into [!DNL Real-time Customer Profile] within minutes. For instructions on creating a source connection with [!DNL Analytics] using the [!DNL Platform] UI, see the [Analytics data connector tutorial](../../tutorials/ui/create/adobe-applications/analytics.md).

For detailed information on the field mapping that occurs between [!DNL Analytics] and [!DNL Experience Platform], please visit the [Adobe Analytics field mapping](./mapping/analytics.md) guide.

## Quelle est la latence attendue sur Platform pour les données Analytics ?

| Données Analytics | Latence attendue |
| -------------- | ---------------- |
| New data to [!DNL Real-time Customer Profile] (A4T **not** enabled) | &lt; 2 minutes |
| New data to [!DNL Real-time Customer Profile] (A4T **is** enabled) | &lt; 15 minutes |
| Nouvelles données pour le lac de données | &lt; 45 minutes |
| Renvoi des données (13 mois de données ou 10 milliards d’événements, selon la valeur la plus faible) | &lt; 4 semaines |

>[!NOTE]
>
>La latence varie selon la configuration client, les volumes de données et les applications clients. Par exemple, si l’implémentation d’Analytics est configurée avec `A4T`, la latence du pipeline passera à 5-10 minutes.

## Identifiants de Principal dans les données Analytics

Chaque accès du connecteur de données Analytics contient un identifiant Principal qui dépend de l’existence d’un ECID ou d’un AAID. S&#39;il existe un ECID, l&#39;ECID est désigné comme identifiant Principal. S&#39;il y a un AAID, celui-ci est désigné comme Principal.