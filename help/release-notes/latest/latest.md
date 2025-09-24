---
title: Notes de mise à jour d’Adobe Experience Platform - Août 2025
description: Les notes de mise à jour d’août 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: ac180f045dd3cc7e8ad9de702a3672630d668ee5
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 41%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/e-release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : mercredi 23 septembre 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Agent Orchestrator](#agent-orchestrator)
- [Alertes](#alerts)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Profil client en temps réel](#profile)
- [Segmentation Service](#segmentation-service)
- [Sources](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator est la nouvelle couche d’agent de Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator est la nouvelle couche d’agent de Adobe Experience Platform. Conçu pour exploiter les données riches et les connaissances des clients de la plateforme, Experience Platform Agent Orchestrator alimente l&#39;intelligence et la logique derrière des agents Adobe Experience Platform experts spécialement conçus, leur permettant d&#39;exécuter des tâches complexes de prise de décision et de résolution de problèmes à vitesse et à l&#39;échelle, le tout avec une supervision humaine. Lorsque vous posez des questions ou demandez de l’aide en langage naturel dans une interface de conversation comme l’assistant d’IA, Agent Orchestrator fait automatiquement appel à des agents spécialisés pour vous obtenir les bonnes réponses. Agent Orchestrator mémorise l&#39;historique de vos conversations, ce qui vous permet de vous appuyer sur les questions précédentes naturellement sans répéter le contexte, et d&#39;associer les informations provenant de plusieurs agents pour vous présenter des réponses claires et unifiées. Pour plus d’informations, consultez la [documentation d’Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). |
| Audience Agent | Audience Agent vous permet d’obtenir des informations sur les audiences, notamment la détection des modifications importantes de la taille de l’audience, la détection des audiences en double, l’exploration de l’inventaire de vos audiences et la récupération de la taille de vos audiences. Pour plus d’informations, consultez la [documentation d’Audience Agent](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Pour plus d’informations, consultez la [documentation d’Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/home).

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface d’utilisation d’Experience Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’UI elle-même ou par le biais de notifications par e-mail.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Alertes d’ingestion de profil en flux continu | Vous pouvez désormais vous abonner à deux nouvelles alertes pour l’ingestion en flux continu au niveau du flux de données : <ul><li>Taux d’échec d’ingestion en flux continu dépassé</li><li>Taux d’ingestion en flux continu ignorée dépassé</li></ul> Les alertes sur la plateforme ou par e-mail vous avertissent lorsque les seuils sont dépassés pour le seuil par défaut ou pour un seuil personnalisé que vous définissez. Pour plus d’informations, consultez le guide [Alertes de profil](../../observability/alerts/rules.md#profile). |

{style="table-layout:auto"}

Pour plus d’informations sur les alertes, consultez la [[!DNL Observability Insights] vue d’ensemble](../../observability/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| Connecteur [!BADGE &#x200B; &#x200B;]{type=Informative}Beta[[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md) | Un nouveau connecteur [!DNL Snowflake Batch] est désormais disponible, offrant une alternative au connecteur de diffusion en continu pour des cas d’utilisation spécifiques. |
| Prise en charge du chiffrement [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Vous pouvez désormais joindre des clés publiques au format RSA pour chiffrer vos fichiers exportés, ce qui vous offre le même niveau de sécurité que les autres destinations de stockage dans le cloud pour vos informations sensibles. |
| Détails d’expiration de l’authentification pour les destinations [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) | Les informations d’expiration de l’authentification pour les destinations [!DNL Pinterest] sont désormais visibles directement dans l’interface d’Experience Platform. Vous pouvez ainsi voir à quel moment votre authentification arrivera à expiration et la renouveler avant qu’elle ne provoque des interruptions de vos flux de données. Vous pouvez surveiller les dates d’expiration de votre jeton à partir de la colonne **[!UICONTROL Date d’expiration du compte]** dans les onglets **[[!UICONTROL Comptes]](../../destinations/ui/destinations-workspace.md#accounts)** ou **[[!UICONTROL Parcourir]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Amélioration des fonctionnalités de gestion des destinations dans l’interface utilisateur d’Experience Platform | Améliorez votre workflow de gestion des destinations avec de nouvelles fonctionnalités de tri dans les onglets [[!UICONTROL Parcourir]](../../destinations/ui/destinations-workspace.md#browse) et [[!UICONTROL Comptes]](../../destinations/ui/destinations-workspace.md#accounts). Vous pouvez désormais également voir un indicateur visuel lorsque l’authentification de votre compte est sur le point d’expirer. <br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| Paramètres de largeur de colonne persistants | Les paramètres de largeur de colonne persistent désormais lorsque vous quittez une page et y revenez. Par exemple, si vous ajustez la largeur d’une colonne dans l’onglet [[!UICONTROL &#x200B; Parcourir &#x200B;]](../../destinations/ui/destinations-workspace.md#browse), la largeur de votre colonne personnalisée reste la même lorsque vous quittez la page et revenez à cet onglet. |

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences clientes par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Schémas basés sur des modèles | Simplifiez la modélisation des données à l’aide de schémas basés sur des modèles. Vous pouvez désormais créer plus facilement des schémas à l’aide d’exemples et de conseils pratiques complets. Cette fonctionnalité est actuellement disponible pour les titulaires de licence Campaign Orchestration. Elle sera étendue aux clients de Data Distiller lors de la phase de disponibilité générale, ce qui rendra la modélisation des données plus accessible et plus efficace. Cette fonctionnalité prend en charge les données de série temporelle et les fonctionnalités de capture de données de modification. |
| Data Mirror | Ingérez les modifications au niveau des lignes à partir des entrepôts de données cloud (par exemple, Snowflake, Databricks, BigQuery) dans Adobe Experience Platform à l’aide de schémas basés sur des modèles. Data Mirror élimine l’ETL en amont et préserve les relations, le contrôle de version et les suppressions en mettant en miroir les structures de base de données existantes directement dans le lac de données. Les fonctionnalités de capture de données de série temporelle et de schéma d’événement d’enregistrement avec modification sont toutes prises en charge. Cette fonctionnalité est actuellement disponible pour les détenteurs de licence Campaign Orchestration et sera développée dans cette version limitée, y compris pour les clients Customer Journey Analytics. Pour plus d’informations[ consultez la documentation de Data Mirror ](../../xdm/data-mirror/overview.md). Contactez votre représentant Adobe pour obtenir l’accès. |

Pour plus d’informations, consultez la [vue d’ensemble XDM](../../xdm/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de la visionneuse de profils | La version de septembre 2025 comprend les améliorations suivantes pour la visionneuse de profils. <ul><li>**Vue combinée** : les attributs, événements et informations ont été combinés en une seule vue.</li><li>**Informations générées par l’IA** : la page des détails du profil affiche désormais des informations générées par l’IA, vous permettant de connaître les détails générés à partir de votre profil. Ces informations peuvent inclure des informations telles que les scores de propension et l’analyse des tendances.</li><li>**Mise à jour de style** : la page des détails du profil a été actualisée visuellement.</li><li>**Parcourir** : vous pouvez désormais explorer vos profils à l’aide d’un carrousel interactif basé sur une carte avec recherche et personnalisation.</li></ul> |

Pour plus d’informations, consultez la [présentation du profil client en temps réel](../../profile/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Audiences de compte avec événements d’expérience obsolètes | Après la mise à niveau de l’architecture B2B, les audiences de compte avec des événements d’expérience ne sont plus prises en charge. Utilisez plutôt la nouvelle approche de segments : créez une audience Personnes avec des événements d’expérience, puis faites référence à cette audience Personnes lors de la création d’une audience Compte. Cela offre une approche plus flexible et plus gérable de la création d’audiences B2B. |

**Mises à jour importantes**

| Mise à jour  | Description |
| ------- | ----------- |
| Annulation de l’actualisation automatique des estimations d’audience | L’amélioration de l’actualisation automatique pour les estimations d’audience a été annulée. Les estimations d’audience continueront à être générées dans le créateur de segments, mais la fonctionnalité d’actualisation automatique a été supprimée. |
| Audience externe | À compter du 30 septembre, les audiences externes seront récupérées par le biais de la Recherche unifiée dans le créateur de segments. Si vous utilisez la correspondance de segments, vous pouvez activer l’expérience héritée dans le créateur de segments. |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] vue d’ensemble](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles sources en disponibilité générale | Les sources suivantes sont désormais en disponibilité générale : plusieurs connecteurs source ont été mis à jour de Beta vers GA : <ul><li>[Acxiom Data Ingestion](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acxiom Prospect Data Ingestion](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP COMMERCE](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. Ces sources sont désormais entièrement prises en charge et prêtes à être utilisées en production. |
| Prise en charge de l’authentification par paire de clés [!DNL Snowflake] | Amélioration de la sécurité des connexions Snowflake avec prise en charge de l’authentification par paire de clés. L’authentification de base (nom d’utilisateur/mot de passe) sera abandonnée d’ici novembre 2025. Nous recommandons donc aux clients de migrer vers l’authentification par paire de clés pour une sécurité accrue. Pour plus d’informations, consultez la [[!DNL Snowflake] documentation](../../sources/connectors/databases/snowflake.md). |
| Disponibilité générale de la prise en charge des liens privés dans les sources | Vous pouvez désormais utiliser des **liens privés** pour un groupe de sources sélectionné. Utilisez cette fonctionnalité pour créer un point d’entrée privé auquel votre source peut se connecter. Grâce aux points d’entrée privés, vous pouvez configurer des connexions et des flux de données qui contournent l’Internet public, ce qui vous offre une sécurité et un isolement réseau accrus pour vos données sensibles. La prise en charge des liens privés est disponible pour les sources suivantes : <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>. Pour plus d’informations, consultez les guides sur la création de liens privés [dans l’API](../../sources/tutorials/api/private-link.md) et [dans l’interface utilisateur](../../sources/tutorials/ui/private-link.md). |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).

<!--
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | Use the [[!DNL Capillary Streaming Events] source](../../sources/connectors/loyalty/capillary.md) to stream loyalty data from your [!DNL Capillary] account to Experience Platform. |
-->