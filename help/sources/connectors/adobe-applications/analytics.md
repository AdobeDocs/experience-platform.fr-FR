---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur de données Analytics
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 97%

---


# Connecteur de données Analytics

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais du connecteur de données Analytics (ADC, Analytics Data Connector). Le connecteur de données Analytics diffuse en temps réel les données collectées par Adobe Analytics vers Platform, en convertissant les données Analytics au format SCDS en champs du modèle de données d’expérience (XDM) utilisables par Platform.

Ce document fournit une présentation d’Adobe Analytics et décrit des cas d’utilisation des données Analytics.

## Adobe Analytics et données Analytics

Adobe Analytics est un moteur puissant qui vous permet d’en savoir plus sur vos clients, sur la manière dont ils interagissent avec vos propriétés web, de déterminer l’efficacité de vos dépenses en marketing numérique et d’identifier les améliorations à apporter. Adobe Analytics gère des trillions de transactions web par an et le connecteur de données Analytics vous permet de facilement tirer parti de ces riches données comportementales et d’enrichir le profil client en temps réel en quelques minutes.

![](./images/analytics-data-experience-platform.png)

À un niveau élevé, Adobe Analytics collecte des données à partir de divers canaux numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (architecture d’identification, de segmentation et de transformation) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être utilisées par Real-time Customer Profile. Dans un processus parallèle, les mêmes données traitées sont microtraitées par lot et ingérées dans des jeux de données Platform pour être utilisées dans Data Science Workspace, Query Service et d’autres applications de découverte de données.

Voir Présentation [des règles de](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules.html) traitement pour plus d’informations sur les règles de traitement.

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes pour qu’une application puisse communiquer avec des services sur Adobe Experience Platform.

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la [présentation du système XDM](../../../xdm/home.md).

## Comment les champs sont-ils mappés d’Adobe Analytics à XDM ?

Lorsqu’une connexion source est établie pour importer des données Analytics dans Experience Platform à l’aide de l’interface utilisateur de Platform, les champs de données sont automatiquement mappés et ingérés par Real-time Customer Profile en quelques minutes. Pour plus d’informations sur la création d’une connexion source avec Adobe Analytics à l’aide de l’interface utilisateur de Platform, consultez le [tutoriel sur le connecteur de données Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Pour plus d’informations sur le mappage des champs entre Analytics et Experience Platform, consultez le guide sur le [mappage des champs Adobe Analytics](./mapping/analytics.md).

## Quelle est la latence attendue sur Platform pour les données Analytics ?

| Données Analytics | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données pour Real-time Customer Profile (A4T **non activé**) | &lt; 2 minutes |
| Nouvelles données pour Real-time Customer Profile (A4T **activé**) | &lt; 15 minutes |
| Nouvelles données pour le lac de données | &lt; 45 minutes |
| Renvoi des données (13 mois de données ou 10 milliards d’événements, selon la valeur la plus faible) | &lt; 4 semaines |

>[!NOTE]
>
>La latence varie selon la configuration client, les volumes de données et les applications clients. Par exemple, si l’implémentation d’Analytics est configurée avec `A4T`, la latence du pipeline passera à 5-10 minutes.