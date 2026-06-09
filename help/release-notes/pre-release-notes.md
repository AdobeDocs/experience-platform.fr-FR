---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5ffdc773cb78a45d14f0614ff26fd262136799fa
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 21%

---

# Notes de mise à jour préliminaires de Adobe Experience Platform

>[!IMPORTANT]
>
>Ce document est conçu comme un **aperçu** des notes de mise à jour du mois en cours. Les éléments de version peuvent faire l’objet de modifications et peuvent être ajoutés ou supprimés dans la version finale.

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/latest)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : juin 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Agent Orchestrator](#agent-orchestrator)
- [Destinations](#destinations)
- [Service de requête](#query-service)
- [Exécuter et exploiter](#run-and-operate)
- [Service de segmentation](#segmentation-service)
- [Sources](#sources)
- [Modèle de données d’expérience (XDM)](#xdm)

## Agent Orchestrator {#agent-orchestrator}

Utilisez Agent Orchestrator pour créer et déployer des agents optimisés par l’IA qui automatisent les workflows et interagissent avec les clients sur plusieurs canaux.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Agent de notifications | Utilisez l’agent de notifications pour faire apparaître les alertes, les événements système et les mises à jour d’audience ou de parcours par le biais d’invites conversationnelles. L’agent fournit des résumés de notifications contextuelles afin que vous puissiez agir sur les événements critiques sans avoir à parcourir plusieurs tableaux de bord. |
| [!BADGE Beta &#x200B;]{type=Informative} Adobe Marketing Agent pour les plateformes d’IA | Utilisez Adobe Marketing Agent pour intégrer des informations opérationnelles, des données d’audience, des informations de parcours et la découverte de ressources Experience Platform à des plateformes d’IA tierces, notamment [!DNL ChatGPT], [!DNL Claude], [!DNL Gemini], [!DNL Amazon Q], [!DNL Databricks Genie] et [!DNL IBM Watsonx]. Contactez votre représentant Adobe pour demander l’accès. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [documentation d’](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| {type=Informative} [Quand activer &#x200B;](../destinations/ui/when-to-activate.md) | Contrôler les types de modification de profil qui déclenchent des exportations vers une destination. Activez ou désactivez trois types de déclencheurs par flux de données : modifications d’attributs, qualification et disqualification d’audience et modifications d’identité. Les trois déclencheurs sont activés par défaut. Cette fonctionnalité est disponible pour un nombre limité de clientes et clients. Pour obtenir l’accès, contactez votre représentant ou représentante Adobe. |
| Lien privé Azure pour les destinations Azure | Acheminez les exportations de données vers [[!DNL Azure Blob Storage]](../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Azure Data Lake Storage Gen2]](../destinations/catalog/cloud-storage/adls-gen2.md) et [[!DNL Azure Event Hubs]](../destinations/catalog/cloud-storage/azure-event-hubs.md) via des adresses IP privées sur la colonne vertébrale [!DNL Microsoft Azure] plutôt que sur l’Internet public. Cette fonctionnalité est disponible pour les clients disposant de droits Healthcare Shield ou Privacy and Security Shield. Contactez votre représentant Adobe pour demander la configuration. |
| Prise en charge d’[[!DNL Snowflake Streaming]](../destinations/catalog/warehouses/snowflake.md) et de [[!DNL Snowflake Batch]](../destinations/catalog/warehouses/snowflake-batch.md) Private Link | Un nouveau bouton (bascule) Lien privé est désormais disponible lors de la configuration de connexions de destination par lots et en flux continu [!DNL Snowflake]. Activez ce bouton uniquement si votre compte [!DNL Snowflake] est configuré pour un accès entrant privé en liaison seule. Si vous désactivez cette option pour les comptes de liaison privés uniquement, le partage des données échoue. |
| {type=Informative} [Exportez des tableaux en tant qu’attributs d’enrichissement](../destinations/ui/activate-batch-profile-destinations.md#select-enrichment-attributes) | Exportez les champs du tableau en tant qu’attributs d’enrichissement lors de l’activation des audiences vers des destinations d’espace de stockage.Sélectionnez des champs individuels dans un tableau d’objets ou exportez le tableau complet. Les données sont ensuite exportées en tant que colonnes distinctes dans les sorties JSON et Parquet. |
| [[!DNL Google Ad Manager 360]](../destinations/catalog/advertising/google-ad-manager-360-connection.md) désormais généralement disponible | La destination [!DNL Google Ad Manager 360] (anciennement en version Beta) est désormais disponible pour tous. |
| [[!DNL Google Customer Match + Display & Video 360]](../destinations/catalog/advertising/google-customer-match-dv360.md) désormais généralement disponible | La destination [!DNL Google Customer Match + Display & Video 360] (anciennement en disponibilité limitée) est désormais disponible pour tous. La surveillance a été mise à jour afin d’afficher une exécution de flux de données par jour, au lieu de plusieurs exécutions distinctes pour les événements réalisés et sortis par espace de noms d’identité. |
| [Rapports au niveau de l’audience pour les destinations supplémentaires](../dataflows/ui/monitor-destinations.md#audience-level-view) | La création de rapports sur les flux de données au niveau de l’audience est désormais disponible pour les destinations suivantes : [Gainsight PX](../destinations/catalog/analytics/gainsight-px.md), [TikTok](../destinations/catalog/social/tiktok.md), [Audiences correspondantes Linkedin](../destinations/catalog/social/linkedin.md), [Demandbase People](../destinations/catalog/advertising/demandbase-people.md), [(héritée) Amazon Ads](../destinations/catalog/advertising/amazon-ads.md), [Liste de clients Pinterest](../destinations/catalog/advertising/pinterest.md), [Twitter Custom Audiences](../destinations/catalog/social/twitter.md), [Braze](../destinations/catalog/mobile-engagement/braze.md), [(Companies) LinkedIn](../destinations/catalog/social/linkedin-b2b.md), [Facebook](../destinations/catalog/social/facebook.md), [Mailchimp Tags](../destinations/catalog/email-marketing/mailchimp-tags.md) et [Salesforce CRM](../destinations/catalog/crm/salesforce.md). |

{style="table-layout:auto"}

**Correctifs et améliorations**

| Corriger | Description |
| --- | --- |
| [[!DNL Reddit Custom Audience]](../destinations/catalog/advertising/reddit-custom-audience.md) le correctif d’activation | Correction d’un problème qui empêchait les clients d’activer les données lorsqu’ils le tentaient plus de 24 heures après l’authentification. |
| Application d’audience restreinte [[!DNL Facebook]](../destinations/catalog/social/facebook.md) | À compter du 8 juin 2026, [!DNL Facebook] bloquera les audiences contenant des données restreintes ou sensibles (telles que des informations financières ou de santé) en vertu de ses Conditions d’utilisation. Consultez la section [données d’audience restreintes](../destinations/catalog/social/facebook.md#restricted-audiences) pour connaître les étapes de dépannage. |
| [Mise à jour du mécanisme de sécurisation pour l’activation des audiences externes](../destinations/guardrails.md#batch-file-based-activation) | Le nombre maximal d’audiences externes (telles que le chargement personnalisé, la composition d’audiences fédérées et la composition d’audiences) pouvant être activées par instance de destination a été porté à 100. |
| [Filtres supplémentaires à l’étape Sélectionner la destination &#x200B;](../destinations/ui/activate-segment-streaming-destinations.md#select-destination) | L’étape **[!UICONTROL Sélectionner la destination]** du workflow d’activation comprend désormais des filtres supplémentaires pour vous aider à localiser plus rapidement le flux de données de destination approprié. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

Le modèle de données d’expérience (XDM) est une spécification open source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Experience Platform.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Améliorations de l’inventaire des schémas](../xdm/ui/resources/schemas.md) | La page de navigation des schémas comprend désormais des métadonnées de schéma supplémentaires, des options de filtrage amélioré, des balises et des dossiers définis par l’utilisateur, ainsi que des actions intégrées pour les tâches courantes de gestion des schémas. Ces mises à jour vous aident à rechercher, organiser et gérer des schémas plus efficacement à partir d’un seul emplacement. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble XDM](../xdm/home.md).

## Service de requête {#query-service}

Utilisez Query Service pour interroger des données dans Adobe Experience Platform à l’aide de SQL standard.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Personalization à long terme avec des accélérateurs de Distiller de données | De nouveaux conseils expliquent comment utiliser les accélérateurs de Distiller de données et les données historiques stockées dans le lac de données pour générer des informations prêtes pour la personnalisation et l’activation de l’audience. Cette approche vous permet de prendre en charge des intervalles de recherche en amont étendus tout en optimisant l’utilisation du magasin de profils et la consommation totale du volume de données. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de Query Service](../query-service/home.md).

## Exécuter et exploiter {#run-and-operate}

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Détection de motifs dans les planifications de tâches](../run-and-operate/job-schedules-anti-patterns.md) | Trois antimodèles sont désormais automatiquement détectés dans la vue Planifications de tâches : plus de 90 exécutions d’ingestion de profils par jour, ingestion de profils planifiée trop proche de la segmentation et segmentation planifiée trop proche de l’activation de destination. La recherche en amont des 7 derniers jours comprend désormais une vue Calendrier pour la sélection de la date. Cette fonctionnalité sera déployée jusqu’à la fin juin 2026. |
| [Contrôles d’intégrité pour P-TTL et e-TTL](../run-and-operate/health-checks.md) | Deux nouveaux contrôles d’intégrité sont désormais disponibles : la durée de vie du profil pseudonyme (P-TTL) vérifie si la politique d’expiration est active pour votre sandbox et répertorie les espaces de noms non authentifiés pertinents. La TTL des jeux de données d’événements d’expérience (e-TTL) analyse les jeux de données de lac de données et d’événements de profil pour identifier les endroits où l’expiration automatique des données n’est pas configurée. |

{style="table-layout:auto"}

## Service de segmentation {#segmentation-service}

Utilisez Segmentation Service pour créer des audiences à partir des données de vos clients et gérer leur cycle de vie complet dans Experience Platform.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Répartition persistante ou aléatoire dans la composition de l’audience](../segmentation/ui/audience-composition.md) | Utilisez le nouveau sélecteur de mode de partage dans la composition de l’audience pour choisir entre les divisions de pourcentage persistantes et aléatoires. La division persistante conserve le même profil dans le même compartiment entre les évaluations. Le partage aléatoire peut placer un profil dans un compartiment différent entre les évaluations. Lors de l’utilisation de la division persistante, sélectionnez un espace de noms d’identité avec peu de variance pour garantir une appartenance fiable à l’audience. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des audiences](../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| [!BADGE Version bêta]{type=Informative} [!DNL Meta Ads] | Utilisez la source [!DNL Meta Ads] pour configurer le workflow complet d’ingestion de [!DNL Meta Ads] dans l’interface utilisateur Sources. Connectez votre compte [!DNL Meta Ads] et importez les données de médias payants directement dans Experience Platform pour activation et analyse. Cette source est disponible pour un nombre limité de clients. Contactez votre représentant Adobe pour demander l’accès. |
| [!BADGE Version bêta]{type=Informative} [!DNL Delta Sharing] | Utilisez la source [!DNL Delta Sharing] pour importer des jeux de données partagés en direct de partenaires ou d’environnements de lac internes dans Experience Platform sans copier ni charger manuellement de fichiers. Connectez-vous à un point d’entrée [!DNL Delta Sharing], choisissez les tables dont vous avez besoin et utilisez ces données gouvernées avec vos profils et informations existants. |

{style="table-layout:auto"}

**Mises à jour et correctifs**

| Source | Description |
| --- | --- |
| [[!DNL Shopify Streaming]](../sources/connectors/ecommerce/shopify-streaming.md) l’authentification HMAC | L’authentification HMAC est désormais prise en charge dans le connecteur [!DNL Shopify Streaming], disponible dans l’interface utilisateur et l’API. Voir la [[!DNL Shopify Streaming] présentation](../sources/connectors/ecommerce/shopify-streaming.md) pour connaître le comportement de rotation des clés et les instructions de configuration. |
| [Désactivation automatique du flux de données](../sources/home.md) | Les flux de données des sources qui échouent en continu pendant 30 jours sont automatiquement désactivés. Lorsqu’un flux de données est désactivé, passez en revue la raison de l’échec dans Surveillance, appliquez les mises à jour nécessaires et réactivez le flux de données. Les raisons d’échec courantes incluent les informations d’identification, les autorisations ou les modifications de configuration des schémas et des mappages. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../sources/home.md).

<!--

| [Scheduled queries with no end date](../query-service/api/scheduled-queries.md) | Create scheduled queries that run indefinitely without specifying an end date. Use this for continuous recurring workflows. The UI may display indefinite schedules using a far-future date such as 31.12.9999. |

## Advanced data lifecycle management {#advanced-data-lifecycle-management}

Experience Platform provides a suite of data hygiene capabilities that let you manage your stored data through programmatic deletions of consumer records and datasets.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Multi-dataset and targeted services for work orders](../hygiene/api/jobs.md) | Two new API-only capabilities are now available for data lifecycle work orders. Use targeted services to scope deletion to specific services (profile, identity, or [!DNL Adobe Journey Optimizer]) without modifying data in the lake. Use multi-dataset support to target one, many, or all datasets in a single work order submission. |

{style="table-layout:auto"}

For more information, read the [advanced data lifecycle management overview](../hygiene/home.md).

-->