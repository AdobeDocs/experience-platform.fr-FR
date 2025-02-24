---
title: Notes de mise à jour d’Adobe Experience Platform - Février 2025
description: Les notes de mise à jour de février 2025 pour Adobe Experience Platform.
source-git-commit: 300be2f922f81f0666a794815cb27777802efb60
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 21%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Cette version comprend des améliorations du module complémentaire Composition de l’audience fédérée . Pour plus d’informations, consultez les [notes de mise à jour de la composition d’audiences fédérées](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes).

**Date de mise à jour : mercredi 18 février 2025**

Mises à jour des fonctionnalités et de la documentation existantes dans Adobe Experience Platform :

- [Assistant IA](#ai-assistant)
- [Catalog Service](#catalog-service)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Sources](#sources)
- [Mises à jour de la documentation](#documentation-updates)
   - [Comparaison entre le réseau et le hub Edge](#edge)
   - [API Flow Service développée pour les sources](#flow-service)
   - [Sauvegarde des configurations d’objet à l’aide de l’outil Sandbox](#back-up-object-configurations)
   - [Activer un centre d’excellence à l’aide de l’outil Sandbox](#center-of-excellence)
   - [Conservation du jeu de données d’événement d’expérience dans le lac de données](#experience-event-dataset-retention)

## Assistant IA {#ai-assistant}

L’Assistant IA dans Adobe Experience Platform est une expérience conversationnelle que vous pouvez utiliser pour accélérer vos workflows dans les applications Adobe. Vous pouvez utiliser l’Assistant IA pour développer vos connaissances sur le produit, résoudre les problèmes ou rechercher des informations et trouver des informations opérationnelles. L’assistant AI prend en charge Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale des informations opérationnelles | Les informations opérationnelles sur l’assistant d’IA sont désormais disponibles en disponibilité générale. Les informations opérationnelles se rapportent aux réponses que l’assistant AI génère sur vos objets de métadonnées (attributs, audiences, flux de données, jeux de données, destinations, parcours, schémas et sources), y compris les nombres, les recherches et l’impact de la parenté. Les informations opérationnelles n’examinent aucune donnée dans le sandbox. Pour plus d’informations, consultez le guide de l’interface utilisateur de l’assistant [AI](../../ai-assistant/ui-guide.md). |
| Prise en charge de la saisie semi-automatique des questions | Lors de la saisie d’une question dans l’assistant AI, vous pouvez désormais effectuer une sélection dans une liste de questions recommandées que l’assistant AI fournit. Utilisez cette fonctionnalité pour accélérer davantage vos workflows avec l’assistant d’IA. Pour plus d’informations, consultez le guide sur l’[utilisation de la saisie automatique des questions avec l’assistant AI](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Prise en charge de l’observabilité des jeux de données | Vous pouvez désormais utiliser l’assistant AI pour répondre aux questions sur des mesures de jeux de données spécifiques, telles que les tailles de stockage et le nombre de lignes. Les questions d’observabilité des données prennent en charge les qualificateurs que vous pouvez utiliser pour filtrer vos requêtes selon une certaine période. Pour plus d’informations, consultez le guide sur les questions de l’assistant [AI](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la présentation de l’assistant [AI](../../ai-assistant/home.md).

## Catalog Service {#catalog-service}

Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, Catalog conserve les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

| Fonctionnalité | Description |
| --- | --- |
| Nouveau point d’entrée de l’API | Gérez plus efficacement vos métadonnées de jeu de données Adobe Experience Platform avec le nouveau point d’entrée [API Catalog Service /v2/dataSets/{DATASET_ID}](../../catalog/api/update-object.md#patch-v2-notation). Mettez facilement à jour des attributs de jeux de données complexes et profondément imbriqués, car le système crée automatiquement les niveaux de chemin manquants pour vous faire gagner du temps, réduire les étapes manuelles et minimiser les erreurs. |

{style="table-layout:auto"}

Pour plus d’informations sur le service de catalogue, consultez la [présentation du service de catalogue](../../catalog/home.md).

## Préparation des données {#data-prep}

Utilisez la préparation des données pour mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge améliorée de l’importation et de l’exportation de mappages | Vous pouvez désormais exporter les mappages vers un fichier CSV et les configurer localement sur une feuille de calcul. Vous pouvez ensuite importer vos mappages mis à jour dans Experience Platform à l’aide de l’interface de mappage de l’interface utilisateur. Vous pouvez utiliser cette fonctionnalité pour configurer un grand nombre de mappages sans avoir à les créer manuellement dans l’interface utilisateur. De plus, lors de la création d’un flux de données, vous pouvez charger une copie de vos mappages directement dans Experience Platform pour accélérer votre workflow. Pour plus d’informations, consultez le guide sur [l’importation et l’exportation de mappages](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Destinations (mise à jour le 20 février) {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Description |
| --- | --- |
| [ (Beta) Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Utilisez le connecteur [!DNL Marketo Engage Person Sync] pour diffuser des mises à jour d’audiences de personnes vers les enregistrements correspondants de votre instance [!DNL Marketo Engage]. Ce connecteur de destination est en version bêta et disponible uniquement pour certains clients et clientes. Pour demander l’accès, contactez votre représentant Adobe. |
| [Connexion CRM Trade Desk](/help/destinations/catalog/advertising/tradedesk-emails.md) disponibilité générale | [!DNL The Trade Desk CRM] connexion est désormais disponible pour tous. Utilisez [!DNL The Trade Desk] destination CRM pour activer des profils sur votre compte [!DNL Trade Desk] afin de permettre le ciblage et la suppression d’audiences en fonction des données CRM. |
| [Connexion aux profils des participants RainFocus](/help/destinations/catalog/marketing-automation/rainfocus.md) | Utilisez la destination [!DNL RainFocus Attendee Profiles] pour diffuser des profils clients de Adobe Experience Platform vers la plateforme [!DNL RainFocus] afin de créer et de mettre à jour des profils de participants. |
| [Connexion Criteo](/help/destinations/catalog/advertising/criteo.md) disponibilité générale | La connexion [!DNL Criteo] est désormais disponible pour tous. Criteo alimente une publicité fiable et percutante pour offrir des expériences plus riches à chaque consommateur sur l&#39;Internet ouvert. Grâce au plus grand ensemble de données commerciales au monde et à l’IA la plus performante de sa catégorie, Criteo veille à ce que chaque point de contact du parcours d’achats soit personnalisé afin d’atteindre les clients avec la bonne annonce, au bon moment. |
| [[!DNL Amazon Ads] Connexion](../../destinations/catalog/advertising/amazon-ads.md) | Le connecteur [!DNL Amazon Ads], auparavant en version bêta, est désormais disponible pour tous. Le connecteur a également été mis à jour pour envoyer un signal de consentement accordé à tous les profils qui ont consenti à ce que leurs données personnelles soient utilisées pour la publicité. En savoir plus sur la nouvelle commande [Signal de consentement Amazon Ads](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| --- | --- |
| Utilisez des libellés d’accès pour gérer l’accès des utilisateurs aux flux de données de destination | Dans le cadre de la fonctionnalité [[!UICONTROL contrôle d’accès basé sur les attributs]](/help/access-control/abac/overview.md) de Real-Time CDP, vous pouvez désormais appliquer des libellés d’accès aux [flux de données de destination](/help/dataflows/ui/monitor-destinations.md). Ainsi, vous pouvez vous assurer que seul un sous-ensemble d’utilisateurs de votre organisation a accès à des flux de données de destination spécifiques. <br> **Important** : lors de la recherche de flux de données de destination à l’aide de la zone de recherche située en haut de l’interface utilisateur d’Experience Platform, les résultats peuvent inclure des flux de données de destination que vos libellés d’accès utilisateur vous empêchent de voir. Ce comportement sera corrigé dans une prochaine mise à jour. |
| [Rapports au niveau de l’audience](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) pour la connexion à [Marketo Engage](/help/destinations/catalog/adobe/marketo-engage.md) | Vous pouvez désormais [afficher des informations](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) sur les identités activées, exclues ou en échec réparties au niveau de l’audience, pour chaque audience qui fait partie des flux de données pour cette destination. |
| Prise en charge des audiences externes pour les connexions [TikTok](/help/destinations/catalog/social/tiktok.md) et [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | Vous pouvez activer des audiences externes vers ces destinations à partir de [chargements personnalisés](../../segmentation/ui/audience-portal.md#import-audience) et [composition d’audiences fédérées](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences). |
| Exporter des tableaux, des mappages et des objets vers des destinations d’espace de stockage | En utilisant le nouveau bouton (bascule) **[!UICONTROL Exporter des tableaux, des mappages]** des objets lors de la connexion à une destination d’espace de stockage , vous pouvez exporter des objets complexes vers des destinations sélectionnées. [En savoir plus](/help/destinations/ui/export-arrays-calculated-fields.md) à propos de la fonctionnalité. |

{style="table-layout:auto"}

**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

- Un problème lié aux outils de test Destination SDK a été corrigé. Certains clients ou partenaires rencontraient des problèmes avec l’outil [exemple de génération de profil](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) en raison d’un format non pris en charge lorsque le schéma utilisé pour générer les profils incluait des types de données avec un sélecteur de `No format`.
- Un problème lors de la mise à jour de la spécification `targetConnection` des destinations à l’aide de l’API Flow Service a été corrigé. Dans certains cas, l’opération PATCH se comporte de la même manière qu’une opération POST, corrompant les flux de données existants. Ce problème est maintenant corrigé et tous les clients peuvent utiliser l’API Flow Service pour mettre à jour leur spécification `targetConnection`. [En savoir plus](/help/destinations/api/edit-destination.md#patch-target-connection).
- Lors de l’exportation de profils vers des destinations basées sur des fichiers, la déduplication garantit qu’un seul profil est exporté lorsque plusieurs profils partagent la même clé de déduplication et le même horodatage de référence. Cette version comprend une mise à jour du processus de déduplication, afin de s’assurer que les exécutions successives avec les mêmes coordonnées produiront toujours les mêmes résultats, ce qui améliore la cohérence. [En savoir plus](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp).

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).


## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des vues dans [!DNL Microsoft Dynamics] | Vous pouvez désormais ingérer des `"entityType": "view"` lors de l’utilisation de la source [!DNL Microsoft Dynamics]. Pour plus d’informations, consultez le guide sur la [connexion d’une source  [!DNL Microsoft Dynamics]  Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).

## Mises à jour de la documentation {#documentation-updates}

### Edge Network et comparaison des concentrateurs {#edge}

La comparaison entre [Edge Network et le hub](../../landing/edge-and-hub-comparison.md) fournit un aperçu détaillant les différences entre les deux types de serveurs pour Adobe Experience Platform (hub et Edge Network), y compris les services disponibles sur chaque type de serveur, les emplacements des serveurs, ainsi que les scénarios recommandés pour l’utilisation de chaque type de serveur.

### Référence de l’API Flow Service développée pour les sources {#flow-service}

La [[!DNL Flow Service] référence d’API](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) pour les sources a été mise à jour avec de nouveaux exemples de requête et de réponse d’API. Utilisez la référence d’API développée pour créer et mettre à jour les spécifications de connexion lors de l’intégration de votre propre source à Experience Platform. Vous pouvez également utiliser la référence d’API développée pour effectuer des transitions d’état sur vos entités sources, mettre à jour les connexions source et cible existantes et récupérer les flux et les spécifications de flux selon un critère de filtrage spécifique.

### Sauvegarde des configurations d’objet à l’aide de l’outil Sandbox {#back-up-object-configurations}

Lisez le [guide de configuration de la sauvegarde d’objet](../../sandboxes/use-cases/backup-object-configuration.md) pour obtenir des instructions détaillées sur la création d’un package de sauvegarde à l’aide de l’outil sandbox afin de vous assurer que les configurations d’objet sont stockées et sécurisées.

### Activer un centre d’excellence à l’aide de l’outil Sandbox {#center-of-excellence}

Lisez le [guide du centre d’excellence](../../sandboxes/use-cases/center-of-excellence.md) pour obtenir des instructions détaillées sur la création d’un package « sandbox doré » qui agit comme un centre d’excellence pour partager efficacement les configurations clés.

### Conservation du jeu de données d’événement d’expérience dans le lac de données {#experience-event-dataset-retention}

Prenez le contrôle de la conservation des jeux de données d’événements d’expérience dans Adobe Experience Platform à l’aide de la durée de vie (TTL). [Ce guide](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) vous guide tout au long de l’évaluation, de la configuration et de la gestion des paramètres de TTL pour supprimer automatiquement les enregistrements obsolètes, optimiser le stockage et conserver la pertinence de vos données. Découvrez les bonnes pratiques, les cas d’utilisation réels et les considérations clés pour améliorer la gestion du cycle de vie des données.
