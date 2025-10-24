---
title: Notes de mise à jour d’octobre 2025 d’Adobe Experience Platform
description: Les notes de mise à jour d’octobre 2025 pour Adobe Experience Platform
source-git-commit: 0191fc8419c696d8cd114a5eb575b8cc0a815a72
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 26%

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

**Date de publication : jeudi 22 octobre 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Agent Orchestrator](#agent-orchestrator)
- [Alertes](#alerts)
- [Destinations](#destinations)
- [Real-Time CDP B2B Edition](#b2b)
- [Sources](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator est la nouvelle couche agentique d’Adobe Experience Platform.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Agent Audience | Audience Agent prend désormais en charge les audiences basées sur un compte pour l’exploration d’audiences conversationnelles et la détection des audiences en double. Pour en savoir plus, consultez la [documentation de l’agent Audience](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Pour plus d’informations sur les agents, consultez la [documentation Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/home).

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte via l’onglet [!UICONTROL Alerts] de l’interface utilisateur d’Experience Platform et choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par e-mail de notification.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Alerte relative au taux d’échec d’activation | Une nouvelle alerte a été ajoutée pour les destinations : **Le taux d’échec de l’activation dépasse le seuil**. Cette alerte vous avertit lorsque le nombre d’enregistrements ayant échoué lors de l’activation des données a dépassé le seuil autorisé, ce qui vous permet de répondre rapidement aux problèmes d’activation. Pour plus d’informations, consultez la documentation sur les [règles d’alertes standard](../../observability/alerts/rules.md). |

{style="table-layout:auto"}

Pour plus d’informations sur les alertes, consultez la [[!DNL Observability Insights] vue d’ensemble](../../observability/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| [!DNL Adform] | Utilisez cette destination pour envoyer des audiences Adobe Real-Time CDP à [!DNL Adform] pour activation en fonction de l’Experience Cloud ID (ECID) et de l’ID Fusion de [!DNL Adform]. ID Fusion de [!DNL Adform] est un service de résolution d’ID qui vous permet d’activer vos audiences propriétaires en fonction de l’Experience Cloud ID (ECID). Lisez la [[!DNL Adform] documentation](../../destinations/catalog/advertising/adform.md) pour plus d’informations |
| [!DNL Amazon Ads] | Ajout de la prise en charge des identifiants personnels. Cela inclut les champs tels que `firstName`, `lastName`, `street`, `city`, `state`, `zip` et `country`. Le mappage de ces champs en tant qu’identités cibles peut améliorer les taux de correspondance d’audience. Pour plus d’informations, consultez la [[!DNL Amazon Ads] documentation](../../destinations/catalog/advertising/amazon-ads.md) . |
| [!DNL Snowflake Batch] (Disponibilité limitée) | Créez un partage de données Live [!DNL Snowflake] pour recevoir des mises à jour quotidiennes de l’audience directement sous forme de tables partagées dans votre compte . Cette intégration est actuellement disponible pour les organisations clientes configurées dans la région VA7. Pour plus d’informations, consultez la [[!DNL Snowflake Batch] documentation](../../destinations/catalog/warehouses/snowflake-batch.md) . |
| [!DNL Snowflake Streaming] (Disponibilité limitée) | Créez un partage de données Live [!DNL Snowflake] pour recevoir des mises à jour d’audience en flux continu directement sous forme de tables partagées dans votre compte . Cette intégration est actuellement disponible pour les organisations clientes configurées dans la région VA7. Pour plus d’informations, consultez la [[!DNL Snowflake Streaming] documentation](../../destinations/catalog/warehouses/snowflake.md) . |

{style="table-layout:auto"}

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Plusieurs nouvelles destinations qui prennent en charge la surveillance au niveau de l’audience](../../dataflows/ui/monitor-destinations.md#audience-level-view) | Les destinations suivantes prennent désormais en charge la surveillance au niveau de l’audience : <ul><li>[!DNL Airship Tags]</li><li>[!DNL Salesforce Marketing Cloud] (API)</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>Engagement de compte [!DNL Salesforce Marketing Cloud]</li><li>[!DNL The Trade Desk]</li></ul> |
| Correctif des mécanismes de sécurisation de l’exportation des jeux de données | Un correctif a été implémenté pour les mécanismes de sécurisation d’exportation des jeux de données. Auparavant, certains jeux de données qui incluaient une colonne d’horodatage mais n’étaient _pas_ basés sur le schéma XDM Experience Events étaient incorrectement traités comme des jeux de données Experience Events, ce qui limitait les exportations à un intervalle de recherche en amont de 365 jours. Le mécanisme de sécurisation de recherche en amont documenté de 365 jours s’applique désormais exclusivement aux jeux de données d’événements d’expérience. Les jeux de données utilisant un schéma autre que le schéma XDM Experience Events sont désormais régis par le mécanisme de sécurisation de 10 milliards d’enregistrements. Certains clients peuvent voir des nombres d’exportation accrus pour les jeux de données qui se trouvaient par erreur sous l’intervalle de recherche en amont de 365 jours. Vous pouvez ainsi exporter des jeux de données pour les workflows prédictifs disposant d’un long intervalle de recherche en amont. Pour plus d’informations, consultez la section [ Mécanismes de sécurisation d’exportation de jeux de données ](../../destinations/guardrails.md#dataset-exports). |
| Rapports améliorés au niveau de l’audience pour les destinations d’entreprise | Après cette version, les clients verront des chiffres de création de rapports d’audience plus précis qui incluent uniquement les audiences pertinentes pour la destination sélectionnée. Cet ajustement de surveillance garantit que les rapports incluent uniquement les audiences mappées sur le flux de données, ce qui fournit des informations plus claires sur l’activation réelle des données. Cela n’a aucune incidence sur la quantité de données activées. Il s’agit simplement d’une amélioration de la surveillance visant à améliorer la précision des rapports. |
| Flux de données grisés dans l’interface utilisateur en raison de libellés d’accès | Pour résoudre le problème où certains utilisateurs voyaient des pages vierges parce que les flux de données de destination auxquels ils n’avaient pas accès étaient complètement masqués, l’interface utilisateur affiche désormais ces flux de données restreints dans un état grisé au lieu de les omettre entièrement. Pour plus d’informations, consultez la documentation sur l’[utilisation de libellés d’accès pour gérer l’accès des utilisateurs aux flux de données de destination](../../access-control/abac/apply-access-labels-destinations.md#important-callouts-and-items-to-know). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../../destinations/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition offre des fonctionnalités complètes de gestion des données client B2B. Cela permet aux entreprises de créer des profils client unifiés, de créer des audiences B2B sophistiquées et d’activer des données sur divers canaux marketing.

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Obsolescence de la prise en charge B2B pour les relations non standard entre les entités B2B | À compter de janvier 2026, Real-Time CDP B2B edition ne prendra plus en charge les relations **non standard** entre les entités B2B. Par conséquent, nous vous recommandons de mettre à jour vos entités B2B pour utiliser les relations standard décrites dans le guide [ Espaces de noms et schémas B2B ](../../rtcdp/schemas/b2b.md). |

{style="table-layout:auto"}

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Modification de la création du jeu de données pour la source Adobe Analytics | Dans le cadre du processus de création de flux de données entre Adobe Analytics et Experience Platform, un jeu de données est créé via le service de catalogue. Ce jeu de données sert de conteneur pour les données à introduire. Actuellement, ce processus implique un identifiant de source de données extrait de la suite de rapports Analytics, envoyé au service de catalogue, puis associé au jeu de données nouvellement créé. Après la modification, l’option permettant de fournir l’identifiant de source de données ne sera plus disponible lors de la création du jeu de données. Par conséquent, les nouveaux jeux de données créés par la source Analytics n’auront plus d’ID de source de données associé dans le service de catalogue. Cette modification s’applique uniquement aux métadonnées et ne modifie en rien le stockage des données dans le jeu de données. Cependant, il est important de savoir que l’identifiant de source de données fourni par Catalog Service ne sera plus disponible dans les jeux de données nouvellement créés pour Adobe Analytics. Lisez la [documentation sur la source Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md) pour plus d’informations sur le connecteur source Adobe Analytics. |
| Disponibilité générale de la source [!DNL Google Ads] (API uniquement) | La version [API de la source  [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md) est désormais en disponibilité générale. La documentation de l’API a été mise à jour afin de refléter le fait que la dernière version est désormais `v21` et qu’Experience Platform prend en charge toutes les versions v19 et ultérieures. [la version de l’interface utilisateur](../../sources/tutorials/ui/create/advertising/ads.md) reste en version bêta et ne prend en charge qu’une ingestion unique. Pour utiliser l’ingestion de données incrémentielle, utilisez l’itinéraire d’API. |
| Prise en charge du réseau virtuel [!DNL Azure Event Hubs] | Adobe prend désormais explicitement en charge les connexions réseau virtuelles à [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md), ce qui permet le transfert de données sur des réseaux privés plutôt que sur des réseaux publics. Placer sur la liste autorisée Les clients peuvent utiliser Experience Platform VNet pour acheminer le trafic Event Hubs de manière privée via la dorsale principale privée Azure, offrant ainsi une sécurité et une conformité améliorées aux workflows d’ingestion de données. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->