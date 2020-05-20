---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 8 avril 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 5%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 8 avril 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :
* [Services intelligents](#intelligent)

Mises à jour des fonctionnalités existantes :
* [Modèle de données d’expérience (XDM)](#xdm)
* [Gouvernance des données](#governance)
* [Destinations](#destinations)
* [Service confidentialité](#privacy)
* [Sources](#sources)

## Services intelligents {#intelligent}

Les services intelligents permettent aux analystes et aux praticiens du marketing d’exploiter la puissance de l’intelligence artificielle et de l’apprentissage automatique dans les cas d’utilisation de l’expérience client. Cela permet aux analystes marketing de configurer des prédictions spécifiques aux besoins d’une société en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’une expertise en sciences des données. En outre, les spécialistes du marketing peuvent activer des prédictions dans Adobe Experience Cloud, Adobe Experience Platform et les applications tierces.

**Fonctionnalités clés**

| Fonction | Description |
|---|---|
| AI client | L’IA du client permet aux spécialistes du marketing de générer des prévisions client au niveau individuel avec des explications. Grâce à des facteurs influents, l’IA du client peut vous indiquer ce qu’un client est susceptible de faire et pourquoi. En outre, les spécialistes du marketing peuvent tirer parti des prédictions et des connaissances d’IA du client pour personnaliser les expériences client en fournissant les offres et les messages les plus appropriés. |
| Attribution AI | Attribution AI est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés. Grâce à l’API d’attribution, les spécialistes du marketing peuvent mesurer et optimiser les dépenses marketing et publicitaires en comprenant l’impact de chaque interaction client individuelle sur chaque phase du parcours des clients. |

**Problèmes connus**

* Aucun problème connu actuellement.

Pour plus d&#39;informations sur les services intelligents et sur ce qu&#39;ils ont à faire pour l&#39;offre, consultez l&#39;aperçu [des services](../../intelligent-services/home.md)intelligents.

## Système de modèle de données d’expérience (XDM) {#xdm}

La normalisation et l’interopérabilité sont des concepts clés de la plate-forme d’expérience. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes à toute application pour communiquer avec les services d’Adobe Experience Platform. En respectant les normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune offrant des informations d’une manière plus rapide et plus intégrée. Vous pouvez obtenir des informations précieuses sur les actions client, définir des audiences client par le biais de segments et utiliser les attributs client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonction | Description |
| --- | --- |
| Informations d&#39;affichage de remplacement automatiques | Le Registre des Schémas applique automatiquement les valeurs de titre et de description personnalisées configurées dans le `alternateDisplayInfo` descripteur. |
| Restrictions des champs de l’échelle | Le Registre des Schémas n’autorise pas plus de 6 000 champs scalaires dans un seul schéma. |
| Révision des performances | Le Registre des Schémas a été remanié pour mieux répondre aux exigences de la Plate-forme d&#39;expérience. |

**Corrections de bogues**

* Mise à jour de XDM en XED converti afin de prendre en charge un format XED plus propre pour les champs URI imbriqués dans XDM standard.

**Problèmes connus**

* Connu

## Gouvernance des données {#governance}

Adobe Experience Platform Data Governance est une série de stratégies et de technologies utilisées pour gérer les données client et assurer la conformité aux réglementations, restrictions et règles applicables à l’utilisation des données. Il joue un rôle clé dans la plate-forme d’expérience à divers niveaux, notamment le catalogage, le lignage des données, l’étiquetage de l’utilisation des données, les stratégies d’accès aux données et le contrôle d&#39;accès sur les données pour les actions marketing.

La prise en main de la gouvernance des données nécessite une compréhension approfondie des réglementations, obligations contractuelles et stratégies d’entreprise qui s’appliquent à vos données client. À partir de là, les données peuvent être classifiées en appliquant les étiquettes d&#39;utilisation appropriées et leur utilisation peut être contrôlée par la définition de stratégies d&#39;utilisation des données.

La structure DULE simplifie et rationalise le processus de catégorisation des données et de création de stratégies d’utilisation des données par le biais de l’interface utilisateur de la plateforme d’expérience et de l’API DULE Policy Service.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Gérer les stratégies d’utilisation des données dans l’interface utilisateur | Les stratégies d’utilisation des données peuvent désormais être gérées dans l’espace de travail _Stratégies_ de l’interface utilisateur de la plate-forme d’expérience. Pour plus d’informations, consultez le guide [de l’utilisateur](../../data-governance/policies/user-guide.md) de la stratégie. |

**Problèmes connus**

* Aucun.

Pour plus d&#39;informations, consultez la présentation [de la gouvernance des](../../data-governance/home.md)données.


## Destinations {#destinations}

Dans [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations préétablies avec les plateformes de destination qui activent les données pour ces partenaires de manière transparente.

**Nouvelles destinations**

Le CDP en temps réel d’Adobe prend désormais en charge l’activation des données à plus de cinquante extensions de lancement d’Experience Cloud, ce qui permet d’effectuer des analyses, de personnaliser et d’autres cas d’utilisation. Voir ci-dessous pour plus de détails :

| Documentation | Description |
|--- | ---|
| [Types et catégories de destination](/help/rtcdp/destinations/destination-types.md) | Cet article explique la différence entre les connexions et les extensions dans l’interface CDP en temps réel d’Adobe et recommande le moment où utiliser chacune de ces destinations. |
| [Extensions de lancement de plateforme d’expérience](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | Cette page décrit les extensions de lancement, les cas d’utilisation des listes et les liens vers la documentation de chaque extension de lancement dans Adobe Real-time CDP. |

Pour plus d&#39;informations, consultez la présentation [des](/help/rtcdp/destinations/destinations-overview.md)Destinations.

## Service confidentialité {#privacy}

Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d&#39;accéder à vos données personnelles ou de les supprimer de vos entrepôts de données sur demande. Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec Privacy Service, vous pouvez envoyer des demandes d’accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui vous permet de respecter automatiquement les règles de confidentialité légales et organisationnelles.

**Nouvelles fonctionnalités**

| Fonction | Description |
| --- | --- |
| Prise en charge de PDPA | Les demandes de confidentialité peuvent maintenant être créées et suivies en vertu de la Loi sur la protection des données personnelles (PDPA) en Thaïlande. Lorsque vous effectuez des demandes de confidentialité dans l&#39;API, le `regulation` tableau accepte la valeur &quot;pdpa_tha&quot;. |
| Types d’Espace de nommage dans l’interface utilisateur | Vous pouvez désormais spécifier différents types d’espace de nommage dans le Créateur de requêtes de l’interface utilisateur de Privacy Service. Consultez le guide [](../../privacy-service/ui/user-guide.md) d’utilisation pour plus d’informations. |
| Ancienne obsolescence des points de terminaison | L’ancien point de terminaison API (`data/privacy/gdpr`) a été abandonné. |

Problèmes connus

* None (Aucun)

Pour plus d&#39;informations sur Privacy Service, veuillez début en lisant la présentation [](../../privacy-service/home.md)Privacy Service.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plate-forme. Vous pouvez ingérer des données à partir de diverses sources, telles que des applications Adobe, des enregistrements basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent d’authentifier et de vous connecter à des systèmes d’enregistrement externes et à des services de gestion de la relation client, de définir les heures d’exécution d’assimilation et de gérer le débit d’assimilation des données.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ------- | ----------- |
| Prise en charge des API et de l’interface utilisateur pour les bases de données | Nouveaux connecteurs source pour Apache Spark (sur HDInsights), Azure Synapse Analytics, Azure Table Enregistrement, Hive (sur HDInsights) et Phoenix. |
| Prise en charge des API et de l’interface utilisateur pour les applications basées sur les paiements | Nouveaux connecteurs source pour PayPal. |
| Prise en charge des API et de l’interface utilisateur pour les applications basées sur des protocoles | Nouveaux connecteurs source pour Generic OData. |

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur les sources, consultez l’aperçu [des](../../sources/home.md)sources.
