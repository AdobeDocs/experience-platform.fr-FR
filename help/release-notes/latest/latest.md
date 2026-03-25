---
title: Notes de mise à jour d’Adobe Experience Platform - Mars 2026
description: Les notes de mise à jour de mars 2026 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 30b66420e9cee6b4d85cf41a31e9595d5a240fda
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 32%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/latest)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : mercredi 24 mars 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Gestion avancée du cycle de vie des données](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Flux de données](#datastreams)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Profil client en temps réel](#real-time-customer-profile)
- [Segmentation Service](#segmentation-service)
- [Sources](#sources)

## Gestion avancée du cycle de vie des données {#advanced-data-lifecycle-management}

Experience Platform offre toute une gamme de fonctionnalités de nettoyage des données. Celles-ci vous permettent de gérer vos données stockées à l’aide de suppressions programmées des enregistrements et des jeux de données des personnes. En utilisant l’espace de travail Cycle de vie des données dans l’interface utilisateur ou des appels à l’API Data Hygiene, vous pouvez gérer efficacement vos entrepôts de données. Utilisez ces fonctionnalités pour vous assurer que les informations sont utilisées comme prévu, qu’elles sont mises à jour lorsque des données incorrectes doivent être corrigées et qu’elles sont supprimées lorsque les politiques d’entreprise le jugent nécessaire.

| Fonctionnalité | Description |
| --- | --- |
| Suppression d’enregistrements de plusieurs jeux de données et de profils uniquement (API uniquement) | Vous pouvez envoyer un seul identifiant de jeu de données, une liste d’identifiants de jeux de données séparés par des virgules ou l’`ALL` littérale dans `datasetId` de supprimer des identités dans un, plusieurs ou tous les jeux de données. Vous pouvez également limiter la suppression aux services liés aux profils en définissant `targetServices` sur `["identity","profile","ajo"]`, ce qui laisse le lac de données inchangé ; cette fonctionnalité est disponible uniquement via l’API Data Hygiene. Pour plus d’informations, consultez le guide [Ordre de travail de suppression des enregistrements](../../hygiene/api/workorder.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble de la gestion avancée du cycle de vie des données](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator vous permet de créer et de déployer des agents optimisés par l’IA qui peuvent automatiser les workflows et interagir avec les clients sur plusieurs canaux.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Adobe Marketing Agent pour  [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] est votre agent intégré qui apporte des informations marketing Adobe directement dans les outils quotidiens tels que les applications [!DNL Teams], [!DNL Word], [!DNL PowerPoint] et d’autres applications [!DNL Microsoft 365]. Vous pouvez utiliser cet agent pour extraire des informations de campagne approuvées à partir des applications Adobe pendant que vous planifiez des campagnes, révisez des audiences, collaborez avec des collègues pour répondre aux questions des clients et prenez des décisions informées basées sur les données sans quitter votre workflow [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Pour en savoir plus, consultez la [documentation d’Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Flux de données {#datastreams}

Un flux de données représente la configuration côté serveur lors de l’implémentation des SDK Web et Mobile Adobe Experience Platform et de l’API du serveur Edge Network Adobe Experience Platform. La commande de configuration du train de données dans les SDK gère tous les services avec lesquels un client interagit.

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale des configurations de trains de données dynamiques | Les configurations de train de données dynamiques sont désormais disponibles. Les configurations dynamiques de train de données vous permettent de définir des ensembles de règles configurables par l’utilisateur pour chaque service activé pour votre train de données, qui déterminent quelle solution Experience Cloud doit recevoir chaque type de données. Pour plus d’informations, consultez le [guide de configuration des trains de données dynamiques](../../datastreams/configure-dynamic-datastream.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des flux de données](../../datastreams/overview.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| Connexion à [&#128279;](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | La nouvelle connexion Adobe Advertising DSP offre la même fonctionnalité que la connexion héritée, ainsi que la prise en charge d’identités supplémentaires. Avec le nouveau connecteur, vous pouvez également exporter des identités basées sur des cookies vers Adobe Advertising DSP. |
| Connexion [FreeWheel](../../destinations/catalog/advertising/freewheel.md) | Envoyez des audiences [!DNL Real-Time CDP] à FreeWheel sous forme de fichiers par lots quotidiens afin de les cibler dans les offres et campagnes FreeWheel sur CTV, les vidéos et les écrans. Contactez votre équipe de compte Adobe pour obtenir l’accès. |
| Prise en charge des audiences externes pour [The Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) et [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Vous pouvez désormais activer des audiences d’origines autres que Segmentation Service vers The Trade Desk CRM, Criteo et Pinterest, y compris les audiences de chargement personnalisées (importées depuis CSV), les audiences semblables, les audiences fédérées et les audiences créées dans d’autres applications Experience Platform telles que [!DNL Adobe Journey Optimizer]. Cette mise à jour sera déployée jusqu’à la fin du mois de mars. Pour plus d’informations, consultez la section [audiences prises en charge](../../destinations/catalog/advertising/criteo.md#supported-audiences) sur la page de catalogue de chaque destination. |
| Augmentation de la limite des audiences de chargement personnalisées | Vous pouvez désormais activer jusqu’à 20 audiences de chargement personnalisées par instance de destination. Auparavant, cette limite était de 10. Pour plus d’informations, consultez la section [&#x200B; Mécanismes de sécurisation des destinations &#x200B;](../../destinations/guardrails.md#batch-file-based-activation) . |
| Prise en charge de l’[Exporter le fichier maintenant](../../destinations/ui/export-file-now.md) et de l’[API d’activation ad hoc](../../destinations/api/ad-hoc-activation-api.md) pour les audiences externes | Vous pouvez désormais utiliser Exporter le fichier maintenant (interface utilisateur) et l’API d’activation ad hoc avec des audiences externes (telles que le chargement personnalisé, les audiences semblables, fédérées et provenant d’autres applications Experience Platform) lors de l’activation vers des destinations basées sur des fichiers par lots. Cette mise à jour sera déployée jusqu’à la fin du mois de mars. |

{style="table-layout:auto"}

**Correctifs et améliorations**

| Correction | Description |
| --- | --- |
| [&#128279;](../../destinations/catalog/social/tiktok.md) hachage du numéro de téléphone du connecteur | Correction d’un problème en raison duquel une mauvaise configuration de la carte de destination signifiait que les identités saisies sur les numéros de téléphone n’étaient pas activées sur TikTok. Pour bénéficier de ce correctif, configurez un nouveau flux d’activation ou supprimez le mappage des numéros de téléphone de votre flux existant, enregistrez-le et ajoutez-le à nouveau. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences clientes par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des actions d’entité XDM et de la suppression | Accédez aux actions des schémas, classes, groupes de champs et types de données directement à partir des menus de tableau intégrés et des menus d’en-tête de page de détail. Si vous disposez des autorisations requises, vous pouvez également supprimer les entités de votre organisation lorsqu’elles ne sont pas utilisées par des jeux de données et ne sont pas activées pour le profil. Pour plus d’informations, consultez le [guide de l’interface utilisateur XDM](../../xdm/ui/explore.md). |

Pour plus d’informations, consultez la [vue d’ensemble XDM](../../xdm/home.md).

## Profil client en temps réel {#real-time-customer-profile}

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Événements | Vous pouvez désormais définir la période de recherche en amont des événements lors de la navigation dans vos profils. Vous pouvez ainsi voir les événements auxquels le profil est associé pendant la période spécifiée. Pour plus d’informations, consultez le [Guide de l’interface utilisateur de Profile](/help/profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Real-Time Customer Profile] vue d’ensemble](../../profile/home.md).

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Type d’ingestion | Vous pouvez maintenant afficher le type d’ingestion de vos attributs. Vous pouvez ainsi connaître l’origine de vos données et créer de meilleures audiences. Pour plus d’informations sur cette fonctionnalité, consultez le [guide du créateur de segments](/help/segmentation/ui/segment-builder.md). |
| Données de résumé | Vous pouvez désormais afficher les données récapitulatives de vos attributs pour les audiences de compte et basées sur les personnes. Pour plus d’informations sur cette fonctionnalité dans les audiences de compte, consultez le guide sur le compte [Guide du créateur d’audiences](/help/rtcdp/segmentation/audience-builder.md). Pour plus d’informations sur cette fonctionnalité dans les audiences basées sur des personnes, consultez le [guide du créateur de segments](/help/segmentation/ui/segment-builder.md). |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] vue d’ensemble](../../segmentation/home.md).

## Sources

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| [!DNL Talon.One] | Vous pouvez désormais connecter Experience Platform à [!DNL Talon.One] à l’aide des nouvelles sources [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) et [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md). Utilisez les nouvelles sources pour ingérer les données de profil de fidélité, ainsi que les événements d’activité de transaction et de fidélité dans Experience Platform. |
| Nouvelles adresses IP à placer sur la liste autorisée | De nouvelles adresses IP pour GBR9 : Royaume-Uni ont été ajoutées à la liste des adresses que vous devez placer sur la liste autorisée pour assurer la réussite des connexions source par lots à Experience Platform sur Azure. Pour plus d’informations, consultez la liste dans le guide [Adresses IP](../../sources/ip-address-allow-list.md#gbr9-united-kingdom). |
| Prise en charge améliorée de la capture des données de modification | Vous pouvez désormais utiliser la capture de données de modification avec les sources [!DNL Marketo Engage], [!DNL Microsoft Dynamics] et [!DNL Salesforce CRM]. |
| Guide d’authentification amélioré pour [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | Le guide d’authentification de la source [!DNL Google BigQuery] a été étendu avec les informations suivantes : <ul><li>Portées nécessaires pour le jeton d’actualisation.</li><li>Rôles IAM requis pour l’identité [!DNL Google].</li><li>Conseils supplémentaires sur l’utilisation de `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->