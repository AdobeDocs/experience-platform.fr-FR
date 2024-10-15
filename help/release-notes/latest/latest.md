---
title: Notes de mise à jour d’Adobe Experience Platform - Septembre 2024
description: Les notes de mise à jour de septembre 2024 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: eac613434f631cab567ab3fa6e30d33acac79d2f
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 100%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 24 septembre 2024**

Mises à jour des fonctionnalités et de la documentation existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Tableaux de bord](#dashboards)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [Query Service](#query-service)
- [Segmentation Service](#segmentation-service)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités de Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface utilisateur de Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des sandbox de développement | Vous pouvez maintenant [vous abonner aux alertes](../../observability/alerts/ui.md) dans les sandbox de production et de développement, ce qui permet une surveillance transparente de tous les environnements. |
| Modèles d’e-mail | Les [alertes par e-mail](../../observability/alerts/ui.md) incluent désormais des informations détaillées sur les ressources, vous permettant ainsi de disposer de toutes les informations clés à portée de main. |
| Amélioration de la personnalisation | Vous pouvez désormais configurer des [seuils d’alerte](../../observability/alerts/ui.md#alert-threshold) pour une plus grande flexibilité afin d’adapter les alertes à vos besoins spécifiques pour les types d’alertes suivants :<br><ul><li>Retard de la tâche relative aux segments</li><li>Retard d’export du segment</li><li>Retard d’exécution du flux de destination</li><li>Retard d’exécution du flux du service d’identités</li><li>Retard d’exécution du flux de profils</li><li>Retard dans l’exécution du flux de sources</li><li>Retard d’exécution de requête</li><li>Taux d’activations ignorées dépassé</li><li>Taux d’erreurs d’ingestion de sources dépassé</ul> |
| Alertes étendues | Les alertes d’informations sur les événements d’audit sont désormais disponibles pour un abonnement pour les [règles d’alerte](../../observability/alerts/rules.md) suivantes :<br><ul><li>Création d’une audience</li><li>Mise à jour d’une audience</li><li>Suppression d’une audience</li><li>Création d’un jeu de données</li><li>Mise à jour d’un jeu de données</li><li>Suppression d’un jeu de données</li><li>Création d’un schéma</li><li>Mise à jour d’un schéma</li><li>Suppression d’un schéma. |

{style="table-layout:auto"}

Pour plus d’informations sur les alertes, consultez la [[!DNL Observability Insights] vue d’ensemble](../../observability/home.md).

## Tableaux de bord {#dashboards}

Experience Platform propose de nombreux tableaux de bord qui vous permettent d’afficher des informations importantes sur les données de votre organisation, telles quʼelles ont été capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Tableau des modules complémentaires d’utilisation des licences | Obtenez une visibilité granulaire sur l’utilisation des licences et gérez vos ressources Platform avec des tableaux dédiés pour les produits principaux et les modules complémentaires. Effectuez le suivi et l’analyse des mesures clés de chaque produit principal avec des vues d’analyse au niveau du sandbox. Les mesures de module complémentaire s’intègrent parfaitement aux mesures de produits principaux, offrant une vue complète de l’utilisation. Une meilleure visibilité vous permet d’optimiser la gestion des licences et d’aligner les ressources sur les besoins de l’entreprise. Pour plus d’informations, voir le [[!UICONTROL guide du tableau de bord Utilisation des licences].](../../dashboards/guides/license-usage.md#overview-tab) |
| Mode de requête pro - Mises à niveau des filtres globaux | Améliorez les analyses avec le nouveau filtre de date du mode de requête pro. Affinez les informations à l’aide de paramètres de date dynamiques dans vos requêtes SQL et filtrez les données par périodes spécifiques. Choisissez des périodes prédéfinies ou personnalisées dans une interface d’utilisation intuitive, en conservant les tableaux de bord pertinents pour tous les utilisateurs et toutes les utilisatrices. Simplifiez les workflows, conservez la précision et prenez des décisions opportunes. Pour plus d’informations, consultez le [guide sur la création de filtres de date](../../dashboards/sql-insights-query-pro-mode/filters/global-filter.md). |
| Mode de requête pro - Explorations | Obtenez des informations plus précises avec la fonctionnalité d’exploration du mode de requête pro et naviguez facilement entre les graphiques généraux et les tableaux de bord détaillés. Utilisez cette fonctionnalité pour passer facilement des résumés aux analyses approfondies et explorer les tendances, les comportements de la clientèle et les KPI. Les passages de filtres automatiques et les explorations à plusieurs niveaux garantissent des données homogènes, assurant une exploration fluide. Simplifiez les workflows, conservez le contexte et accélérez les décisions. Pour plus d’informations, lisez le [guide détaillé sur la création d’explorations](../../dashboards/sql-insights-query-pro-mode/drill-through.md). |
| Mode de requête pro - Attributs de table avancés | Utilisez les attributs de table avancés du mode de requête pro pour rationaliser la visualisation des données, améliorer l’efficacité des workflows et améliorer la clarté des données. Ajoutez un tri, un redimensionnement et une pagination automatiques à vos tableaux de bord directement depuis les tableaux de bord personnalisés. Triez les colonnes afin de hiérarchiser les données clés, redimensionnez-les pour une lisibilité optimale et parcourez facilement les jeux de données volumineux sans modifier les requêtes SQL. Pour découvrir comment intégrer ces fonctionnalités et améliorer vos informations sur les données, lisez le guide « [Afficher plus](../../dashboards/sql-insights-query-pro-mode/view-more.md) ». |
| Volume total des données | La mesure « Richesse du profil moyenne » par la mesure « Volume total des données ». Le volume total des données fait référence à la quantité totale de données disponibles pouvant être utilisées avec Profil client en temps réel pour les workflows d’engagement et de personnalisation. Vous trouverez plus d’informations sur cette modification dans le [guide Volume total des données](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Préparation des données {#data-prep}

Utilisez la préparation des données pour mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Version Beta]{type=Informative} Nouvelles fonctions de préparation des données à utiliser dans les destinations | Vous pouvez désormais utiliser les fonctions de table suivantes pour les cas d’utilisation des destinations :<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Pour plus d’informations, consultez le [guide des fonctions de préparation de données](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Pour plus d’informations sur la préparation des données, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Destinations {#destinations}

**Mise à jour : 30 septembre 2024**

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Description |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | La version de septembre 2024 comporte une option de mappage permettant d’exporter le paramètre `countryCode` vers Amazon Ads. Utilisez `countryCode` dans l’[étape de mappage](/help/destinations/catalog/advertising/amazon-ads.md#map) pour améliorer vos taux de correspondance d’identité avec Amazon. |
| [[!BADGE B2B]{type=Informative} Demandbase](/help/destinations/catalog/advertising/demandbase.md) | Utilisez cette destination pour activer les audiences de votre compte pour les cas d’utilisation d’Account-Based Marketing (ABM). Faites de la publicité auprès des personas et des rôles pertinents dans vos comptes cibles via Demand Side Platform (DSP) B2B de DemandBase. Les comptes cibles peuvent également être enrichis avec des données tierces DemandBase pour d’autres cas d’utilisation en aval dans le marketing et les ventes. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de l’[export de jeux de données](/help/destinations/ui/export-datasets.md) | La version de septembre 2024 d’Experience Platform comprend plusieurs améliorations des fonctionnalités d’export de jeux de données, afin de mieux prendre en charge divers cas d’utilisation de la sortie de données. Les améliorations de ces fonctionnalités sont les suivantes : <ul><li>Nouvelles options de configuration des dossiers de données, y compris la possibilité d’ajouter et de supprimer des sous-dossiers.</li><li>Nouvelles options d’export, notamment l’export de fichiers complets (une seule fois) et la possibilité de spécifier des dates de fin.</li><li>Remarque : Adobe introduit également une date de fin par défaut, le 1er mai 2025, pour tous les flux de données d’export de jeux de données créés avant la version de septembre. Pour ces flux de données, les clientes et clients devront mettre à jour manuellement la date de fin dans le flux de données avant la date de fin, sinon les exports s’arrêteront à cette date.</li></ul> <br> ![Image de l’interface d’utilisation d’Experience Platform qui illustre l’option Modifier le planning et les dossiers de l’étape de planification.](../2024/assets/september/edit-schedule-folders.png "Option Modifier le planning et les dossiers de l’étape de planification."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations apportées à l’éditeur de schémas | Contrôlez les relations de votre schéma avec un workflow de relation mis à jour dans l’éditeur de schémas. Mettez facilement à jour ou supprimez des relations existantes directement depuis l’interface d’utilisation d’Experience Platform, pour une gestion des schémas plus fluide et plus intuitive. Ajustez les schémas de référence et renommez les relations en toute confiance, ce qui garantit intégrité transparente des données entre les processus de segmentation et autres processus clés. Pour en savoir plus sur la gestion efficace des relations de votre schéma, voir les guides sur la [définition des champs de relation dans l’interface d’utilisation](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) et sur les [relations B2B](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Pour plus d’informations sur XDM, consultez la [vue d’ensemble du système XDM](../../xdm/home.md).

## Service d’identités {#identity-service}

Utilisez le service d’identités d’Adobe Experience Platform pour créer une vue complète de votre clientèle et de ses comportements en reliant les identités entre les appareils et les systèmes, vous permettant ainsi de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité limitée des règles de liaison de graphiques d’identité | Les règles de liaison de graphiques d’identité sont une suite d’outils du service d’identités que vous pouvez utiliser pour garantir une personnalisation précise pour vos utilisateurs et utilisatrices. <ul><li>Vous pouvez désormais utiliser l’[algorithme d’optimisation des identités](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) pour vous assurer qu’un graphique d’identité est représentatif d’une seule personne et, par conséquent, empêcher la fusion indésirable d’identités sur Profil client en temps réel.</li><li>Configurez les [priorités d’espace de noms](../../identity-service/identity-graph-linking-rules/namespace-priority.md) pour définir l’importance de vos espaces de noms respectifs et influencer la manière dont vos profils sont formés et segmentés.</li><li>Utilisez l’[outil de simulation graphique dans l’interface d’utilisation](../../identity-service/identity-graph-linking-rules/graph-simulation.md) pour simuler des graphiques d’identité avec des configurations variées.</li><li>Utilisez l’[interface des paramètres d’identité](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) pour désigner votre espace de noms unique et établir des priorités pour tous les espaces de noms de votre organisation.</li><li>Reportez-vous au [tableau de bord d’identité](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) pour connaître les mesures et les tendances concernant vos données graphiques.</li></ul> Pour tester les règles de liaison de graphiques d’identité, contactez votre équipe Adobe en charge des comptes pour accéder aux sandbox de développement. |

**Documentation mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Guide de dépannage des règles de liaison de graphiques d’identité | Lisez le nouveau [guide de dépannage des règles de liaison de graphiques d’identité](../../identity-service/identity-graph-linking-rules/troubleshooting.md) pour découvrir les approches et les solutions de débogage à adopter pour résoudre les problèmes courants que vous pouvez rencontrer lors de l’utilisation des règles de liaison de graphiques d’identité. |
| Questions fréquentes sur les règles de liaison de graphiques d’identité | Lisez les nouvelles [Questions fréquentes sur les règles de liaison de graphiques d’identité](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) pour obtenir une liste des réponses aux questions fréquentes sur la priorité des espaces de noms, l’algorithme d’optimisation des identités et d’autres facettes des règles de liaison de graphiques d’identité. |

{style="table-layout:auto"}

Pour plus d’informations sur le service d’identités, consultez la [vue d’ensemble du service d’identités](../../identity-service/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL data lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou à ingérer en tant que profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Audiences de Data Distiller | Créez, gérez et activez facilement des audiences avec l’extension d’audience SQL dans Experience Platform Data Distiller. Définissez des segments d’audience avec des commandes SQL directement depuis votre lac de données, en éliminant la nécessité de données brutes dans les profils. Affinez les stratégies de ciblage et synchronisez automatiquement les audiences avec les destinations basées sur les fichiers avec cette approche flexible et axée sur les données. Rationalisez les workflows, optimisez la gestion de l’audience et exploitez tout le potentiel des données. Lisez le [guide sur l’utilisation de l’extension d’audience SQL](../../query-service/data-distiller-audiences/overview.md) pour améliorer vos stratégies d’audience. |
| Statistiques de Data Distiller - Hypercubes | Optimisez l’analyse du Big Data avec des hypercubes. Gérez des calculs complexes, tels que des décomptes distincts et des analyses multidimensionnelles, sans retraiter les données historiques. Mettez à jour les données de manière incrémentielle, rationalisez les workflows et réduisez le temps de traitement tout en garantissant la précision et l’efficacité. Obtenez plus rapidement des informations évolutives et économiques qui transforment la prise de décision. Explorez le [guide sur l’utilisation d’hypercubes](../../query-service/hypercubes/overview.md) pour pouvoir tirer profit de l’analyse avancée. |
| Explorateur d’objets du requêteur | Améliorez l’efficacité des requêtes grâce au nouvel explorateur d’objets du requêteur. Recherchez, filtrez et accédez rapidement aux jeux de données pour écrire et affiner plus rapidement les requêtes. Grâce aux mises à jour de schémas en temps réel et aux métadonnées de table instantanées, vous pouvez rationaliser les workflows, réduire le temps de navigation et améliorer votre expérience de requête. Exploitez le potentiel de vos données et optimisez l’analyse. Pour plus d’informations, consultez le [guide sur l’utilisation de l’explorateur d’objets](../../query-service/ui/user-guide.md#object-browser). |
| Heures de calcul | Contrôlez l’utilisation des ressources avec la nouvelle mesure des heures de calcul visible pour les requêtes planifiées. Affichez les heures de calcul au niveau de l’exécution de la requête afin de surveiller et d’optimiser l’utilisation des ressources pour les requêtes par lots CTAS/ITAS. Suivez les heures de début, l’état d’achèvement et la durée de calcul pour chaque exécution de requête. Ajustez les performances et réduisez les coûts sans effort. Pour plus d’informations sur l’optimisation de l’efficacité de vos requêtes, lisez le [guide sur les heures de calcul](../../query-service/ui/query-schedules.md#compute-hours-at-job-level). |

{style="table-layout:auto"}

Pour en savoir plus sur Query Service, consultez la [vue d’ensemble de Query Service](../../query-service/home.md).

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à jour des critères de segmentation en streaming | À compter de la version de septembre 2024, les critères permettant aux audiences d’être éligibles pour la segmentation en streaming ont été mis à jour. Vous trouverez plus d’informations sur ces modifications dans la [mise à jour des critères d’éligibilité à la segmentation en streaming](../../segmentation/eligibility-criteria-update.md). |
| Implémentation de la recherche unifiée | Le comportement de recherche dans le créateur de segments utilise désormais la recherche unifiée. Cela permet d’obtenir une expérience plus robuste lors de la gestion et de la recherche d’audiences à réutiliser pour l’appartenance à un segment. Pour plus d’informations sur cette modification, consultez le [guide du créateur de segments](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [vue d’ensemble de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Version Beta]{type=Informative} Prise en charge de l’ingestion de données chiffrées dans l’interface d’utilisation | Vous pouvez désormais ingérer des données chiffrées à partir d’une source par lots d’espace de stockage dans le cloud à l’aide de l’espace de travail Sources dans l’interface d’utilisation d’Experience Platform. Pour plus d’informations, consultez le tutoriel sur l’[ingestion de données chiffrées dans l’interface d’utilisation](../../sources/tutorials/ui/encryped-ingestion.md). |
| Disponibilité générale de la source [!DNL Snowflake Streaming] | La source [!DNL Snowflake Streaming] est désormais en disponibilité générale. Utilisez cette source pour diffuser des données de votre compte [!DNL Snowflake] vers Experience Platform. Pour plus d’informations, consultez la [[!DNL Snowflake Streaming] vue d’ensemble](../../sources/connectors/databases/snowflake-streaming.md). |
| Prise en charge de l’authentification du compte de service dans [!DNL Google BigQuery] | Vous pouvez désormais connecter votre compte [!DNL Google BigQuery] à Experience Platform à l’aide de l’authentification du compte de service. Pour plus d’informations, consultez la [[!DNL Google BigQuery] vue d’ensemble. ](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)<br> ![Image de l’interface d’utilisation d’Experience Platform qui illustre l’option Modifier le planning et les dossiers de l’étape de planification.](../2024/assets/september/service_auth.png "Authentification de service pour Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Prise en charge de la possibilité d’ignorer la prévisualisation des données d’exemple | Vous pouvez maintenant choisir d’ignorer la prévisualisation des données lors de la création d’une connexion source avec les sources suivantes : <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Vous pouvez ignorer la prévisualisation des données pour contourner un délai d’expiration qui peut se produire lors de l’ingestion de données par lots volumineuses. Cela peut empêcher la validation automatique de vos champs calculés et obligatoires. Si vous choisissez d’ignorer la prévisualisation des données, vous devrez peut-être valider manuellement vos champs calculés et obligatoires lors du mappage. |
| Prise en charge de la désactivation du regroupement dans [!DNL SFTP] | Vous pouvez désormais configurer un paramètre qui permet de désactiver le regroupement dans la source [!DNL SFTP]. Pour plus d’informations, consultez la [[!DNL SFTP] vue d’ensemble](../../sources/connectors/cloud-storage/sftp.md). |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).
