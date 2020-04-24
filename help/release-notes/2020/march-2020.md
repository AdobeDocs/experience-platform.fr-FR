---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 11 mars 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 11 mars 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [Gouvernance des données](#governance)
* [Ingestion des données](#ingestion)
* [Destinations](#destinations)
* [Service d’identité](#identity)
* [Sources](#sources)

## Gouvernance des données {#governance}

Experience Platform permet aux de rassembler des données issues de plusieurs systèmes d’entreprise afin de mieux permettre aux spécialistes du marketing d’identifier, de comprendre et d’impliquer les clients. Experience Platform inclut une infrastructure de gouvernance des données de bout en bout, y compris l’étiquetage et l’application de l’utilisation des données (DULE), afin d’assurer l’utilisation appropriée des données dans la plateforme et lors du partage entre les systèmes.

La gouvernance des données d’Adobe Experience Platform est une série de stratégies et de technologies utilisées pour gérer les données des clients et garantir la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. Il joue un rôle clé dans Experience Platform à différents niveaux, notamment le catalogage, le lignage des données, l’étiquetage de l’utilisation des données, les stratégies d’accès aux données et les  sur les données pour les actions marketing.

**Nouvelles fonctionnalités**

>[!NOTE] Certaines des nouvelles fonctionnalités suivantes sont actuellement en version bêta et ne sont pas disponibles pour tous les utilisateurs. Les fonctionnalités bêta peuvent être modifiées.

| Fonction | Description |
| ------- | ----------- |
| Application automatisée des stratégies d’utilisation des données pour la plateforme de données clientes en temps réel | Les stratégies d’utilisation des données sont désormais appliquées dans le processus d’activation des données vers les destinations. La gouvernance des données est également intégrée et appliquée lors de l’apport de modifications qui affectent les  de  existantes (telles que les modifications des libellés des jeux de données, des stratégies de fusion, des définitions de segment, etc.). |
| Plage de données pour l&#39;application | Lorsqu’une stratégie d’utilisation des données est violée dans le CDP en temps réel, l’interface utilisateur affiche une notification qui contient des informations de lignage de données pour aider l’utilisateur à comprendre pourquoi les stratégies ont été violées et ce qu’il peut faire pour résoudre la violation. |


**Problèmes connus**

* None (Aucun)

Pour plus d’informations sur la gouvernance des données, voir l’aperçu [de la gouvernance des](../../data-governance/home.md)données.

## Ingestion des données {#ingestion}

Adobe Experience Platform offre un ensemble de fonctionnalités très complet pour assimiler tout type de données et leur latence. L’intégration des données d’Adobe Experience Platform propose plusieurs alternatives pour l’assimilation de données, notamment des API par lots, des API de diffusion en continu, des connecteurs Adobe natifs, des partenaires d’intégration de données ou l’interface utilisateur d’Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonction | Description |
|------- | -----------|
| Récupération partielle par lot | L’assimilation partielle par lot permet d’assimiler des données contenant des erreurs, jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent intégrer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont mises en lots séparément. Des détails sont ajoutés aux lots non validés pour expliquer pourquoi ils n’ont pas réussi la validation. Vous trouverez plus d&#39;informations sur l&#39;assimilation partielle de lots dans la documentation [sur l&#39;assimilation](../../ingestion/batch-ingestion/partial.md)partielle de lots. |

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur l’assimilation de données dans Platform, consultez la documentation [sur l’](../../ingestion/home.md)assimilation des données.


## Destinations {#destinations}

Dans [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations prédéfinies avec les plateformes de destination qui activent les données de manière transparente vers ces partenaires.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| Destinations de stockage dans le cloud | Le CDP en temps réel d’Adobe peut désormais diffuser vos segments sous forme de fichiers de données dans votre cloud Amazon S3 ou SFTP  des emplacements  de vos. Vous pouvez ainsi envoyer des audiences et leurs attributs de profils à vos systèmes internes, au moyen de fichiers CSV ou séparés par des tabulations. |
| Destinations publicitaires | La carte de destination Google est maintenant divisée en trois cartes de destination, pour les trois plates-formes Google actuellement prises en charge dans le CDP en temps réel d’Adobe : Annonces Google, Google Ad Manager, Google Display &amp; Video 360. |

Pour en savoir plus, consultez la présentation des [destinations](../../rtcdp/destinations/destinations-overview.md)

## Identity Service {#identity}

La diffusion d’expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela est rendu plus difficile lorsque les données de vos clients sont fragmentées entre des systèmes disparates, ce qui donne à chaque client l’impression d’avoir plusieurs &quot;identités&quot;.

Le service d’identité Adobe Experience Platform vous permet de mieux  de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes, ce qui vous permet de diffuser en temps réel des expériences numériques personnelles et impactées.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ------- | ----------- |
| Graphique privé amélioré | La fonctionnalité Graphique privé a été améliorée afin de réduire la latence de génération de graphiques d’un traitement par lots hebdomadaire à un graphique actualisé quotidiennement, ce qui permet aux clients du service d’identité d’accéder à des graphiques d’identité et à des liens plus récents. |

**Problèmes connus**

* None (Aucun)

Pour plus d&#39;informations sur Identity Service, consultez la présentation [de](../../identity-service/home.md)Identity Service.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plateforme. Vous pouvez assimiler des données à partir de diverses sources, telles que des applications Adobe, des  basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des systèmes de  et des services de gestion de la relation client externes, de définir les heures d&#39;exécution de l&#39;assimilation et de gérer le débit d&#39;assimilation des données.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ------- | ----------- |
| Signaux obsolètes pour le connecteur Adobe   Manager | Les données de niveau signal de   Manager ne seront plus envoyées. Notez que l’appartenance aux segments pour les Caractéristiques et les Segments sera toujours incluse. Suite à ce changement, les jeux de données entrants ne seront plus générés. |
| Jeu de données renommé | Les jeux de données générés par  connecteur  Manager auront des noms et des descriptions mis à jour. |
| Activer la bascule  dans  Gestionnaire de  | La bascule  peut être activée ou désactivée pour convertir le jeu de données en client en temps réel. Basculer sera activé par défaut. |
| Prise en charge de l’interface utilisateur pour les  de cloud  systèmes | Nouveau connecteur source pour Azure Data Lake   Gen2 dans l&#39;interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes CRM | Nouveau connecteur source pour HubSpot, Salesforce Service Cloud et ServiceNow dans l’interface utilisateur. |
| Prise en charge de l’interface utilisateur pour les systèmes de base de données | Nouveau connecteur source pour AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server et MySQL dans l’interface utilisateur. |

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur les sources, consultez l’aperçu [des](../../sources/home.md)sources.