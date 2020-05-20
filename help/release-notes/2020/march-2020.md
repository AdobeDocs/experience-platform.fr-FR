---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 11 mars 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 8%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 11 mars 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [Gouvernance des données](#governance)
* [Incorporation de données](#ingestion)
* [Destinations](#destinations)
* [Service d’identité](#identity)
* [Sources](#sources)

## Gouvernance des données {#governance}

Experience Platform permet aux sociétés de rassembler les données de plusieurs systèmes d’entreprise afin de mieux permettre aux spécialistes du marketing d’identifier, de comprendre et d’impliquer les clients. La plate-forme d’expérience comprend une infrastructure de gouvernance des données de bout en bout, y compris l’étiquetage et l’application de l’utilisation des données (DULE), afin d’assurer l’utilisation appropriée des données dans la plate-forme et lors du partage entre les systèmes.

Adobe Experience Platform Data Governance est une série de stratégies et de technologies utilisées pour gérer les données client et assurer la conformité aux réglementations, restrictions et règles applicables à l’utilisation des données. Il joue un rôle clé dans la plate-forme d’expérience à divers niveaux, notamment le catalogage, le lignage des données, l’étiquetage de l’utilisation des données, les stratégies d’accès aux données et le contrôle d&#39;accès sur les données pour les actions marketing.

**Nouvelles fonctionnalités**

>[!NOTE] Certaines des nouvelles fonctionnalités suivantes sont actuellement en version bêta et ne sont pas disponibles pour tous les utilisateurs. Les fonctionnalités bêta peuvent être modifiées.

| Fonction | Description |
| ------- | ----------- |
| Application automatisée des règles d’utilisation des données pour la plateforme de données client en temps réel | Les stratégies d’utilisation des données sont désormais appliquées dans le processus d’activation des données vers les destinations. La gouvernance des données est également intégrée et appliquée lorsque des modifications affectent des activations existantes (telles que les modifications apportées aux étiquettes de jeux de données, aux stratégies de fusion, aux définitions de segment, etc.). |
| Plage de données pour l&#39;application | Lorsqu’une stratégie d’utilisation des données est violée dans le CDP en temps réel, l’interface utilisateur affiche une notification qui contient des informations de lignage de données pour aider l’utilisateur à comprendre pourquoi les stratégies ont été violées et ce qu’il peut faire pour résoudre la violation. |


**Problèmes connus**

* None (Aucun)

Pour plus d’informations sur la gouvernance des données, voir l’aperçu [de la gouvernance des](../../data-governance/home.md)données.

## Incorporation de données {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’assimiler n’importe quel type de données et de latence. L’intégration des données de la plate-forme Adobe Experience Platform offre plusieurs alternatives pour l’assimilation des données, notamment les API de lot, les API de diffusion en continu, les connecteurs Adobe natifs, les partenaires d’intégration des données ou l’interface utilisateur de la plate-forme Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonction | Description |
|------- | -----------|
| Récupération partielle par lot | L&#39;assimilation partielle par lot permet d&#39;assimiler des données contenant des erreurs, jusqu&#39;à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent intégrer toutes leurs données correctes dans Adobe Experience Platform, tandis que toutes leurs données incorrectes sont mises en lots séparément. Des détails sont ajoutés aux lots non validés pour expliquer pourquoi ils n’ont pas réussi la validation. Vous trouverez plus d&#39;informations sur l&#39;assimilation partielle de lots dans la documentation [sur l&#39;assimilation](../../ingestion/batch-ingestion/partial.md)partielle de lots. |

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur l&#39;assimilation de données dans la plate-forme, consultez la documentation [sur l&#39;importation de](../../ingestion/home.md)données.


## Destinations {#destinations}

Dans [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations préétablies avec les plateformes de destination qui activent les données pour ces partenaires de manière transparente.

**Nouvelles destinations**

De nouvelles destinations sont disponibles où vous pouvez activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| Destinations de stockage dans le cloud | Adobe Real-time CDP peut désormais diffuser vos segments sous forme de fichiers de données vers vos enregistrements cloud Amazon S3 ou SFTP. Vous pouvez ainsi envoyer des audiences et leurs attributs de profils à vos systèmes internes, au moyen de fichiers CSV ou séparés par des tabulations. |
| Destinations publicitaires | La carte de destination Google est maintenant divisée en trois cartes de destination, pour les trois plates-formes Google différentes actuellement prises en charge dans le CDP en temps réel d’Adobe : Annonces Google, Google Ad Manager, Google Display &amp; Video 360. |

Pour en savoir plus, consultez la présentation des [destinations](../../rtcdp/destinations/destinations-overview.md)

## Identity Service {#identity}

La diffusion d’expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela est rendu plus difficile lorsque les données de vos clients sont fragmentées entre des systèmes disparates, ce qui donne à chaque client l’impression d’avoir plusieurs &quot;identités&quot;.

Adobe Experience Platform Identity Service vous aide à mieux vue de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes, ce qui vous permet de fournir des expériences numériques personnelles et impactées en temps réel.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ------- | ----------- |
| Graphique privé amélioré | La fonctionnalité Graphique privé a été améliorée afin de réduire la latence de génération de graphiques d&#39;un traitement par lots hebdomadaire à un graphique actualisé quotidiennement, ce qui permet aux clients Identity Service d&#39;accéder à des graphiques d&#39;identité et des liens d&#39;identité plus à jour. |

**Problèmes connus**

* None (Aucun)

Pour plus d&#39;informations sur Identity Service, consultez la présentation [de](../../identity-service/home.md)Identity Service.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plate-forme. Vous pouvez ingérer des données à partir de diverses sources, telles que des applications Adobe, des enregistrements basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent d’authentifier et de vous connecter à des systèmes d’enregistrement externes et à des services de gestion de la relation client, de définir les heures d’exécution d’assimilation et de gérer le débit d’assimilation des données.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ------- | ----------- |
| Signaux obsolètes pour le connecteur Adobe Audience Manager | Les données au niveau du signal d’Audience Manager ne seront plus envoyées. Notez que l’appartenance aux segments pour les Caractéristiques et les Segments sera toujours incluse. Suite à ce changement, les jeux de données entrants ne seront plus générés. |
| Jeu de données renommé | Les jeux de données générés par le connecteur Audience Manager auront des noms et des descriptions mis à jour. |
| Activer la bascule Profil dans Audience Manager | La bascule de Profil peut être activée ou désactivée pour convertir le jeu de données en Profil client en temps réel. Basculer sera activé par défaut. |
| Prise en charge de l’interface utilisateur pour les systèmes d’enregistrement cloud | Nouveau connecteur source pour Azure Data Lake Enregistrement Gen2 dans l&#39;interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes CRM | Nouveau connecteur source pour HubSpot, Salesforce Service Cloud et ServiceNow dans l’interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes de base de données | Nouveau connecteur source pour AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server et MySQL dans l’interface utilisateur. |

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur les sources, consultez l’aperçu [des](../../sources/home.md)sources.