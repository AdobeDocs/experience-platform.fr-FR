---
keywords: Experience Platform ; accueil ; rubriques populaires ; Analytics Source Connector ; analytics ; Analytics
solution: Experience Platform
title: Connecteur de source Adobe Analytics pour les données d’une suite de rapports
topic-legacy: overview
description: Ce document fournit un aperçu d’Analytics et décrit les cas d’utilisation des données Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
translation-type: tm+mt
source-git-commit: af5ad975bbfd6a67fe66c90e33da1365d49c8899
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 28%

---

# Connecteur source Adobe Analytics pour les données de la suite de rapports

Adobe Experience Platform vous permet d’assimiler des données Adobe Analytics via le connecteur source Analytics. Le connecteur source [!DNL Analytics] diffuse en temps réel les données collectées par [!DNL Analytics] vers la plate-forme, en convertissant les données [!DNL Analytics] au format SCDS dans les champs [!DNL Experience Data Model] (XDM) pour consommation par plate-forme.

Ce document présente un aperçu de [!DNL Analytics] et décrit les cas d&#39;utilisation des données [!DNL Analytics].

## Adobe Analytics et données Analytics

[!DNL Analytics] est un puissant moteur qui vous aide à en savoir plus sur vos clients, comment ils interagissent avec vos propriétés web, à déterminer où sont les dépenses de marketing numérique et à identifier les améliorations à apporter. [!DNL Analytics] gère des milliards de transactions web par an et le connecteur  [!DNL Analytics] source vous permet de puiser facilement dans ces riches données comportementales et d&#39;enrichir les données  [!DNL Real-time Customer Profile] en quelques minutes.

![](./images/analytics-data-experience-platform.png)

À un niveau élevé, [!DNL Analytics] collecte les données de divers canaux numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (Identification des Visiteurs, Segmentation et Architecture de transformation) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être utilisées par [!DNL Real-time Customer Profile]. Dans un processus parallèle à celui mentionné ci-dessus, les mêmes données traitées sont micro-battues et assimilées à des jeux de données de la plateforme pour consommation par [!DNL Data Science Workspace], [!DNL Query Service] et d&#39;autres applications de découverte de données.

Pour plus d&#39;informations sur les règles de traitement, consultez l&#39;[aperçu des règles de traitement](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules.html).

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes pour qu’une application puisse communiquer avec des services sur Experience Platform.

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la [présentation du système XDM](../../../xdm/home.md).

## Comment les champs sont-ils mappés d’Adobe Analytics à XDM ?

Lorsqu&#39;une connexion source est établie pour importer des données [!DNL Analytics] dans l&#39;Experience Platform à l&#39;aide de l&#39;interface utilisateur de la plate-forme, les champs de données sont automatiquement mappés et assimilés dans [!DNL Real-time Customer Profile] en quelques minutes. Pour obtenir des instructions sur la création d’une connexion source avec [!DNL Analytics] à l’aide de l’interface utilisateur de la plate-forme, consultez le [didacticiel sur le connecteur source Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Pour plus d’informations sur le mappage des champs qui se produit entre [!DNL Analytics] et l’Experience Platform, voir le guide de mappage des champs [Adobe Analytics](./mapping/analytics.md).

## Quelle est la latence attendue sur Platform pour les données Analytics ?

| Données Analytics | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données à [!DNL Real-time Customer Profile] (A4T **non** activé) | &lt; 2 minutes |
| Nouvelles données à [!DNL Real-time Customer Profile] (A4T **est** activé) | &lt; 15 minutes |
| Nouvelles données pour le lac de données | &lt; 90 minutes |
| Renvoi des données (13 mois de données ou 10 milliards d’événements, selon la valeur la plus faible) | &lt; 4 semaines |

>[!NOTE]
>
>La latence varie selon la configuration client, les volumes de données et les applications clients. Par exemple, si l&#39;implémentation [!DNL Analytics] est configurée avec `A4T` la latence de Pipeline passera à 5-10 minutes.

## Identifiants Principal dans les données [!DNL Analytics]

Chaque accès à partir du connecteur source [!DNL Analytics] contient un identifiant Principal qui dépend de l&#39;existence d&#39;un ECID ou d&#39;un AAID. S&#39;il existe un ECID, l&#39;ECID est désigné comme identifiant Principal. S&#39;il y a un AAID, celui-ci est désigné comme Principal.
