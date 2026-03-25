---
title: Notes de mise à jour d’Adobe Experience Platform - Mars 2026
description: Les notes de mise à jour de mars 2026 pour Adobe Experience Platform.
exl-id: 66b948fd-caa0-4e5e-83dd-3b15b77c09fa
source-git-commit: 6b6a03fb8675ed01dd255f7206b23b05c809f2a6
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 21%

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

Experience Platform offre toute une gamme de fonctionnalités d’hygiène des données pour vous aider à gérer vos données stockées par le biais de suppressions par programmation des jeux de données et des enregistrements des clients. En utilisant l’espace de travail Cycle de vie des données dans l’interface utilisateur ou des appels à l’API Data Hygiene, vous pouvez gérer efficacement vos entrepôts de données. Utilisez ces fonctionnalités pour vous assurer que les informations sont utilisées comme prévu, qu’elles sont mises à jour lorsque des données incorrectes doivent être corrigées et qu’elles sont supprimées lorsque les politiques d’entreprise le jugent nécessaire.

| Fonctionnalité | Description |
| --- | --- |
| Suppression d’enregistrements de plusieurs jeux de données et de profils uniquement (API uniquement) | Vous pouvez envoyer un seul identifiant de jeu de données, une liste d’identifiants de jeux de données séparés par des virgules ou l’`ALL` littérale dans `datasetId` de supprimer des identités dans un, plusieurs ou tous les jeux de données. Vous pouvez également limiter la suppression aux services liés aux profils en définissant `targetServices` sur `["identity","profile","ajo"]`, ce qui laisse le lac de données inchangé ; cette fonctionnalité est disponible uniquement via l’API Data Hygiene. Pour plus d’informations, consultez le guide [Ordre de travail de suppression des enregistrements](../../hygiene/api/workorder.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble de la gestion avancée du cycle de vie des données](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Utilisez Agent Orchestrator pour créer et déployer des agents optimisés par l’IA qui automatisent les workflows et interagissent avec les clients sur plusieurs canaux.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Adobe Marketing Agent pour  [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] est votre agent intégré qui apporte des informations marketing Adobe directement dans les outils quotidiens tels que les applications [!DNL Teams], [!DNL Word], [!DNL PowerPoint] et d’autres applications [!DNL Microsoft 365]. Vous pouvez utiliser cet agent pour extraire des informations de campagne approuvées à partir des applications Adobe pendant que vous planifiez des campagnes, révisez des audiences, collaborez avec des collègues pour répondre aux questions des clients et prenez des décisions informées basées sur les données sans quitter votre workflow [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Pour en savoir plus, consultez la [documentation d’Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Flux de données {#datastreams}

Un flux de données représente la configuration côté serveur lors de l’implémentation des SDK Web et Mobile Adobe Experience Platform et de l’API du serveur Edge Network Adobe Experience Platform. La commande de configuration du train de données dans les SDK gère tous les services avec lesquels un client interagit.

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale des configurations de trains de données dynamiques | Les configurations de train de données dynamiques sont désormais disponibles. Avec les configurations de train de données dynamiques, vous pouvez définir des ensembles de règles configurables par l’utilisateur pour chaque service activé pour votre train de données, qui déterminent quelle solution Experience Cloud doit recevoir chaque type de données. Pour plus d’informations, consultez le [guide de configuration des trains de données dynamiques](../../datastreams/configure-dynamic-datastream.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des flux de données](../../datastreams/overview.md).

## Destinations {#destinations}

[!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination. Utilisez les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| Sélecteur de zone géographique [Lot &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md) | Vous pouvez désormais trouver plus facilement votre région avec la nouvelle liste déroulante consultable, qui combine la recherche et la liste déroulante en un seul contrôle. Cette mise à jour sera déployée jusqu’à la fin du mois de mars. |
| Nouvelle structure de table pour les destinations [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) | Les tables partagées dans votre compte Snowflake ont désormais une nouvelle structure qui inclut des colonnes distinctes de nom d’audience et d’origine d’audience. La nouvelle structure de tableau s’applique à toutes les nouvelles connexions de destination configurées à l’avenir. Pour toutes les nouvelles connexions que vous configurez, les deux structures de table sont créées : la nouvelle structure comporte le préfixe V2 et l’ancienne structure est conservée jusqu’à la fin du mois de juin 2026, après quoi elle sera abandonnée. Pour en savoir plus, consultez la section [Données exportées](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) de la documentation par lots de Snowflake. Cette mise à jour sera déployée jusqu’à la fin du mois de mars. |
| Connexion à [&#128279;](../../destinations/catalog/advertising/adobe-advertising-dsp-connection.md) | La nouvelle connexion Adobe Advertising DSP offre la même fonctionnalité que la connexion héritée, ainsi que la prise en charge d’identités supplémentaires. Avec le nouveau connecteur, vous pouvez également exporter des identités basées sur des cookies vers Adobe Advertising DSP. |
| Connexion [FreeWheel](../../destinations/catalog/advertising/freewheel.md) | Envoyez des audiences [!DNL Real-Time CDP] à FreeWheel sous forme de fichiers par lots quotidiens afin de les cibler dans les offres et campagnes FreeWheel sur CTV, les vidéos et les écrans. Contactez votre équipe de compte Adobe pour obtenir l’accès. |
| Prise en charge des audiences externes pour [The Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) et [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Vous pouvez désormais activer des audiences d’origines autres que Segmentation Service vers The Trade Desk CRM, Criteo et Pinterest, y compris les audiences de chargement personnalisées (importées depuis CSV), les audiences semblables, les audiences fédérées et les audiences créées dans d’autres applications Experience Platform telles que [!DNL Adobe Journey Optimizer]. Cette mise à jour sera déployée jusqu’à la fin du mois de mars. Pour plus d’informations, consultez la section [audiences prises en charge](../../destinations/catalog/advertising/criteo.md#supported-audiences) sur la page de catalogue de chaque destination. |
| Augmentation de la limite des audiences de chargement personnalisées | Vous pouvez désormais activer jusqu’à 20 audiences de chargement personnalisées par instance de destination. Auparavant, cette limite était de 10. Pour plus d’informations, consultez la section [&#x200B; Mécanismes de sécurisation des destinations &#x200B;](../../destinations/guardrails.md#batch-file-based-activation) . |
| Prise en charge de l’[Exporter le fichier maintenant](../../destinations/ui/export-file-now.md) et de l’[API d’activation ad hoc](../../destinations/api/ad-hoc-activation-api.md) pour les audiences externes | Vous pouvez désormais utiliser Exporter le fichier maintenant (interface utilisateur) et l’API d’activation ad hoc avec des audiences externes (telles que le chargement personnalisé, les audiences semblables, fédérées et provenant d’autres applications Experience Platform) lors de l’activation vers des destinations basées sur des fichiers par lots. Cette mise à jour sera déployée jusqu’à la fin du mois de mars. |
| Destinations [API HTTP](../../destinations/catalog/streaming/http-destination.md) avec OAuth 2 et mTLS | Vous pouvez désormais créer et authentifier des destinations d’API HTTP qui utilisent OAuth 2 lorsque le point d’entrée d’authentification nécessite un protocole TLS mutuel (mTLS) ; la récupération de jetons lors de la configuration de la destination prend désormais en charge le protocole mTLS. Cette mise à jour sera déployée jusqu’à la fin du mois de mars. |

{style="table-layout:auto"}

**Correctifs et améliorations**

| Correction | Description |
| --- | --- |
| [&#128279;](../../destinations/catalog/social/tiktok.md) hachage du numéro de téléphone du connecteur | Correction d’un problème en raison duquel une mauvaise configuration de la carte de destination signifiait que les identités saisies sur les numéros de téléphone n’étaient pas activées sur TikTok. Pour bénéficier de ce correctif, configurez un nouveau flux d’activation ou supprimez le mappage des numéros de téléphone de votre flux existant, enregistrez-le et ajoutez-le à nouveau. |
| Validation de l’identifiant de compte [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) et [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) | Un programme de validation d’expression régulière a été ajouté à l’étape ID de compte . Lorsque vous saisissez votre identifiant, il est désormais validé afin de s’assurer que l’identifiant de l’organisation et l’identifiant du compte sont au bon format (séparés par un point). Cette mise à jour sera déployée jusqu’à la fin du mois de mars. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences clientes par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des actions d’entité XDM et de la suppression | Accédez aux actions des schémas, classes, groupes de champs et types de données directement à partir des menus de tableau intégrés et des menus d’en-tête de page de détail. Si vous disposez des autorisations requises, vous pouvez également supprimer les entités de votre organisation lorsqu’elles ne sont pas utilisées par des jeux de données et ne sont pas activées pour le profil. Pour plus d’informations, consultez le [guide de l’interface utilisateur XDM](../../xdm/ui/explore.md). |

Pour plus d’informations, consultez la [vue d’ensemble XDM](../../xdm/home.md).

## Profil client en temps réel {#real-time-customer-profile}

Le profil client en temps réel offre une vue complète de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Utilisez le profil pour consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Événements | Vous pouvez désormais définir la période de recherche en amont des événements lors de la navigation dans vos profils. Vous pouvez ainsi voir les événements auxquels le profil est associé pendant la période spécifiée. Pour plus d’informations, consultez le [Guide de l’interface utilisateur de Profile](../../profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Real-Time Customer Profile] vue d’ensemble](../../profile/home.md).

## Exécuter et exploiter {#run-and-operate}

Inspectez, dépannez et optimisez vos implémentations Experience Platform à l’aide des outils Exécuter et exploiter . Gagnez de la visibilité sur les activations par lots planifiées, identifiez les problèmes de configuration et améliorez la fiabilité du système.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Plannings de tâches](../../run-and-operate/job-schedules.md) disponibilité générale | [!DNL Job Schedules] fournit une vue unifiée de toutes les tâches de traitement par lots planifiées sur votre pipeline de données, de l’ingestion à l’activation de la destination. Inspectez le statut d’exécution, identifiez les conflits de planification et diagnostiquez les problèmes de configuration avant qu’ils n’affectent les opérations de votre entreprise. |
| [Contrôles d’intégrité](../../run-and-operate/health-checks.md) disponibilité générale | Des configurations de schéma et d’identité médiocres entraînent d’importants problèmes en aval, notamment une création de profil incorrecte, un échec de la qualification du segment et une activation inexacte. <br>Les contrôles d’intégrité permettent de passer d’une approche de dépannage réactif à une maintenance proactive et préventive. Les contrôles d’intégrité sont des analyses permanentes de vos schémas et identités utilisés dans votre sandbox et fournissent un résumé des problèmes que vous pouvez utiliser pour explorer et résoudre les problèmes. |

{style="table-layout:auto"}

Pour plus d’informations, consultez les [Présentation de l’exécution et du fonctionnement](../../run-and-operate/overview.md), [Inspecter les plannings de tâches](../../run-and-operate/job-schedules.md) et le [Guide de l’interface utilisateur de Platform](../../landing/ui-guide.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Type d’ingestion | Vous pouvez maintenant afficher le type d’ingestion de vos attributs. Vous pouvez ainsi connaître l’origine de vos données et créer de meilleures audiences. Pour plus d’informations sur cette fonctionnalité, consultez le [guide du créateur de segments](../../segmentation/ui/segment-builder.md). |
| Données de résumé | Vous pouvez désormais afficher les données récapitulatives de vos attributs pour les audiences de compte et basées sur les personnes. Pour plus d’informations sur cette fonctionnalité dans les audiences de compte, consultez le guide sur le compte [Guide du créateur d’audiences](../../rtcdp/segmentation/audience-builder.md). Pour plus d’informations sur cette fonctionnalité dans les audiences basées sur des personnes, consultez le [guide du créateur de segments](../../segmentation/ui/segment-builder.md). |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] vue d’ensemble](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Utilisez ces connexions source pour vous authentifier et vous connecter à des systèmes de stockage externes et à des services CRM, définir des heures d’exécution de l’ingestion et gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| Nouvelles adresses IP à placer sur la liste autorisée | De nouvelles adresses IP pour GBR9 : Royaume-Uni ont été ajoutées à la liste des adresses que vous devez placer sur la liste autorisée pour assurer la réussite des connexions source par lots à Experience Platform sur Azure. Pour plus d’informations, consultez la liste dans le guide [Adresses IP](../../sources/ip-address-allow-list.md#gbr9-united-kingdom). |
| Prise en charge améliorée de la capture des données de modification | Vous pouvez désormais utiliser la capture de données de modification avec les sources [!DNL Marketo Engage], [!DNL Microsoft Dynamics] et [!DNL Salesforce CRM]. |
| Guide d’authentification amélioré pour [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | Le guide d’authentification de la source [!DNL Google BigQuery] a été étendu avec les informations suivantes : <ul><li>Portées nécessaires pour le jeton d’actualisation.</li><li>Rôles IAM requis pour l’identité [!DNL Google].</li><li>Conseils supplémentaires sur l’utilisation de `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).
