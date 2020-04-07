---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 8 avril 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: b3ee2839412c9949d67c2ae976e3df32fea7731e

---


# Notes de mise à jour d’Adobe Experience Platform

## Date de publication : 8 avril 2020

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