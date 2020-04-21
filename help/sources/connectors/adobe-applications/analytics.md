---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur de données Analytics
topic: overview
translation-type: tm+mt
source-git-commit: 75c446aed75100bd2b5b4a3d365c090cb01dcc69

---


# Connecteur de données Analytics

Adobe Experience Platform vous permet d’assimiler des données Adobe Analytics par le biais d’Analytics Data Connector (ADC). ADC diffuse en temps réel les données collectées par Adobe Analytics vers la plate-forme, en convertissant les données Analytics formatées au format SCDS en champs de modèle de données d’expérience (XDM) pour les utiliser par plate-forme.

Ce donne une vue d’ensemble d’Adobe Analytics et décrit les cas d’utilisation des données Analytics.

## Données Adobe Analytics et Analytics

Adobe Analytics est un puissant moteur d’analyse qui vous permet d’en savoir plus sur vos clients, sur la manière dont ils interagissent avec vos propriétés Web, de déterminer l’efficacité de vos dépenses de marketing numérique et d’identifier les améliorations à apporter. Adobe Analytics gère des milliards de transactions Web par an et ADC vous permet de tirer facilement parti de ces riches données comportementales et d’enrichir le client en temps réel en quelques minutes.

![](./images/analytics-data-experience-platform.png)

À un niveau élevé, Adobe Analytics collecte des données à partir de divers numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (Identification des, Segmentation et Architecture de transformation) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être consommées par le client en temps réel. Dans un processus parallèle à celui mentionné ci-dessus, les mêmes données traitées sont micro-traitées et assimilées dans des jeux de données de plateformes pour la consommation par Data Science Workspace, le service de  de données et d’autres applications de découverte de données.

Pour plus d’informations sur VISTA et les règles de traitement, reportez-vous au  suivant :
* [Présentation des règles VISTA](https://marketing.adobe.com/resources/help/fr_FR/reference/VISTA.html)
* [Règles de traitement - Aperçu](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules.html)

## Modèle de données d’expérience (XDM)

XDM est une spécification publiquement documentée qui fournit des structures et des définitions communes à une application à utiliser pour communiquer avec des services sur Adobe Experience Platform.

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la présentation [du système](../../../xdm/home.md)XDM.

## Comment les champs d’Adobe Analytics sont-ils mappés à XDM ?

Lorsqu’une connexion source est établie pour importer des données Analytics dans la plate-forme d’expérience à l’aide de l’interface utilisateur de la plate-forme, les champs de données sont automatiquement mappés et assimilés dans le client en temps réel en quelques minutes. Pour plus d’informations sur la création d’une connexion source avec Adobe Analytics à l’aide de l’interface utilisateur de la plate-forme, voir le didacticiel [sur le connecteur de données](../../tutorials/ui/create/adobe-applications/analytics.md)Analytics.

Pour plus d’informations sur le mappage des champs entre Analytics et la plateforme d’expérience, consultez le guide de mappage des [champs d’](./mapping/analytics.md) Adobe Analytics.

## Quelle est la latence attendue pour les données Analytics sur la plateforme ?

| Données d’analyse | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données au client en temps réel (A4T **non** activé) | &lt; 2 minutes |
| Nouvelles données pour  client en temps réel (A4T **est** activé) | &lt; 15 minutes |
| Nouvelles données sur Data Lake | &lt; 45 minutes |
| Données de renvoi (13 mois de données ou 10 milliards de , selon la valeur la plus faible) | &lt; 4 semaines |

>[!NOTE] La latence varie selon la configuration du client, les volumes de données et les applications grand public. Par exemple, si l’implémentation d’Analytics est configurée avec `A4T` la latence du pipeline, elle passera à 5-10 minutes.