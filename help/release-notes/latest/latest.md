---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 8 avril 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: dc1c9b7dd9ff4c8b20de96e4ee123d90be4580cc

---


# Notes de mise à jour d’Adobe Experience Platform

## Date de publication : 8 avril 2020

## Système XDM (Experience Data Model)

La normalisation et l’interopérabilité sont les concepts clés de la plateforme d’expérience. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des  pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes à toute application pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des  de  clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Infos d’affichage de remplacement automatiques | Le Registre des  applique automatiquement les valeurs de titre et de description personnalisées configurées dans le `alternateDisplayInfo` descripteur. |
| Restrictions des champs de l’échelle | Le Registre des  ne permet pas plus de 6000 champs scalaires dans un seul  de. |
| Révision des performances | Le Registre des  a été remanié pour mieux répondre aux exigences de la Plateforme d’expérience. |

**Corrections de bogues**

* Mise à jour de XDM en XED converti pour prendre en charge un format XED plus propre pour les champs URI imbriqués dans XDM standard.

**Problèmes connus**

* Connu

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


## Destinations

Dans [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations prédéfinies avec les plateformes de destination qui activent les données de manière transparente vers ces partenaires.

### Nouvelles destinations

Le CDP en temps réel d’Adobe prend désormais en charge les données  les de plus de cinquante extensions de lancement d’Experience Cloud, ce qui permet d’activer les analyses, la personnalisation et d’autres utilisations. Voir ci-dessous pour plus de détails :

| Documentation | Description |
|--- | ---|
| [Types de destination et  de](/help/rtcdp/destinations/destination-types.md) | Cet article explique la différence entre les connexions et les extensions dans l’interface CDP en temps réel d’Adobe et recommande quand utiliser chacune de ces destinations. |
| [Extensions de lancement de plateforme d’expérience](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | Cette page explique ce que sont les extensions de lancement,  les cas d’utilisation pour les utiliser et des liens vers la documentation pour chaque extension de lancement dans Adobe Real-time CDP. |

Pour plus d&#39;informations, reportez-vous à la présentation [des](/help/rtcdp/destinations/destinations-overview.md)Destinations.

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