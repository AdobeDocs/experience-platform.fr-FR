---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 8 avril 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 3f3704cc1e11a4d11278a34800c8bfdc24a80753

---


# Notes de mise à jour d’Adobe Experience Platform

## Date de publication : 8 avril 2020

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

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->