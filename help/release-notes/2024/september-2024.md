---
title: Notes de mise à jour d’Adobe Experience Platform - Septembre 2024
description: Les notes de mise à jour de septembre 2024 pour Adobe Experience Platform.
source-git-commit: 33d1305aef7c763e7b0bd8c6db6a1a9417cc2a9d
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 24%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 24 septembre 2024**

Mises à jour des fonctionnalités et de la documentation existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Tableaux de bord](#dashboards)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [Query Service](#query-service)
- [Segmentation Service](#segmentation-service)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités de Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface utilisateur de Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des environnements de développement | Vous pouvez désormais [vous abonner aux alertes](../../observability/alerts/ui.md) dans les environnements de test de production et de développement, ce qui permet une surveillance transparente dans tous les environnements. |
| Modèles d&#39;email | [Les alertes par e-mail](../../observability/alerts/ui.md) incluent désormais des informations détaillées sur les ressources, en vous assurant que vous disposez de tous les détails clés à portée de main. |
| Personnalisation améliorée | Vous pouvez désormais configurer des [seuils d’alerte](../../observability/alerts/ui.md#alert-threshold) pour une plus grande flexibilité afin d’adapter les alertes à vos besoins spécifiques pour les types d’alerte suivants :<br><ul><li>Retard de la tâche relative aux segments</li><li>Délai d’exportation de segments</li><li>Retard de l’exécution du flux de destinations</li><li>Retard d’exécution du flux du service d’identités</li><li>Retard d’exécution du flux de profils</li><li>Délai d’exécution du flux des sources</li><li>Retard d’exécution de requête</li><li>Taux de saut d’activation dépassé</li><li>Taux d’erreur d’ingestion des sources dépassé</ul> |
| Alertes étendues | Les alertes d’informations sur les événements d’audit sont désormais disponibles pour l’abonnement pour les [règles d’alerte](../../observability/alerts/rules.md) suivantes :<br><ul><li>Création d’audience</li><li>Mise à jour d’audience</li><li>Suppression d’audience</li><li>Création de jeux de données</li><li>Mise à jour du jeu de données</li><li>Suppression de jeux de données</li><li>Création de schéma</li><li>Mise à jour du schéma</li><li>Suppression d’un schéma. |

{style="table-layout:auto"}

Pour plus d’informations sur les alertes, consultez la [[!DNL Observability Insights] présentation](../../observability/home.md).

## Tableaux de bord {#dashboards}

Experience Platform fournit plusieurs tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre entreprise, telles qu’elles sont capturées lors d’instantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Tableau des modules complémentaires d’utilisation de licence | Obtenez une visibilité granulaire sur l’utilisation des licences et gérez vos ressources Platform avec des tables dédiées pour les produits principaux et les modules complémentaires. Effectuez le suivi et l’analyse des mesures clés de chaque produit principal avec des vues d’analyse au niveau de l’environnement de test. Les mesures de module complémentaire s’intègrent de manière transparente aux mesures de produits de base, offrant une vue d’ensemble complète de l’utilisation. Une meilleure visibilité vous permet d’optimiser la gestion des licences et d’aligner les ressources avec les besoins de l’entreprise. Pour plus d’informations, consultez le [[!UICONTROL guide de tableau de bord Utilisation de la licence] .](../../dashboards/guides/license-usage.md#overview-tab) |
| Mode Query Pro - Mises à niveau des filtres globaux | Amélioration de l’analyse avec le nouveau filtre de date de Query Pro Mode. Affinez les informations à l’aide de paramètres de date dynamiques dans vos requêtes SQL et filtrez les données selon des périodes spécifiques. Choisissez des périodes prédéfinies ou personnalisées dans une interface utilisateur intuitive, en conservant les tableaux de bord pertinents pour tous les utilisateurs. Simplifiez les workflows, maintenez la précision et prenez des décisions opportunes. Pour plus d’informations, consultez le [guide sur la création de filtres de date](../../dashboards/data-distiller/query-pro-mode/filters/global-filter.md) . |
| Modes Query Pro - Exploration publicitaires | Déverrouillez des informations plus précises avec la fonction d’exploration du mode Query Pro et naviguez facilement des graphiques de haut niveau aux tableaux de bord détaillés. Utilisez cette fonction pour passer facilement des résumés aux analyses approfondies et explorer les tendances, les comportements des clients et les indicateurs clés de performance. Les dépassements automatiques de filtre et les explorations à plusieurs niveaux maintiennent les données homogènes, assurant une exploration en douceur. Simplifiez les workflows, conservez le contexte et accélérez les décisions. Pour plus d’informations, lisez le [guide détaillé sur la création d’explorations publicitaires](../../dashboards/data-distiller/query-pro-mode/drill-through.md) . |
| Mode Query Pro - Attributs de tableau avancés | Utilisez les attributs de tableau avancés du mode Query Pro pour rationaliser la visualisation des données, améliorer l’efficacité des workflows et améliorer la clarté des données. Ajoutez un tri, un redimensionnement et une pagination automatiques à vos tableaux de bord directement depuis les tableaux de bord personnalisés. Triez les colonnes afin de prioriser les données clés, redimensionnez-les pour une lisibilité optimale et naviguez facilement les jeux de données volumineux sans modifier les requêtes SQL. Lisez le guide &quot;[Afficher plus](../../dashboards/data-distiller/query-pro-mode/view-more.md)&quot; pour savoir comment intégrer ces fonctionnalités et améliorer vos informations sur les données. |
| Volume total des données | La mesure &quot;Richesse moyenne du profil&quot; a été remplacée par la mesure &quot;Volume total des données&quot;. Le volume total de données fait référence à la quantité totale de données disponibles pouvant être utilisées avec Real-time Customer Profile pour les workflows d’engagement et de personnalisation. Vous trouverez plus d’informations sur cette modification dans le [guide Total Data Volume](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Préparation de données {#data-prep}

Utilisez la préparation de données pour mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} Nouvelles fonctions de préparation de données à utiliser dans les destinations | Vous pouvez désormais utiliser les fonctions de tableau suivantes pour les cas d’utilisation des destinations :<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Pour plus d’informations, consultez le [guide des fonctions de prép de données](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Pour plus d’informations sur la préparation des données, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Destinations {#destinations}

**Mise à jour : 30 septembre 2024**

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Description |
| --- | --- |
| [Publicités Amazon](/help/destinations/catalog/advertising/amazon-ads.md) | La version de septembre 2024 ajoute l’option de mappage pour exporter le paramètre `countryCode` vers Amazon Ads. Utilisez `countryCode` dans l’ [étape de mappage](/help/destinations/catalog/advertising/amazon-ads.md#map) pour améliorer les taux de correspondance d’identité avec Amazon. |
| [[!BADGE B2B]{type=Informative} Demandbase](/help/destinations/catalog/advertising/demandbase.md) | Utilisez cette destination pour activer les audiences de votre compte pour les cas d’utilisation de Account-Based Marketing (ABM). Annoncez les rôles et les personnalités appropriés dans vos comptes cibles via le Demand Side Platform B2B de DemandBase (DSP). Les comptes Target peuvent également être enrichis avec des données tierces Demandbase, pour d’autres cas d’utilisation en aval dans le marketing et les ventes. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| --- | --- |
| [Améliorations de l’export de jeux de données](/help/destinations/ui/export-datasets.md) | La version de septembre 2024 d’Experience Platform comprend plusieurs améliorations des fonctionnalités d’exportation des jeux de données, afin de mieux prendre en charge divers cas d’utilisation de la sortie de données. Ces fonctionnalités ont été améliorées : <ul><li>Nouvelles options de configuration du dossier de données, y compris l’option permettant d’ajouter et de supprimer des sous-dossiers.</li><li>Nouvelles options d’exportation, notamment l’exportation de fichiers complets (une seule fois) et la possibilité de spécifier des dates de fin</li><li>Remarque : Adobe introduit également une date de fin par défaut, le 1er mai 2025, pour tous les flux de données d’exportation de jeux de données créés avant la version de septembre. Pour l’un de ces flux de données, les clients devront mettre à jour manuellement la date de fin dans le flux de données avant la date de fin, sinon les exportations s’arrêteront à cette date.</li></ul> <br> ![Image de l’interface utilisateur de l’Experience Platform qui illustre l’option Modifier la planification et les dossiers de l’étape de planification.](../2024/assets/september/edit-schedule-folders.png " Option Modifier la planification et les dossiers dans l’étape de planification."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations apportées à l’éditeur de schémas | Prenez le contrôle de vos relations de schéma avec un workflow de relation mis à jour dans l’éditeur de schémas. Mettez facilement à jour ou supprimez les relations existantes directement depuis l’interface utilisateur de l’Experience Platform, ce qui rend la gestion des schémas plus fluide et plus intuitive. Ajustez les schémas de référence et renommez les relations en toute confiance, en assurant une intégrité transparente des données entre la segmentation et d’autres processus clés. Pour en savoir plus sur la gestion efficace de vos relations de schéma, consultez les guides sur la [définition des champs de relation dans l’interface utilisateur](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) et sur les [relations B2B](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Pour plus d’informations sur XDM, consultez la [présentation du système XDM](../../xdm/home.md).

## Service d’identités {#identity-service}

Utilisez le service d’identités d’Adobe Experience Platform pour créer une vue complète de votre clientèle et de ses comportements en reliant les identités entre les appareils et les systèmes, vous permettant ainsi de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité limitée des règles de liaison de graphiques d’identités | Les règles de liaison de graphiques d’identités sont une suite d’outils d’Identity Service que vous pouvez utiliser pour garantir une personnalisation précise pour vos utilisateurs. <ul><li>Vous pouvez désormais utiliser l’[ algorithme d’optimisation des identités](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) pour vous assurer qu’un graphique d’identités est représentatif d’une seule personne et, par conséquent, empêcher la fusion indésirable d’identités sur Real-time Customer Profile.</li><li>Configurez les [priorités d’espace de noms](../../identity-service/identity-graph-linking-rules/namespace-priority.md) pour définir l’importance de vos espaces de noms respectifs et influencer la manière dont vos profils sont formés et segmentés.</li><li>Utilisez l’outil de simulation [graphique dans l’interface utilisateur](../../identity-service/identity-graph-linking-rules/graph-simulation.md) pour simuler des graphiques d’identités avec des configurations variées.</li><li>Utilisez l’ [ interface des paramètres d’identité](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) pour désigner votre espace de noms unique et établir des priorités pour tous les espaces de noms de votre organisation.</li><li>Reportez-vous au [tableau de bord d’identité](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) pour connaître les mesures et les tendances concernant vos données graphiques.</li></ul> Pour tester les règles de liaison de graphiques d’identités, contactez votre équipe de compte d’Adobe pour accéder aux environnements de test de développement. |

**Documentation mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Guide de dépannage des règles de liaison de graphiques d’identités | Lisez le nouveau [guide de dépannage des règles de liaison de graphiques d’identités](../../identity-service/identity-graph-linking-rules/troubleshooting.md) pour connaître les approches et les solutions de débogage que vous pouvez entreprendre afin de résoudre les problèmes courants que vous pouvez rencontrer lors de l’utilisation de règles de liaison de graphiques d’identités. |
| FAQ sur les règles de liaison de graphiques d’identités | Lisez la nouvelle [FAQ sur les règles de liaison de graphiques d’identités](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) pour obtenir une liste des réponses aux questions fréquentes sur la priorité des espaces de noms, l’algorithme d’optimisation des identités et d’autres facettes des règles de liaison de graphiques d’identités. |

{style="table-layout:auto"}

Pour plus d’informations sur le service d’identités, consultez la [vue d’ensemble du service d’identités](../../identity-service/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL data lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou à ingérer en tant que profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Audiences Distiller de données | Créez, gérez et activez facilement des audiences avec l’extension d’audience SQL dans Experience Platform Data Distiller. Définissez des segments d’audience avec des commandes SQL directement depuis votre lac de données, en contournant la nécessité de données brutes dans les profils. Affinez les stratégies de ciblage et synchronisez automatiquement les audiences avec les destinations basées sur les fichiers avec cette approche flexible et axée sur les données. Rationalisez les workflows, optimisez la gestion de l’audience et déverrouillez tout le potentiel des données. Lisez le [guide sur l’utilisation de l’extension d’audience SQL](../../query-service/data-distiller-audiences/overview.md) pour améliorer vos stratégies d’audience. |
| Statistiques Data Distiller - Hypercubes | Optimisez l&#39;analyse des données volumineuses avec les hypercubes. Gérez des calculs complexes, tels que des décomptes distincts et des analyses multidimensionnelles, sans retraiter les données historiques. Mettez à jour les données de manière incrémentielle, rationalisez les workflows et réduisez le temps de traitement tout en assurant précision et efficacité. Obtenez des informations plus rapides, évolutives et économiques qui transforment la prise de décision. Explorez le [guide sur l’utilisation d’hypercubes](../../query-service/hypercubes/overview.md) pour déverrouiller l’analyse avancée. |
| Explorateur d’objets de Query Editor | Améliorez l’efficacité des requêtes grâce au nouvel explorateur d’objets de l’éditeur de requêtes. Recherchez, filtrez et accédez rapidement aux jeux de données pour écrire et affiner plus rapidement les requêtes. Grâce aux mises à jour de schémas en temps réel et aux métadonnées instantanées de la table, vous pouvez rationaliser les workflows, réduire le temps de navigation et améliorer votre expérience de requête. Déverrouillez le potentiel de vos données et optimisez l’analyse. Pour plus d’informations, consultez le [guide sur l’utilisation de l’explorateur d’objets](../../query-service/ui/user-guide.md#object-browser) . |
| Heures de calcul | Contrôlez l’utilisation des ressources avec la mesure Heures de calcul nouvellement visible pour les requêtes planifiées. Affichez les heures de calcul au niveau de l’exécution des requêtes afin de surveiller et d’optimiser l’utilisation des ressources pour les requêtes par lots CTAS/ITAS. Suivez les heures de début, l’état d’achèvement et l’heure de calcul pour chaque exécution de requête. Ajustez les performances et réduisez les coûts sans effort. Lisez le [guide sur les heures de calcul](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) pour plus d’informations sur la manière d’optimiser l’efficacité de vos requêtes. |

{style="table-layout:auto"}

Pour en savoir plus sur Query Service, consultez la [présentation de Query Service](../../query-service/home.md).

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à jour des critères de segmentation par flux | À compter de la version de septembre 2024, les critères permettant aux audiences d’être éligibles pour la segmentation par flux ont été mis à jour. Vous trouverez plus d’informations sur ces modifications dans la [mise à jour des critères d’éligibilité de la segmentation par flux](../../segmentation/eligibility-criteria-update.md). |
| Implémentation de la recherche unifiée | Le comportement de recherche dans le créateur de segments utilise désormais la recherche unifiée. Cela permet une expérience plus robuste lors de la gestion et de la recherche d’audiences à réutiliser pour l’adhésion au segment. Pour plus d’informations sur cette modification, consultez le [guide du créateur de segments](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} Prise en charge de l’ingestion de données chiffrées dans l’interface utilisateur | Vous pouvez désormais ingérer des données chiffrées à partir d’une source par lots de stockage dans le cloud à l’aide de l’espace de travail sources dans l’interface utilisateur de l’Experience Platform. Pour plus d’informations, lisez le tutoriel sur l’ [ingestion de données chiffrées dans l’interface utilisateur](../../sources/tutorials/ui/encryped-ingestion.md) . |
| Disponibilité générale de la source [!DNL Snowflake Streaming] | La source [!DNL Snowflake Streaming] est désormais en disponibilité générale. Utilisez cette source pour diffuser des données de votre compte [!DNL Snowflake] vers Experience Platform. Pour plus d’informations, consultez la [[!DNL Snowflake Streaming] présentation](../../sources/connectors/databases/snowflake-streaming.md) . |
| Prise en charge de l’authentification du compte de service dans [!DNL Google BigQuery] | Vous pouvez désormais connecter votre compte [!DNL Google BigQuery] à l’Experience Platform à l’aide de l’authentification du compte de service. Pour plus d’informations, consultez la [[!DNL Google BigQuery] présentation](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) . <br> ![Image de l’interface utilisateur de l’Experience Platform qui illustre l’option Modifier la planification et les dossiers de l’étape de planification.](../2024/assets/september/service_auth.png "Authentification de service pour Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Prise en charge de l’absence d’aperçu des données d’exemple | Vous pouvez maintenant choisir d’ignorer l’aperçu des données lors de la création d’une connexion source avec les sources suivantes : <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Vous pouvez ignorer l’aperçu des données pour contourner un délai d’expiration qui peut se produire lors de l’ingestion de données par lots volumineux. Cela peut empêcher la validation automatique de vos champs calculés et obligatoires. Si vous choisissez d’ignorer l’aperçu des données, vous devrez peut-être valider manuellement vos champs calculés et obligatoires lors du mappage. |
| Prise en charge de la désactivation du découpage dans [!DNL SFTP] | Vous pouvez maintenant configurer un paramètre qui vous permet de désactiver le découpage dans la source [!DNL SFTP]. Consultez la [[!DNL SFTP] vue d’ensemble](../../sources/connectors/cloud-storage/sftp.md) pour plus d’informations. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).
