---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur de données Analytics
topic: overview
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Connecteur de données Analytics

Adobe Experience Platform vous permet d’assimiler des données Adobe Analytics via le connecteur de données Analytics (ADC). ADC diffuse en temps réel les données collectées par Adobe Analytics vers la plate-forme, en convertissant des données Analytics formatées pour SCDS en champs de modèle de données d’expérience (XDM) pour les utiliser par plate-forme.

Ce document fournit un aperçu d’Adobe Analytics et décrit les cas d’utilisation des données Analytics.

## Données Adobe Analytics et Analytics

Adobe Analytics est un puissant moteur d’analyse qui vous permet d’en savoir plus sur vos clients, comment ils interagissent avec vos propriétés Web, de déterminer où sont les dépenses de marketing numérique et d’identifier les améliorations à apporter. Adobe Analytics gère des milliers de milliards de transactions Web par an et ADC vous permet de tirer facilement parti de ces riches données comportementales et d’enrichir le Profil client en temps réel en quelques minutes.

![](./images/analytics-data-experience-platform.png)

À un niveau élevé, Adobe Analytics collecte des données à partir de divers canaux numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (Visiteur Identification, Segmentation and Transformation Architecture) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être consommées par le Profil client en temps réel. Dans un processus parallèle à celui mentionné ci-dessus, les mêmes données traitées sont micro-battues et assimilées à des jeux de données de plateformes pour être consommées par Data Science Workspace, Requête Service et d’autres applications de découverte de données.

Voir Présentation [des règles de](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/processing-rules/processing-rules.html) traitement pour plus d’informations sur les règles de traitement.

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions communes à une application à utiliser pour communiquer avec des services sur Adobe Experience Platform.

Le respect des normes XDM permet d&#39;intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la présentation [du système](../../../xdm/home.md)XDM.

## Comment les champs d’Adobe Analytics sont-ils mappés à XDM ?

Lorsqu’une connexion source est établie pour importer des données Analytics dans la plate-forme d’expérience à l’aide de l’interface utilisateur de la plate-forme, les champs de données sont automatiquement mappés et ingérés dans le Profil client en temps réel en quelques minutes. Pour obtenir des instructions sur la création d’une connexion source avec Adobe Analytics à l’aide de l’interface utilisateur de la plate-forme, voir le didacticiel [sur le connecteur de données](../../tutorials/ui/create/adobe-applications/analytics.md)Analytics.

Pour obtenir des informations détaillées sur le mappage des champs qui se produit entre Analytics et la plate-forme d’expérience, consultez le guide de mappage des [champs d’](./mapping/analytics.md) Adobe Analytics.

## Quelle est la latence attendue pour les données Analytics sur la plate-forme ?

| Données d’analyse | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données au Profil client en temps réel (A4T **non** activé) | &lt; 2 minutes |
| Nouvelles données au Profil client en temps réel (A4T **est** activé) | &lt; 15 minutes |
| Nouvelles données sur Data Lake | &lt; 45 minutes |
| Données de renvoi (13 mois de données ou 10 milliards de événements, selon la valeur la plus faible) | &lt; 4 semaines |

>[!NOTE] La latence varie en fonction de la configuration du client, des volumes de données et des applications grand public. Par exemple, si la mise en oeuvre d’Analytics est configurée avec `A4T` la latence du pipeline, elle passera à 5-10 minutes.