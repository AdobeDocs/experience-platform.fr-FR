---
keywords: Experience Platform;accueil;rubriques populaires;Connecteur source Analytics;analytics;Analytics
solution: Experience Platform
title: Connecteur source Adobe Analytics pour les données d’une suite de rapports
topic-legacy: overview
description: Ce document présente Analytics et décrit les cas d’utilisation des données Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 26%

---

# Connecteur source Adobe Analytics pour les données de suite de rapports

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais du connecteur source Analytics. Le [!DNL Analytics] connecteur source diffuse en temps réel les données collectées par [!DNL Analytics] vers Platform, en convertissant les données [!DNL Analytics] au format SCDS en champs [!DNL Experience Data Model] (XDM) à des fins d’utilisation par Platform.

Ce document présente [!DNL Analytics] et décrit les cas d’utilisation des données [!DNL Analytics].

## Adobe Analytics et données Analytics

[!DNL Analytics] est un moteur puissant qui vous aide à en savoir plus sur vos clients, sur la manière dont ils interagissent avec vos propriétés web, à déterminer l’efficacité de vos dépenses de marketing numérique et à identifier les améliorations à apporter. [!DNL Analytics] gère des milliards de transactions web par an et le connecteur  [!DNL Analytics] source vous permet d’exploiter facilement ces riches données comportementales et d’enrichir le  [!DNL Real-time Customer Profile] en quelques minutes.

![](./images/analytics-data-experience-platform.png)

À un haut niveau, [!DNL Analytics] collecte des données à partir de divers canaux numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (Visitor Identification, Segmentation and Transformation Architecture) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être utilisées par [!DNL Real-time Customer Profile]. Dans un processus parallèle, les mêmes données traitées sont microtraitées par lot et ingérées dans des jeux de données Platform pour être utilisées par [!DNL Data Science Workspace], [!DNL Query Service] et d’autres applications de découverte de données.

Pour plus d’informations sur les règles de traitement, consultez la [présentation des règles de traitement](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) .

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes pour qu’une application puisse communiquer avec des services sur Experience Platform.

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la [présentation du système XDM](../../../xdm/home.md).

## Comment les champs sont-ils mappés d’Adobe Analytics à XDM ?

Lorsqu’une connexion source est établie pour importer des données [!DNL Analytics] dans Experience Platform à l’aide de l’interface utilisateur de Platform, les champs de données sont automatiquement mappés et ingérés dans [!DNL Real-time Customer Profile] en quelques minutes. Pour obtenir des instructions sur la création d’une connexion source avec [!DNL Analytics] à l’aide de l’interface utilisateur de Platform, consultez le [tutoriel sur le connecteur source Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Pour plus d’informations sur le mappage des champs entre [!DNL Analytics] et l’Experience Platform, consultez le guide [Mapping des champs Adobe Analytics](./mapping/analytics.md) .

## Quelle est la latence attendue sur Platform pour les données Analytics ?

| Données Analytics | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données pour [!DNL Real-time Customer Profile] (A4T **not** activé) | &lt; 2 minutes |
| Nouvelles données pour [!DNL Real-time Customer Profile] (A4T **is** activé) | &lt; 15 minutes |
| Nouvelles données pour le lac de données | &lt; 90 minutes |
| Renvoi des données (13 mois de données ou 10 milliards d’événements, selon la valeur la plus faible) | &lt; 4 semaines |

>[!NOTE]
>
>La latence varie selon la configuration client, les volumes de données et les applications clients. Par exemple, si l’implémentation de [!DNL Analytics] est configurée avec `A4T`, la latence du pipeline passera à 5-10 minutes.

## Identifiants Principal dans les données [!DNL Analytics]

Chaque accès du connecteur source [!DNL Analytics] contient un identifiant Principal qui dépend de l’existence ou non d’un ECID ou d’un AAID. S’il existe un ECID, celui-ci est désigné comme l’identifiant Principal. S’il existe un AAID, celui-ci est désigné comme la Principale.
