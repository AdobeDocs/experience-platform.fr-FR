---
keywords: Experience Platform ; accueil ; rubriques populaires ; Connecteur de données Analytics ; analyses ; Analytics
solution: Experience Platform
title: Connecteur de source Adobe Analytics pour les données d’une suite de rapports
topic: aperçu
description: Ce document fournit un aperçu d’Analytics et décrit les cas d’utilisation des données Analytics.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 46%

---


# Connecteur Adobe Analytics pour les données de suite de rapports

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais du connecteur de données Analytics (ADC, Analytics Data Connector). ADC diffuse les données collectées par [!DNL Analytics] en [!DNL Platform] en temps réel, en convertissant les données [!DNL Analytics] au format SCDS en champs [!DNL Experience Data Model] (XDM) pour les utiliser par [!DNL Platform].

Ce document présente un aperçu de [!DNL Analytics] et décrit les cas d&#39;utilisation des données [!DNL Analytics].

## Adobe Analytics et données Analytics

[!DNL Analytics] est un moteur puissant qui vous permet d’en savoir plus sur vos clients, sur la manière dont ils interagissent avec vos propriétés web, de déterminer l’efficacité de vos dépenses en marketing numérique et d’identifier les améliorations à apporter. [!DNL Analytics] gère des milliards de transactions web par an et ADC vous permet de puiser facilement dans ces riches données comportementales et de les enrichir  [!DNL Real-time Customer Profile] en quelques minutes.

![](./images/analytics-data-experience-platform.png)

À un niveau élevé, [!DNL Analytics] collecte les données de divers canaux numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (architecture d’identification, de segmentation et de transformation) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être utilisées par [!DNL Real-time Customer Profile]. Dans un processus parallèle à celui mentionné ci-dessus, les mêmes données traitées sont micro-battues et assimilées à des jeux de données de la plateforme pour consommation par [!DNL Data Science Workspace], [!DNL Query Service] et d&#39;autres applications de découverte de données.

Voir [Présentation des règles de traitement](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules.html) pour plus d’informations sur les règles de traitement.

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes pour qu’une application puisse communiquer avec des services sur [!DNL Experience Platform].

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la [présentation du système XDM](../../../xdm/home.md).

## Comment les champs sont-ils mappés d’Adobe Analytics à XDM ?

Lorsqu&#39;une connexion source est établie pour importer des données [!DNL Analytics] dans [!DNL Experience Platform] à l&#39;aide de l&#39;interface utilisateur [!DNL Platform], les champs de données sont automatiquement mappés et assimilés dans [!DNL Real-time Customer Profile] en quelques minutes. Pour obtenir des instructions sur la création d’une connexion source avec [!DNL Analytics] à l’aide de l’[!DNL Platform] interface utilisateur, consultez le [didacticiel sur le connecteur de données Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Pour obtenir des informations détaillées sur le mappage des champs qui se produit entre [!DNL Analytics] et [!DNL Experience Platform], consultez le guide [Adobe Analytics field mapping](./mapping/analytics.md).

## Quelle est la latence attendue sur Platform pour les données Analytics ?

| Données Analytics | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données à [!DNL Real-time Customer Profile] (A4T **non** activé) | &lt; 2 minutes |
| Nouvelles données à [!DNL Real-time Customer Profile] (A4T **est** activé) | &lt; 15 minutes |
| Nouvelles données pour le lac de données | &lt; 90 minutes |
| Renvoi des données (13 mois de données ou 10 milliards d’événements, selon la valeur la plus faible) | &lt; 4 semaines |

>[!NOTE]
>
>La latence varie selon la configuration client, les volumes de données et les applications clients. Par exemple, si l’implémentation d’Analytics est configurée avec `A4T`, la latence du pipeline passera à 5-10 minutes.

## Identifiants de Principal dans les données Analytics

Chaque accès du connecteur de données Analytics contient un identifiant Principal qui dépend de l’existence d’un ECID ou d’un AAID. S&#39;il existe un ECID, l&#39;ECID est désigné comme identifiant Principal. S&#39;il y a un AAID, celui-ci est désigné comme Principal.