---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour d’avril 2024 pour Adobe Experience Platform.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: 14dccb993b38ca352c6de3ed851bafe7c44ca631
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 25%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 30 avril 2024**

>[!TIP]
>
>Utilisez le [glossaire Adobe Experience Platform](/help/landing/glossary.md) pour vous familiariser avec la terminologie utilisée dans Real-Time Customer Data Platform et Adobe Experience Platform. Si vous ne trouvez pas de terme spécifique que vous recherchez, utilisez les options de commentaire de la page pour demander l’ajout de nouveaux termes au glossaire.

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Tableaux de bord](#dashboards)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Service d’identités](#identity-service)
- [Surveillance](#monitoring)
- [Query Service](#query-service)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Real-Time Customer Data Platform B2B insights | Explorez les [insights de données B2B de Real-Time CDP préconfigurés sur les comptes et les opportunités](../../dashboards/insights/account-profiles.md) pour vous aider à comprendre vos données et à prendre des décisions professionnelles. Vous pouvez également [créer vos propres insights à l’aide du modèle de données Real-Time CDP B2B](../../dashboards/data-models/cdp-insights-data-model-b2c.md) pour visualiser et explorer vos données et enregistrer vos visualisations personnalisées dans votre tableau de bord. |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permet de collecter des données d’expérience client côté client et de les envoyer à l’Edge Network Experience Platform où elles peuvent être enrichies, transformées et distribuées vers des destinations Adobe ou non Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Extensions | [!DNL Acxiom Anonymous Visitor Insights] Extension de balises | Découvrez d’où viennent les visiteurs de votre site web avec [!DNL Acxiom's Visitor Insights]. En utilisant la technologie de recherche de géolocalisation des adresses IP, Acxiom peut localiser les navigateurs anonymes. Une fois identifiée, une recherche dans leur base de données organisée apporte des informations supplémentaires qui sont renvoyées au navigateur. Les créateurs de contenu peuvent ainsi personnaliser leur contenu pour qu’il corresponde à ces points de données, ce qui offre une expérience plus personnalisée et attrayante aux visiteurs, même s’ils ont commencé comme des étrangers. |
| Trains de données | [Détection de robots Edge Network](../../datastreams/bot-detection.md) | Le trafic provenant d’entités non humaines, telles que les programmes automatisés, les web-scrapers, les araignées, les scanneurs à scripts, peut rendre plus difficile l’identification des événements provenant de visiteurs humains. Ce type de trafic peut avoir une incidence négative sur les mesures commerciales importantes, ce qui entraîne des rapports de trafic incorrects. <br>La détection des robots vous permet d’identifier les événements générés par le [SDK Web](../../web-sdk/home.md), le [SDK mobile](https://developer.adobe.com/client-sdks/home/) et le [[!DNL Server API]](../../server-api/overview.md) comme étant générés par des araignées et des robots connus. En configurant la détection des robots pour vos flux de données, vous pouvez identifier des adresses IP, des plages d’adresses IP et des en-têtes de requête spécifiques que vous souhaitez classer comme événements de robots. <br> L’identification du trafic de robots peut vous fournir une mesure plus précise de l’activité des utilisateurs sur votre site ou application mobile. |
| SDK Mobile | Version majeure | De nouvelles versions majeures du SDK Mobile ont été publiées pour les plateformes suivantes : iOS Mobile Core 5.x et les extensions iOS compatibles, Android Mobile Core 3.x et les extensions Android compatibles, React Native Core 6.x et les extensions React Native compatibles, FbattCore 4.x et les extensions Fbattage compatibles. Ces versions contiennent plusieurs nouvelles fonctionnalités et améliorations, notamment la prise en charge du SDK Android pour Jetpack Composer, la prise en charge d’expériences basées sur le code Adobe Journey Optimizer et la disponibilité générale de l’extension de messagerie Adobe Journey Optimizer pour FSaisir. Pour obtenir des notes de mise à jour plus détaillées, reportez-vous à la section [Notes de mise à jour du SDK Mobile](https://developer.adobe.com/client-sdks/home/release-notes/). |
| SDK Mobile | Confidentialité    | En raison de la mise à jour de la stratégie Apple, à compter du 1er mai 2024, les développeurs doivent mettre en oeuvre de nouvelles fonctionnalités de confidentialité pour se soumettre à App Store. Tous les clients Adobe qui utilisent le SDK Mobile devront effectuer une mise à niveau vers la version 5.x du SDK s’ils souhaitent recevoir l’approbation d’App Store après le 1er mai. |
| SDK Roku | SDK Roku | La première version majeure du SDK Roku a été publiée avec la prise en charge des médias en flux continu pour l’Edge Network Platform. |
| Balises et transfert d’événement | Conseils intégrés aux produits | Les [balises](../../tags/home.md) et le [transfert d’événement](../../tags/ui/event-forwarding/overview.md) Experience Platform offrent une nouvelle gamme d’expériences qui peuvent vous aider à démarrer rapidement et à obtenir un temps de valeur rapide. Ces expériences incluent de nouveaux écrans d’intégration, des tutoriels intégrés au produit et des info-bulles. <br>![Transfert d’événement avec la recommandation intégrée au produit mise en évidence.](../2024/assets/april/event-forwarding.png "L’éditeur de schémas avec les champs Type et Type de valeur de carte mis en surbrillance."){width="100" zoomable="yes"}<br> |
| SDK Web | adoption simplifiée du SDK Web pour les clients Audience Manager | Plusieurs mises à jour du SDK Web simplifient désormais l’adoption du SDK Web sans utiliser le modèle de données d’expérience (XDM) pour les solutions Experience Cloud, telles que Audience Manager, Analytics et Target. Pour en savoir plus sur l’adoption du SDK Web d’Audience Manager, consultez les guides suivants : <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Mettez à jour votre bibliothèque de collecte de données pour l’Audience Manager de l’extension de balise d’Audience Manager vers l’extension de balise du SDK Web.</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Mettez à jour votre bibliothèque de collecte de données pour l’Audience Manager de la bibliothèque JavaScript AppMeasurement vers la bibliothèque JavaScript SDK Web</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Pour en savoir plus sur les collections de données, consultez la [présentation de la collecte de données](../../collection/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Paramètre `isRequired` désormais disponible pour les champs de données client imbriqués dans Destination SDK | Lors de la configuration d’une destination dans Destination SDK, vous pouvez désormais [définir des champs de données client imbriqués comme requis](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). Ainsi, les utilisateurs configurant votre destination ne peuvent pas poursuivre leur flux d’activation tant qu’ils n’ont pas sélectionné une valeur pour ce champ. |
| La segmentation Edge n’est plus obligatoire lors de la configuration d’une destination Adobe Target avec SDK Web. | Auparavant, lors de la configuration d’une [destination Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) avec le SDK Web, la banque de données devait être activée pour la personnalisation et la segmentation Edge. L’exigence que le flux de données soit activé pour la segmentation Edge [a été supprimée ](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Notez que ce modèle d’intégration vous permet uniquement de bénéficier d’un sous-ensemble de cas d’utilisation de la personnalisation lors de l’utilisation d’Adobe Target avec Real-Time CDP. En savoir plus sur les [cas d’utilisation activés par type d’intégration](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases). |
| [!BADGE Beta]{type=Informative} Supprimer plusieurs audiences et jeux de données des flux d’activation | Vous pouvez désormais sélectionner et supprimer plusieurs audiences et jeux de données des flux d’activation de destination. Pour plus d’informations, consultez la documentation [détails de destination](../../destinations/ui/destination-details-page.md#bulk-remove) et [ exportation de jeux de données](../../destinations/ui/export-datasets.md) . |

{style="table-layout:auto"}

Pour obtenir plus d’informations générales sur les destinations, consultez la [vue d’ensemble des destinations](../../destinations/home.md).

## Service d’identités {#identity-service}

Utilisez Adobe Experience Platform Identity Service pour créer une vue d’ensemble complète de vos clients et de leurs comportements en rapprochant des identités entre les appareils et les systèmes, ce qui vous permet de fournir des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Obsolescence des points d’entrée `/orgs/{ORG}/` dans l’API | Les points de terminaison suivants de l’[[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) ont été abandonnés :<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Vous pouvez utiliser les points de terminaison `/idnamespace/identities` et `/idnamespace/identities/{ID}` pour accomplir les mêmes tâches et récupérer tous les espaces de noms d’une organisation ou un espace de noms spécifique d’une organisation. |

{style="table-layout:auto"}

Pour plus d’informations sur le service d’identités, consultez la [présentation du service d’identités](../../identity-service/home.md).

## Surveillance {#monitoring}

Utilisez le tableau de bord de surveillance dans l’interface utilisateur de l’Experience Platform pour surveiller le parcours de vos données à partir de sources, d’Identity Service, de Real-Time Customer Profile, d’audiences et de destinations.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Surveillance de l’extension du tableau de bord | Vous pouvez désormais utiliser le tableau de bord de surveillance pour différents types de données en fonction de votre cas d’utilisation professionnel. Utilisez le tableau de bord de surveillance pour surveiller les activités de type de données de personnes, de comptes et de prospects dans les sources, les audiences et les destinations. |

{style="table-layout:auto"}

Pour plus d&#39;informations, consultez le guide sur [à l&#39;aide du tableau de bord de surveillance](../../dataflows/ui/monitor.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Quarantaine de requête | isoler automatiquement les exécutions de requête ayant échoué afin d’éviter des perturbations et de maintenir des performances homogènes. Pour plus d’informations, consultez la documentation [mise en quarantaine des requêtes](../../query-service/ui/query-schedules.md#quarantine) . |
| Annuler la requête | Contrôlez l’exécution des requêtes et améliorez votre productivité en annulant les requêtes longues. Pour plus d’informations, consultez la documentation [Annuler la requête](../../query-service/ui/user-guide.md#cancel-query) . |
| Alertes de requête planifiées | Tenez compte des notifications proactives tout en planifiant les requêtes, ce qui vous permet de garantir une gestion efficace et opportune des tâches. Vous pouvez [ vous abonner aux alertes lors de la création d&#39;une requête ](../../query-service/ui/query-schedules.md#alerts-for-query-status) ou à l&#39;aide des actions intégrées pour les requêtes planifiées existantes. Pour plus d’informations, consultez la documentation [abonner aux alertes avec des actions intégrées](../../query-service/ui/monitor-queries.md#alert-subscription) . |
| Amélioration de la navigation des requêtes planifiées | Naviguez facilement entre les modèles de requête et les exécutions planifiées pour accroître la productivité. Pour plus d’informations, consultez la documentation sur l’ [affichage des exécutions de requête planifiées](../../query-service/ui/query-schedules.md#scheduled-query-runs) . |
| Sortie de requête étendue | Accédez à jusqu’à 500 lignes de résultats de requête dans la console pour une analyse plus approfondie de vos données. Pour plus d’informations, consultez la documentation [result count](../../query-service/ui/user-guide.md#result-count) . |
| Jeu de soleil de l’ancien Query Editor | Depuis le 30 avril 2024, l’éditeur de requêtes amélioré est devenu l’éditeur par défaut pour tous les utilisateurs. L’ancien éditeur sera abandonné les 24 et 24 mai 2024 et ne sera plus disponible. Pour plus d’informations, consultez le [guide d’utilisation de Query Editor](../../query-service/ui/user-guide.md) . |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, consultez la [vue d’ensemble de Query Service](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Outil Sandbox](../../sandboxes/ui/sandbox-tooling.md) | Utilisez l’outil d’environnement de test pour [exporter](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) tous les types d’objets pris en charge dans un package d’environnement de test complet, puis [importer](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) le package dans différents environnements de test pour répliquer les configurations d’objet. |

{style="table-layout:auto"}

Pour plus d’informations sur les environnements de test, consultez la [présentation des environnements de test](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| États du cycle de vie de l’audience | Les états du cycle de vie de l’audience ont été rationalisés afin de simplifier la gestion du cycle de vie. Pour en savoir plus sur ces états de cycle de vie, consultez la [FAQ sur Segmentation Service](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Nouvelles sources**

| Nouvelles sources | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Utilisez la [[!DNL PathFactory] source](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) pour intégrer les données de vos visiteurs, sessions et pages vues de [!DNL PathFactory] à votre Experience Platform. Lisez la [[!DNL PathFactory] présentation](../../sources/connectors/marketing-automation/pathfactory.md) pour plus d’informations sur la façon de commencer. |
| [!DNL Teradata Vantage] | Utilisez la [[!DNL Teradata Vantage] source](../../sources/tutorials/ui/create/databases/teradata-vantage.md) pour ingérer des données à partir d’environnements multicloud hybrides vers Experience Platform. Lisez la [[!DNL Teradata Vantage] présentation](../../sources/connectors/databases/teradata-vantage.md) pour plus d’informations sur la façon de commencer. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles et mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour des adresses IP pour les listes autorisées dans VA7 | Les adresses IP suivantes ont été ajoutées à la liste des adresses IP à ajouter à votre liste autorisée pour VA7 (Amérique du Nord) : <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Pour obtenir une liste complète des adresses IP à ajouter à votre liste autorisée, lisez le document [liste autorisée d’adresses IP](../../sources/ip-address-allow-list.md). |
| Prise en charge de nouveaux types d’authentification avec la source [!DNL Azure Event Hubs] | Vous pouvez désormais connecter votre source [!DNL Event Hubs] à l’Experience Platform à l’aide de [!DNL Azure Active Directory Authentication] ou de [!DNL Scoped Azure Active Directory Authentication]. Pour plus d’informations, consultez le guide sur la [connexion [!DNL Event Hubs] à l’Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) . |
| Mises à jour de la récupération des informations d’identification [!DNL Data Landing Zone] | Vous pouvez désormais utiliser le rail de droite dans l’espace de travail des sources pour récupérer vos informations d’identification [!DNL Data Landing Zone]. Vous pouvez également désormais utiliser le rail de droite pour actualiser vos informations d’identification. Pour plus d’informations, consultez le [[!DNL Data Landing Zone] guide de l’interface utilisateur](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) . |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Pour plus d’informations sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).
