---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 8 avril 2020
doc-type: release notes
last-update: April 7, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 7335a258a53d2685933b401dc4cd00bb60aa6c07

---


# Notes de mise à jour d’Adobe Experience Platform

## Date de publication : 8 avril 2020

## Gouvernance des données

La gouvernance des données d’Adobe Experience Platform est une série de stratégies et de technologies utilisées pour gérer les données des clients et garantir la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. Il joue un rôle clé dans Experience Platform à différents niveaux, notamment le catalogage, le lignage des données, l’étiquetage de l’utilisation des données, les stratégies d’accès aux données et les  sur les données pour les actions marketing.

La prise en main de la gouvernance des données nécessite une compréhension approfondie des réglementations, des obligations contractuelles et des stratégies d’entreprise qui s’appliquent aux données client. À partir de là, les données peuvent être classifiées en appliquant les étiquettes d’utilisation des données appropriées, et leur utilisation peut être contrôlée par la définition des stratégies d’utilisation des données.

La structure DULE simplifie et rationalise le processus de catégorisation des données et de création de stratégies d’utilisation des données via l’interface utilisateur de la plateforme d’expérience et l’API DULE Policy Service.

### Nouvelles fonctionnalités

| Fonction | Description |
| -----------| ---------- |
| Gestion des stratégies d’utilisation des données dans l’interface utilisateur | Les stratégies d’utilisation des données peuvent désormais être gérées dans l’espace de travail _Stratégies_ de l’interface utilisateur de la plateforme d’expérience. Pour plus d’informations, consultez le guide [de l’utilisateur](../../data-governance/policies/user-guide.md) des stratégies. |

**Problèmes connus**

* Aucun.

Pour plus d’informations, consultez la présentation [de la gouvernance des](../../data-governance/home.md)données.

## Services intelligents

Les services intelligents permettent aux analystes et aux praticiens du marketing d’exploiter la puissance de l’intelligence artificielle et de l’apprentissage automatique dans les cas d’utilisation de l’expérience client. Cela permet aux analystes marketing de configurer des prédictions spécifiques aux besoins d’un en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’expertise en sciences des données. En outre, les spécialistes du marketing peuvent activer les prédictions dans Adobe Experience Cloud, Adobe Experience Platform et les applications tierces.

**Fonctionnalités clés**

| Fonction | Description |
|---|---|
| AI client | L’IA du client permet aux spécialistes du marketing de générer des prévisions client au niveau individuel avec des explications. Avec l’aide de facteurs influents, l’IA du client peut vous dire ce qu’un client est susceptible de faire et pourquoi. En outre, les spécialistes du marketing peuvent tirer parti des prédictions et des informations sur l’IA du client pour personnaliser les expériences du client en diffusant les  et les messages  les plus appropriés. |
| Attribution AI | Attribution AI est un service d’attribution algorithmique à plusieurs qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés. Grâce à l’API d’attribution, les marketeurs peuvent mesurer et optimiser les dépenses publicitaires et marketing en comprenant l’impact de chaque interaction client sur chaque phase du parcours des clients. |

**Problèmes connus**

* Aucun problème connu pour le moment.

Pour plus d’informations sur les services intelligents et sur ce qu’ils doivent faire pour  , voir l’aperçu [des services](../../intelligent-services/home.md)intelligents.

## Service confidentialité

Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d&#39;accéder à vos données personnelles ou de les supprimer de vos entrepôts de données sur demande. Le service de confidentialité d’Adobe Experience Platform fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec Privacy Service, vous pouvez envoyer des demandes d’accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui facilite la conformité automatisée aux réglementations légales et de confidentialité de l’entreprise.

**Nouvelles fonctionnalités**

| Fonction | Description |
| --- | --- |
| Prise en charge de PDPA | Les demandes de protection de la vie privée peuvent maintenant être créées et suivies en vertu de la Loi sur la protection des données personnelles (PDPA) en Thaïlande. Lors de l’exécution de demandes de confidentialité dans l’API, le `regulation` tableau accepte la valeur &quot;pdpa_tha&quot;. |
|  types de  de dans l’interface utilisateur | Vous pouvez désormais spécifier différents types de  de  dans le Créateur de requêtes dans l’interface utilisateur de Privacy Service. Pour plus d’informations, consultez le guide [d’utilisation](../../privacy-service/ui/user-guide.md) . |
| Ancienne dépréciation du point de fin | L’ancien point de terminaison API (`data/privacy/gdpr`) a été abandonné. |

Problèmes connus

* None (Aucun)

Pour plus d&#39;informations sur Privacy Service, veuillez  en lisant la présentation [](../../privacy-service/home.md)Privacy Service.

## Sources

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plateforme. Vous pouvez assimiler des données à partir de diverses sources, telles que des applications Adobe, des  basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des systèmes de  et des services de gestion de la relation client externes, de définir les heures d&#39;exécution de l&#39;assimilation et de gérer le débit d&#39;assimilation des données.

### Nouvelles fonctionnalités

| Fonction | Description |
| ------- | ----------- |
| Prise en charge des API et de l’interface utilisateur pour les bases de données | Nouveaux connecteurs source pour Apache Spark (sur HDInsights), Azure Synapse Analytics, Azure Table  , Hive (sur HDInsights) et Phoenix. |
| Prise en charge des API et de l’interface utilisateur pour les applications basées sur les paiements | Nouveaux connecteurs source pour PayPal. |
| Prise en charge des API et de l’interface utilisateur pour les applications basées sur des protocoles | Nouveaux connecteurs source pour Generic OData. |

### Problèmes connus

* None (Aucun)

For more information about sources, see the [sources overview](../../source-connectors/home.md).