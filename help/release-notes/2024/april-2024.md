---
title: Notes de mise à jour d’Adobe Experience Platform - Avril 2024
description: Les notes de mise à jour d’avril 2024 pour Adobe Experience Platform.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 28%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 30 avril 2024**

>[!TIP]
>
>Utilisez le glossaire [Adobe Experience Platform](/help/landing/glossary.md) pour vous familiariser avec la terminologie utilisée dans Real-Time Customer Data Platform et Adobe Experience Platform. Si vous ne trouvez pas un terme spécifique que vous recherchez, utilisez les options de commentaires de la page pour demander l’ajout de nouveaux termes au glossaire.

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Tableaux de bord](#dashboards)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Service d’identités](#identity-service)
- [Surveillance](#monitoring)
- [Service de requête](#query-service)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Informations B2B sur Real-Time Customer Data Platform | Explorez les informations préconfigurées sur les données B2B de [Real-Time CDP sur les comptes et les opportunités](../../dashboards/insights/account-profiles.md) pour mieux comprendre vos données et prendre des décisions éclairées. Vous pouvez également [créer vos propres informations à l’aide du modèle de données B2B de Real-Time CDP](../../dashboards/data-models/cdp-insights-data-model-b2c.md) pour visualiser et explorer vos données et enregistrer vos visualisations personnalisées dans votre tableau de bord. |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Extensions | Extension [!DNL Acxiom Anonymous Visitor Insights] Tags | Découvrez d’où viennent les visiteurs et visiteuses de votre site web avec [!DNL Acxiom's Visitor Insights]. En utilisant la technologie de recherche d’adresses IP géographiques, Acxiom peut localiser les navigateurs anonymes. Une fois identifié, une recherche dans leur base de données organisée génère des informations supplémentaires qui sont renvoyées au navigateur. Les créateurs de contenu peuvent ainsi personnaliser leur contenu pour qu’il corresponde à ces points de données, offrant ainsi une expérience plus personnalisée et plus attrayante aux visiteurs, même s’ils ont commencé comme des inconnus. |
| Trains de données | [Détection de robots Edge Network](../../datastreams/bot-detection.md) | Le trafic provenant d’entités non humaines, telles que les programmes automatisés, les web scrapers, les araignées et les scanners scriptés, peut rendre plus difficile l’identification des événements provenant de visiteurs humains. Ce type de trafic peut avoir un impact négatif sur des mesures commerciales importantes, ce qui entraîne des rapports de trafic incorrects. <br>La détection des robots vous permet d’identifier les événements générés par les [Web SDK](../../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) et [[!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/getting-started/) comme étant générés par des araignées et des robots connus. En configurant la détection des robots pour vos flux de données, vous pouvez identifier des adresses IP, des plages d’adresses IP et des en-têtes de requête spécifiques que vous souhaitez classer comme événements de robots. <br> L’identification du trafic de robots peut vous permettre de mesurer plus précisément l’activité des utilisateurs sur votre site ou application mobile. |
| SDK Mobile | Version majeure | De nouvelles versions majeures de Mobile SDK ont été publiées pour les plateformes suivantes : iOS Mobile Core 5.x et extensions iOS compatibles, Android Mobile Core 3.x et extensions Android compatibles, React Native Core 6.x et extensions React Native compatibles, Flutter Core 4.x et extensions Flutter compatibles. Ces versions offrent plusieurs nouvelles fonctionnalités et améliorations, notamment la prise en charge d’Android SDK pour Jetpack Compose, la prise en charge des expériences basées sur du code Adobe Journey Optimizer et la disponibilité générale de l’extension de messagerie Adobe Journey Optimizer pour Flutter. Pour des notes de mise à jour plus détaillées, voir [Notes de mise à jour de Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes/). |
| SDK Mobile | Confidentialité    | En raison de la mise à jour de la politique d’Apple, à compter du 1er mai 2024, les développeurs et les développeuses doivent mettre en œuvre de nouvelles fonctionnalités de confidentialité pour envoyer des emails à App Store. Tous les clients Adobe qui utilisent Mobile SDK devront effectuer la mise à niveau vers la version 5.x de SDK s’ils souhaitent recevoir l’approbation d’App Store après le 1er mai. |
| SDK Roku | SDK Roku | La première version majeure de Roku SDK a été publiée avec la prise en charge de Streaming Media pour Experience Platform Edge Network. |
| Balises et transfert d’événement | Conseils intégrés au produit | Experience Platform [Balises](../../tags/home.md) et [Transfert d’événement](../../tags/ui/event-forwarding/overview.md) offrent une nouvelle gamme d’expériences qui peuvent vous aider à démarrer rapidement et à rentabiliser rapidement votre investissement. Ces expériences comprennent de nouveaux écrans d’intégration, des tutoriels intégrés au produit et des info-bulles. <br>![ Transfert d’événement avec les conseils intégrés au produit mis en surbrillance.](../2024/assets/april/event-forwarding.png "Éditeur de schémas avec les champs Type et Type de valeur de mappage mis en surbrillance."){width="100" zoomable="yes"}<br> |
| SDK Web | Adoption simplifiée de Web SDK pour les clients Audience Manager | Plusieurs mises à jour de Web SDK simplifient désormais l’adoption de Web SDK sans utiliser Experience Data Model (XDM) pour les solutions Experience Cloud telles qu’Audience Manager, Analytics et Target. Pour en savoir plus sur l’adoption d’Audience Manager Web SDK, consultez les guides suivants : <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Mettez à jour votre bibliothèque de collecte de données pour Audience Manager de l’extension de balise Audience Manager à l’extension de balise Web SDK</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Mettez à jour votre bibliothèque de collecte de données pour Audience Manager de la bibliothèque AppMeasurement JavaScript à la bibliothèque Web SDK JavaScript</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Pour en savoir plus sur les collections de données, lisez la [présentation de la collecte de données](../../collection/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalité nouvelle ou mise à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| `isRequired` paramètre désormais disponible pour les champs de données client imbriqués dans Destination SDK | Lors de la configuration d’une destination dans Destination SDK, vous pouvez désormais [définir des champs de données client imbriqués selon vos besoins](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). De cette manière, les utilisateurs qui configurent votre destination ne peuvent pas poursuivre leur flux d’activation tant qu’ils n’ont pas sélectionné une valeur pour ce champ. |
| La segmentation Edge n’est plus obligatoire lors de la configuration d’une destination Adobe Target avec Web SDK | Auparavant, lors de la configuration d’une destination [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) avec Web SDK, le flux de données devait être activé pour la personnalisation et la segmentation Edge. L’exigence selon laquelle le flux de données doit être activé pour la segmentation Edge [a maintenant été supprimée](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Notez que ce modèle d’intégration vous permet uniquement de bénéficier d’un sous-ensemble de cas d’utilisation de la personnalisation lors de l’utilisation d’Adobe Target avec Real-Time CDP. En savoir plus sur le [cas d’utilisation activés par le type d’intégration](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases). |
| [!BADGE Beta ]{type=Informative} supprimer plusieurs audiences et jeux de données des flux d’activation | Vous pouvez désormais sélectionner et supprimer plusieurs audiences et jeux de données des flux d’activation de destination. Consultez la documentation [détails de la destination](../../destinations/ui/destination-details-page.md#bulk-remove) et [exportation du jeu de données](../../destinations/ui/export-datasets.md) pour plus d’informations. |

{style="table-layout:auto"}

Pour obtenir plus d’informations générales sur les destinations, consultez la [vue d’ensemble des destinations](../../destinations/home.md).

## Service d’identités {#identity-service}

Utilisez le service d’identités d’Adobe Experience Platform pour créer une vue complète de votre clientèle et de ses comportements en reliant les identités entre les appareils et les systèmes, vous permettant ainsi de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Obsolescence des points d’entrée `/orgs/{ORG}/` dans l’API | Les points d’entrée suivants de l’API [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) ont été abandonnés :<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Vous pouvez utiliser les points d’entrée `/idnamespace/identities` et `/idnamespace/identities/{ID}` pour accomplir les mêmes tâches et récupérer tous les espaces de noms d’une organisation ou un espace de noms spécifique d’une organisation. |

{style="table-layout:auto"}

Pour plus d’informations sur le service d’identités, consultez la [vue d’ensemble du service d’identités](../../identity-service/home.md).

## Surveillance {#monitoring}

Utilisez le tableau de bord de surveillance de l’interface utilisateur d’Experience Platform pour surveiller le parcours de vos données à partir des sources, du service d’identités, du profil client en temps réel, des audiences et des destinations.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Surveillance de l’extension des tableaux de bord | Vous pouvez désormais utiliser le tableau de bord de surveillance pour différents types de données en fonction de votre cas d’utilisation professionnel. Utilisez le tableau de bord de surveillance pour surveiller les activités de type de données sur les personnes, les comptes et les prospects dans les sources, les audiences et les destinations. |

{style="table-layout:auto"}

Pour plus d’informations, consultez le guide sur [l’utilisation du tableau de bord de surveillance](../../dataflows/ui/monitor.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Quarantaine de requête | Isolez automatiquement les exécutions de requête ayant échoué afin d’éviter les perturbations et de maintenir des performances cohérentes. Pour plus d’informations, consultez la documentation [Quarantaine de requête](../../query-service/ui/query-schedules.md#quarantine). |
| Annuler la requête | Prenez le contrôle de l’exécution des requêtes et améliorez votre productivité en annulant les requêtes de longue durée. Pour plus d’informations, consultez la documentation [annuler la requête](../../query-service/ui/user-guide.md#cancel-query). |
| Alertes de requête planifiées | Tenez-vous informé grâce à des notifications proactives lors de la planification des requêtes, assurant ainsi une gestion efficace et opportune des tâches. Vous pouvez vous [abonner à des alertes lors de la création d’une requête](../../query-service/ui/query-schedules.md#alerts-for-query-status) ou à l’aide d’actions intégrées pour les requêtes planifiées existantes. Pour plus d’informations, consultez la documentation [s’abonner aux alertes avec des actions intégrées](../../query-service/ui/monitor-queries.md#alert-subscription) . |
| Amélioration de la navigation dans les requêtes planifiées | Naviguez facilement entre les modèles de requête et les exécutions planifiées pour une productivité accrue. Pour plus d’informations, consultez la documentation sur l’[affichage des exécutions de requête planifiées](../../query-service/ui/query-schedules.md#scheduled-query-runs). |
| Sortie de requête étendue | Accédez à jusqu’à 500 lignes de résultats de requête dans la console pour une analyse plus approfondie de vos données. Pour plus d’informations, consultez la documentation [nombre de résultats](../../query-service/ui/user-guide.md#result-count). |
| Coucher de soleil de l’ancien Query Editor | Depuis le 30 avril 2024, le Query Editor amélioré est l’éditeur par défaut pour tous les utilisateurs et utilisatrices. L’éditeur hérité sera abandonné le 24 mai 2024 et ne sera plus disponible. Pour plus d’informations, consultez le [guide d’utilisation de Query Editor](../../query-service/ui/user-guide.md). |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, consultez la [vue d’ensemble de Query Service](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Outil Sandbox](../../sandboxes/ui/sandbox-tooling.md) | Utilisez l’outil sandbox pour [exporter](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) tous les types d’objet pris en charge dans un package sandbox complet, puis [importer](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) le package dans différents sandbox afin de répliquer les configurations d’objet. |

{style="table-layout:auto"}

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Experience Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| États du cycle de vie de l’audience | Les états du cycle de vie des audiences ont été rationalisés afin de simplifier la gestion du cycle de vie. Pour en savoir plus sur ces états de cycle de vie, consultez le [FAQ sur Segmentation Service](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Nouvelles sources**

| Nouvelles sources | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Utilisez la [[!DNL PathFactory] source](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) pour intégrer les données relatives aux visiteurs, aux sessions et aux pages vues de [!DNL PathFactory] à Experience Platform. Lisez la [[!DNL PathFactory] présentation](../../sources/connectors/marketing-automation/pathfactory.md) pour plus d’informations sur la prise en main. |
| [!DNL Teradata Vantage] | Utilisez la [[!DNL Teradata Vantage] source](../../sources/tutorials/ui/create/databases/teradata-vantage.md) pour ingérer des données à partir d’environnements multi-cloud hybrides vers Experience Platform. Lisez la [[!DNL Teradata Vantage] présentation](../../sources/connectors/databases/teradata-vantage.md) pour plus d’informations sur la prise en main. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles et mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour des adresses IP pour les listes autorisées dans VA7 | Les adresses IP suivantes ont été ajoutées à la liste des adresses IP à ajouter à votre liste autorisée pour VA7 (Amérique du Nord) : <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Pour obtenir une liste complète des adresses IP à ajouter à votre liste autorisée, consultez le document [ liste autorisée d’adresses IP ](../../sources/ip-address-allow-list.md). |
| Prise en charge de nouveaux types d’authentification avec la source [!DNL Azure Event Hubs] | Vous pouvez désormais connecter votre source de [!DNL Event Hubs] à Experience Platform à l’aide de [!DNL Azure Active Directory Authentication] ou de [!DNL Scoped Azure Active Directory Authentication]. Pour plus d’informations, consultez le guide sur la [connexion [!DNL Event Hubs] à Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md). |
| Mises à jour de la récupération des informations d’identification [!DNL Data Landing Zone] | Vous pouvez maintenant utiliser le rail de droite dans l’espace de travail des sources pour récupérer vos informations d’identification [!DNL Data Landing Zone]. Vous pouvez également utiliser le rail de droite pour actualiser vos informations d’identification. Pour plus d’informations, consultez le [[!DNL Data Landing Zone]  guide de l’interface utilisateur ](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) . |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Pour plus d’informations sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).
