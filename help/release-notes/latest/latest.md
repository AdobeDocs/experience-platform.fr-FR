---
title: Notes de mise à jour d’Adobe Experience Platform - Février 2025
description: Notes de mise à jour de février 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c4064771a384a90d94903ba1761fc9ee20f47747
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 88%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Cette version comprend des améliorations du module complémentaire Composition d’audiences fédérées. Pour plus d’informations, consultez les [notes de mise à jour de la Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/release-notes).

**Date de mise à jour : 18 février 2025**

Mises à jour des fonctionnalités et de la documentation existantes dans Adobe Experience Platform :

- [Assistant IA](#ai-assistant)
- [Catalog Service](#catalog-service)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Sources](#sources)
- [Service de segmentation](#segmentation)
- [Mises à jour de la documentation](#documentation-updates)
   - [Comparaison entre Edge Network et un hub](#edge)
   - [API de service de flux développé pour les sources](#flow-service)
   - [Sauvegarder des configurations d’objet à l’aide des outils de sandbox](#back-up-object-configurations)
   - [Activer un centre d’excellence à l’aide des outils de sandbox](#center-of-excellence)
   - [Conservation du jeu de données d’événement d’expérience dans le lac de données](#experience-event-dataset-retention)

## Assistant IA {#ai-assistant}

L’Assistant IA dans Adobe Experience Platform est une expérience conversationnelle que vous pouvez utiliser pour accélérer vos workflows dans les applications Adobe. Vous pouvez utiliser l’Assistant IA pour développer vos connaissances sur le produit, résoudre les problèmes ou rechercher des informations et trouver des informations opérationnelles. L’assistant IA prend en charge Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale des informations opérationnelles | Les informations opérationnelles sur l’assistant d’IA sont désormais disponibles en disponibilité générale. Les informations opérationnelles se rapportent aux réponses que l’assistant AI génère sur vos objets de métadonnées (attributs, audiences, flux de données, jeux de données, destinations, parcours, schémas et sources), y compris les nombres, les recherches et l’impact de la parenté. Les informations opérationnelles n’examinent aucune donnée dans le sandbox. Pour plus d’informations, consultez le guide de l’interface utilisateur de l’assistant [AI](../../ai-assistant/ui-guide.md). |
| Prise en charge de la saisie semi-automatique des questions | Lors de la saisie d’une question dans l’assistant IA, vous pouvez désormais effectuer une sélection dans une liste de questions recommandées fournies par l’assistant IA. Utilisez cette fonctionnalité pour accélérer davantage vos workflows avec l’assistant IA. Pour plus d’informations, consultez le guide sur l’[utilisation de la saisie semi-automatique des questions avec l’assistant IA](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Prise en charge du contrôle des jeux de données | Vous pouvez désormais utiliser l’assistant IA pour répondre aux questions sur des mesures de jeux de données spécifiques, telles que les tailles de stockage et le nombre de lignes. Les questions de contrôle des données prennent en charge les qualificateurs que vous pouvez utiliser pour filtrer vos requêtes selon une certaine période. Pour plus d’informations, consultez le [guide des questions de l’assistant IA](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble de l’assistant IA](../../ai-assistant/home.md).

## Catalog Service {#catalog-service}

Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, Catalog conserve les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

| Fonctionnalité | Description |
| --- | --- |
| Nouveau point d’entrée de l’API | Gérez plus efficacement vos métadonnées de jeu de données Adobe Experience Platform avec le nouveau [point d’entrée de l’API Catalog Service /v2/dataSets/{DATASET_ID}](../../catalog/api/update-object.md#patch-v2-notation). Mettez facilement à jour des attributs de jeux de données complexes et profondément imbriqués tandis que le système crée automatiquement les niveaux de chemin manquants pour vous faire gagner du temps, réduire les étapes manuelles et minimiser les erreurs. |

{style="table-layout:auto"}

Pour plus d’informations sur Catalog Service, consultez la [vue d’ensemble de Catalog Service](../../catalog/home.md).

## Préparation des données {#data-prep}

Utilisez la préparation des données pour mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge améliorée de l’import et de l’export de mappages | Vous pouvez désormais exporter des mappages vers un fichier CSV et les configurer localement sur une feuille de calcul. Vous pouvez ensuite importer vos mappages mis à jour dans Experience Platform à l’aide de l’interface de mappage de l’IU. Vous pouvez utiliser cette fonctionnalité pour configurer un grand nombre de mappages sans avoir à les créer manuellement dans l’IU. De plus, lors de la création d’un flux de données, vous pouvez charger une copie de vos mappages directement dans Experience Platform pour accélérer votre workflow. Pour plus d’informations, consultez le guide sur [l’import et l’export de mappages](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble de la préparation de données](../../data-prep/home.md).

## Destinations (mise à jour le 20 février) {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Description |
| --- | --- |
| [(Version bêta) Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Utilisez le connecteur [!DNL Marketo Engage Person Sync] pour diffuser des mises à jour d’audiences de personnes vers les enregistrements correspondants de votre instance [!DNL Marketo Engage]. Ce connecteur de destination est en version bêta et disponible uniquement pour certaines personnes. Pour obtenir l’accès, contactez votre représentant ou représentante Adobe. |
| Disponibilité générale de la [connexion CRM Trade Desk](/help/destinations/catalog/advertising/tradedesk-emails.md) | La connexion [!DNL The Trade Desk CRM] est désormais disponible pour toute la clientèle. Utilisez la destination CRM [!DNL The Trade Desk] pour activer des profils sur votre compte [!DNL Trade Desk], afin de permettre le ciblage et la suppression d’audiences en fonction des données CRM. |
| [Connexion aux profils des participantes et participants RainFocus](/help/destinations/catalog/marketing-automation/rainfocus.md) | Utilisez la destination [!DNL RainFocus Attendee Profiles] pour diffuser des profils clientèle d’Adobe Experience Platform vers la plateforme [!DNL RainFocus] afin de créer et de mettre à jour des profils de participantes et participants. |
| Disponibilité générale de la [connexion Criteo](/help/destinations/catalog/advertising/criteo.md) | La connexion [!DNL Criteo] est désormais disponible pour toute la clientèle. Criteo permet de proposer des publicités fiables et percutantes afin d’offrir des expériences plus riches à chaque personne sur Internet. Grâce au plus grand jeu de données du commerce au monde et à la meilleure IA de sa catégorie, Criteo veille à ce que chaque point de contact du parcours d’achat soit personnalisé afin de toucher les clientes et clients avec la bonne annonce, au bon moment. |
| [[!DNL Amazon Ads] Connexion](../../destinations/catalog/advertising/amazon-ads.md) | Le connecteur [!DNL Amazon Ads], auparavant en version bêta, est désormais disponible pour toute la clientèle. Le connecteur a également été mis à jour pour envoyer un signal d’accord de consentement à tous les profils qui ont consenti à ce que leurs données personnelles soient utilisées à des fins de publicité. En savoir plus sur la nouvelle commande [Signal de consentement des publicités Amazon](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| --- | --- |
| Utiliser des libellés d’accès pour gérer l’accès des utilisateurs et utilisatrices aux flux de données de destination | Dans le cadre de la fonctionnalité de [[!UICONTROL contrôle d’accès basé sur les attributs]](/help/access-control/abac/overview.md) de Real-Time CDP, vous pouvez désormais appliquer des libellés d’accès aux [flux de données de destination](/help/dataflows/ui/monitor-destinations.md). Ainsi, vous pouvez vous assurer que seul un sous-ensemble d’utilisateurs et d’utilisatrices de votre organisation a accès à des flux de données de destination spécifiques. <br> **Important** : lors de la recherche de flux de données de destination à l’aide de la zone de recherche située en haut de l’interface d’utilisation d’Experience Platform, les résultats peuvent inclure des flux de données de destination que vos libellés d’accès d’utilisation vous empêchent de voir. Ce comportement sera corrigé dans une mise à jour à venir. |
| [Rapports au niveau de l’audience](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) pour la [connexion Marketo Engage](/help/destinations/catalog/adobe/marketo-engage.md) | Vous pouvez désormais [afficher des informations](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) sur les identités activées, exclues ou en échec réparties au niveau de l’audience, pour chaque audience qui fait partie des flux de données pour cette destination. |
| Prise en charge des audiences externes pour les connexions [TikTok](/help/destinations/catalog/social/tiktok.md) et [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | Vous pouvez activer des audiences externes vers ces destinations à partir de [chargements personnalisés](../../segmentation/ui/audience-portal.md#import-audience) et de la [composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/start/audiences). |
| Exporter des tableaux, des mappages et des objets vers des destinations d’espace de stockage | En utilisant le nouveau bouton (bascule) **[!UICONTROL Exporter des tableaux, des mappages]** des objets lors de la connexion à une destination d’espace de stockage , vous pouvez exporter des objets complexes vers des destinations sélectionnées. [En savoir plus](/help/destinations/ui/export-arrays-calculated-fields.md) à propos de la fonctionnalité. |

{style="table-layout:auto"}

**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

- Correction d’un problème lié aux outils de test de Destination SDK. Certaines personnes partenaires ou clientes et clients rencontraient des problèmes avec [l’outil de génération de profil d’exemple](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) en raison d’un format non pris en charge lorsque le schéma utilisé pour générer les profils incluait des types de données avec un sélecteur `No format`.
- Résolution d’un problème lors de la mise à jour de la spécification `targetConnection` des destinations à l’aide de l’API Flow Service. Dans certains cas, l’opération PATCH se comportait de la même manière qu’une opération POST, corrompant les flux de données existants. Ce problème est maintenant corrigé et tous les clientes et clients peuvent utiliser l’API Flow Service pour mettre à jour leur spécification `targetConnection`. [En savoir plus](/help/destinations/api/edit-destination.md#patch-target-connection).
- Lors de l’exportation de profils vers des destinations basées sur des fichiers, la déduplication garantit qu’un seul profil est exporté lorsque plusieurs profils partagent la même clé de déduplication et le même horodatage de référence. Cette version comprend une mise à jour du processus de déduplication, afin de s’assurer que les exécutions successives avec les mêmes coordonnées produiront toujours les mêmes résultats, ce qui améliore la cohérence. [En savoir plus](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp).

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Division persistante | La composition de l’audience prend désormais en charge les divisions persistantes. Le fractionnement des audiences peut rester constant lors du fractionnement par profil en ajoutant un espace de noms d’identité à votre bloc Fractionner . Vous trouverez plus d’informations sur cette fonctionnalité dans la [documentation sur la composition de l’audience](../../segmentation/ui/audience-composition.md). |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des vues dans [!DNL Microsoft Dynamics] | Vous pouvez désormais ingérer `"entityType": "view"` lors de l’utilisation de la source [!DNL Microsoft Dynamics]. Pour plus d’informations, consultez le guide sur la [connexion d’une source  [!DNL Microsoft Dynamics]  à Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).

## Mises à jour de la documentation {#documentation-updates}

### Comparaison entre Edge Network et un hub {#edge}

La [comparaison entre Edge Network et un hub](../../landing/edge-and-hub-comparison.md) fournit une vue d’ensemble détaillant les différences entre les deux types de serveurs pour Adobe Experience Platform (hub et Edge Network), y compris les services disponibles sur chaque type de serveur, les emplacements des serveurs, ainsi que les scénarios recommandés pour l’utilisation de chaque type de serveur.

### Référence de l’API Flow Service développée pour les sources {#flow-service}

La [[!DNL Flow Service] référence d’API](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) pour les sources a été mise à jour avec de nouveaux exemples de requête et de réponse d’API. Utilisez la référence d’API développée pour créer et mettre à jour des spécifications de connexion lors de l’intégration de votre propre source à Experience Platform. Vous pouvez également utiliser la référence d’API développée pour effectuer des transitions d’état sur vos entités sources, mettre à jour les connexions source et cible existantes et récupérer les flux et les spécifications de flux selon un critère de filtrage spécifique.

### Sauvegarder des configurations d’objet à l’aide des outils de sandbox {#back-up-object-configurations}

Lisez le [guide de configuration de la sauvegarde d’objets](../../sandboxes/use-cases/backup-object-configuration.md) pour obtenir des instructions détaillées sur la création d’un package de sauvegarde à l’aide des outils de sandbox afin de vous assurer que les configurations d’objet sont stockées et sécurisées.

### Activer un centre d’excellence à l’aide des outils de sandbox {#center-of-excellence}

Lisez le [guide du centre d’excellence](../../sandboxes/use-cases/center-of-excellence.md) pour obtenir des instructions détaillées sur la création d’un package « sandbox doré » qui agit comme un centre d’excellence pour partager efficacement les configurations clés.

### Conservation du jeu de données d’événement d’expérience dans le lac de données {#experience-event-dataset-retention}

Prenez le contrôle de la conservation des jeux de données des événements d’expérience dans Adobe Experience Platform à l’aide de la durée de vie (TTL). [Ce guide](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) vous accompagne tout au long de l’évaluation, de la configuration et de la gestion des paramètres TTL pour supprimer automatiquement les enregistrements obsolètes, optimiser le stockage et conserver la pertinence de vos données. Découvrez les bonnes pratiques, les cas d’utilisation réels et les principales considérations permettant d’améliorer la gestion du cycle de vie des données.
