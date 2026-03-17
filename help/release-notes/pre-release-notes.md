---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: efa50881315d986940f7cb3afcbfcc30ef67c3a7
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 28%

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

**Date de publication : mars 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Gestion avancée du cycle de vie des données](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Destinations](#destinations)
- [Service de requête](#query-service)
- [Profil client en temps réel](#profile)
- [Exécuter et exploiter](#run-and-operate)
- [Service de segmentation](#segmentation-service)
- [Sources](#sources)

## Gestion avancée du cycle de vie des données {#advanced-data-lifecycle-management}

Experience Platform offre toute une gamme de fonctionnalités de nettoyage des données. Celles-ci vous permettent de gérer vos données stockées à l’aide de suppressions programmées des enregistrements et des jeux de données des personnes. Depuis l’espace de travail Cycle de vie des données de l’interface d’utilisation ou par le biais d’appels à l’API Data Hygiene, vous pouvez gérer efficacement vos banques de données. Utilisez ces fonctionnalités pour vous assurer que les informations sont utilisées comme prévu, qu’elles sont mises à jour lorsque des données incorrectes doivent être corrigées et qu’elles sont supprimées lorsque les politiques d’entreprise le jugent nécessaire.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Suppression d’enregistrements multi-jeux de données et profil uniquement (API uniquement) | Vous pouvez envoyer un seul identifiant de jeu de données, une liste d’identifiants de jeux de données séparés par des virgules ou l’`ALL` littérale dans `datasetId` de supprimer des identités dans un, plusieurs ou tous les jeux de données. Vous pouvez également limiter la suppression aux services de profil en définissant `targetServices` sur `["identity","profile","ajo"]`, ce qui laisse le lac de données inchangé. Pour plus d’informations[ consultez le guide ](../hygiene/api/workorder.md)Enregistrement des ordres de travail de suppression. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble de la gestion avancée du cycle de vie des données](../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator vous permet de créer et de déployer des agents optimisés par l’IA qui peuvent automatiser les workflows et interagir avec les clients sur plusieurs canaux.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Adobe Marketing Agent pour [!DNL Microsoft 365 Copilot] | Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] est votre agent intégré qui apporte des informations marketing Adobe directement dans les outils quotidiens tels que les applications [!DNL Teams], [!DNL Word], [!DNL PowerPoint] et d’autres applications [!DNL Microsoft 365]. Vous pouvez utiliser cet agent pour extraire des informations de campagne approuvées à partir des applications Adobe lors de la planification de campagnes, de la révision d’audiences ou de la collaboration avec des collègues, pour répondre aux questions des clients et pour prendre des décisions informées basées sur les données sans quitter votre workflow de [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [documentation d’Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| [Diffusion en continu Snowflake](../destinations/catalog/warehouses/snowflake.md) prise en charge multi-région | Le connecteur de streaming Snowflake est désormais disponible pour les clients situés en dehors de la région VA7 des États-Unis. Utilisez le sélecteur de liste déroulante Région pour sélectionner la région Snowflake dans laquelle se trouve votre compte. Mise à jour de la documentation avec la structure de données attendue pour les tables de streaming Snowflake. |
| Sélecteur de zone géographique [Diffusion en continu Snowflake](../destinations/catalog/warehouses/snowflake.md) et [Lot Snowflake](../destinations/catalog/warehouses/snowflake-batch.md) | Vous pouvez désormais trouver plus facilement votre région avec la nouvelle liste déroulante consultable, qui combine la recherche et la liste déroulante en un seul contrôle. |
| Exporter les métadonnées d’audience vers des destinations [Snowflake Batch](../destinations/catalog/warehouses/snowflake-batch.md) | Les fichiers exportés vers cette destination incluent désormais des métadonnées d’audience. La nouvelle structure de tableau s’applique à toutes les nouvelles connexions de destination configurées à l’avenir. L’ancienne structure de tables sera conservée pendant trois mois supplémentaires avant d’être abandonnée. |
| Connexion [!DNL Adobe Advertising Cloud DSP] | La nouvelle connexion Adobe Advertising DSP offre la même fonctionnalité que la connexion héritée, ainsi que la prise en charge d’identités supplémentaires. |
| Prise en charge des audiences externes pour [The Trade Desk CRM](../destinations/catalog/advertising/tradedesk-emails.md), [Criteo](../destinations/catalog/advertising/criteo.md) et [Pinterest](../destinations/catalog/advertising/pinterest.md) | Vous pouvez désormais activer des audiences au-delà des segments Segmentation Service vers The Trade Desk CRM, Criteo et Pinterest, y compris les audiences de chargement personnalisées (importées depuis CSV), les audiences semblables, les audiences fédérées et les audiences créées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer. Pour plus d’informations, consultez la section [audiences prises en charge](../destinations/catalog/advertising/criteo.md#supported-audiences) sur la page de catalogue de chaque destination. |
| Filtrage des audiences dans le workflow d’activation | Vous pouvez désormais rechercher et filtrer des audiences dans l’étape **[!UICONTROL Select audiences]** avec la même expérience que la page Audiences . Par exemple, vous pouvez filtrer par origine d’audience pour trouver facilement l’audience que vous recherchez. |
| Augmentation de la limite des audiences de chargement personnalisées | Vous pouvez désormais activer jusqu’à 20 audiences de chargement personnalisées par instance de destination. Auparavant, cette limite était de 10. |
| Prise en charge de l’[Exporter le fichier maintenant](../destinations/ui/export-file-now.md) et de l’[API d’activation ad hoc](../destinations/api/ad-hoc-activation-api.md) pour les audiences externes | Vous pouvez désormais utiliser Exporter le fichier maintenant (interface utilisateur) et l’API d’activation ad hoc avec des audiences externes (telles que le chargement personnalisé, les audiences semblables, fédérées et provenant d’autres applications Experience Platform) lors de l’activation vers des destinations basées sur des fichiers par lots. |
| Destinations d’API HTTP avec OAuth 2 et mTLS | Vous pouvez désormais créer et authentifier des destinations d’API HTTP qui utilisent OAuth 2 lorsque le point d’entrée d’authentification nécessite un protocole TLS mutuel (mTLS) ; la récupération de jetons lors de la configuration de la destination prend désormais en charge le protocole mTLS. |
| Destination du compte ZoomInfo | Vous pouvez désormais envoyer des audiences de compte à ZoomInfo à partir de Real-Time Customer Data Platform (B2B). |

{style="table-layout:auto"}

**Correctifs et améliorations**

| Correction | Description |
| --- | --- |
| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) validation de l’identifiant de compte | Un programme de validation d’expression régulière a été ajouté à l’étape ID de compte . Lorsque vous saisissez votre identifiant, il est désormais validé afin de s’assurer que l’identifiant de l’organisation et l’identifiant du compte sont au bon format (séparés par un point). |
| [TikTok](../destinations/catalog/social/tiktok.md) hachage du numéro de téléphone du connecteur | Correction d’un problème en raison duquel une mauvaise configuration de la carte de destination signifiait que les identités saisies sur les numéros de téléphone n’étaient pas activées sur TikTok. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../destinations/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Sélecteur de temps des événements de profil | Vous pouvez désormais définir une fenêtre temporelle dans l’onglet Événements de profil pour afficher et analyser les événements de cette plage. Vous pouvez définir la fenêtre temporelle sur 30 jours au maximum. Par défaut, il affiche les événements des dernières 48 heures. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble du profil client en temps réel](../profile/home.md).

## Service de requête {#query-service}

Le service de requête vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Accélérateurs de Distiller de données | Vous pouvez désormais sélectionner un accélérateur dans l’onglet Accélérateurs , saisir les paramètres requis et exécuter ou planifier le code SQL généré sans l’écrire vous-même ; clonez n’importe quel accélérateur dans un modèle personnalisé à modifier. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de Query Service](../query-service/home.md).

## Exécuter et exploiter {#run-and-operate}

Inspectez, dépannez et optimisez vos implémentations Experience Platform à l’aide des outils Exécuter et exploiter . Gagnez de la visibilité sur les activations par lots planifiées, identifiez les problèmes de configuration et améliorez la fiabilité du système.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Plannings de tâches](../run-and-operate/job-schedules.md) disponibilité générale | [!DNL Job Schedules] fournit une vue unifiée de toutes les tâches de traitement par lots planifiées sur votre pipeline de données, de l’ingestion à l’activation de la destination. Inspectez le statut d’exécution, identifiez les conflits de planification et diagnostiquez les problèmes de configuration avant qu’ils n’affectent les opérations de votre entreprise. |
| Disponibilité générale des contrôles d’intégrité | Des configurations de schéma et d’identité médiocres entraînent d’importants problèmes en aval, notamment une création de profil incorrecte, un échec de la qualification du segment et une activation inexacte. <br>Les contrôles d’intégrité permettent de passer d’une approche de dépannage réactif à une maintenance proactive et préventive. Les contrôles d’intégrité sont des analyses permanentes de vos schémas et identités utilisés dans votre sandbox et fournissent un résumé des problèmes que vous pouvez utiliser pour explorer et résoudre les problèmes. |

{style="table-layout:auto"}

Pour plus d’informations, consultez les [Présentation de l’exécution et du fonctionnement](../run-and-operate/overview.md), [Inspecter les plannings de tâches](../run-and-operate/job-schedules.md) et le [Guide de l’interface utilisateur de Platform](../landing/ui-guide.md).

## Service de segmentation {#segmentation}

Experience Platform vous permet de créer des segments d’audience à partir des données de vos clients et de gérer l’ensemble du cycle de vie de ces audiences.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Source d’ingestion dans le Créateur d’audience | Vous pouvez désormais voir si chaque attribut provient d’un lot, d’une source de diffusion en continu ou Edge dans le créateur d’audiences afin d’éviter de créer des audiences de diffusion en continu non valides ou inefficaces. |
| Afficher uniquement les champs contenant des données dans le créateur d’audiences de compte | Vous pouvez désormais filtrer pour n’afficher que les attributs contenant des données lors de la création d’audiences de compte. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des audiences](../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| Prise en charge améliorée de la capture des données de modification | Vous pouvez désormais utiliser la capture de données de modification avec les sources [!DNL Marketo Engage], [!DNL Microsoft Dynamics] et [!DNL Salesforce CRM]. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../sources/home.md).

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

-->