---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: eceafa1852fc7c17660263d6ef7878a3e7bd0841
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 32%

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

**Date de publication : février 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Agent Orchestrator](#agent-orchestrator)
- [Alertes](#alerts)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service de requête](#query-service)
- [Sources](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator vous permet de créer et de déployer des agents optimisés par l’IA qui peuvent automatiser les workflows et interagir avec les clients sur plusieurs canaux.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Agent d’intégration des données | Utilisez l’agent d’intégration de données pour configurer les connexions source, valider la qualité des données, appliquer un enrichissement sémantique, vérifier et valider les schémas et exécuter l’ingestion des données. Suivez les workflows étape par étape pour les flux B2C et B2B, examinez les sorties attendues et résolvez les problèmes courants. |
| Agent de Distiller de données | Utilisez l’agent Data Distiller pour créer des tâches SQL en langage naturel, optimiser les performances SQL, récupérer après des erreurs SQL, planifier et gérer des tâches SQL et surveiller l’état des tâches. Consultez les mécanismes de sécurisation, les autorisations requises et les conseils de dépannage pour commencer. |
| Agent de collecte de données | Utilisez l’agent de collecte de données pour obtenir des conseils contextuels sur les configurations complexes de collecte de données et pour explorer la parenté, les dépendances et les relations entre vos objets de collecte de données au moyen d’informations conversationnelles. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [documentation d’Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte via l’onglet [!UICONTROL Alerts] de l’interface utilisateur d’Experience Platform et choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par e-mail de notification.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Intégration d’[!DNL Slack] pour les alertes destinées aux clients et clientes | Vous pouvez désormais envoyer des alertes destinées aux clients et clientes à [!DNL Slack]. Suivez le tutoriel détaillé pour configurer l’intégration [!DNL Slack] et recevoir des notifications d’alerte directement dans votre espace de travail [!DNL Slack]. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Observability Insights] vue d’ensemble](../observability/home.md).

## Collecte de données {#data-collection}

La collecte de données Adobe Experience Platform fournit un ensemble de technologies qui vous permettent de collecter des données d’expérience client côté client et de les envoyer à Adobe Experience Platform Edge Network et à d’autres destinations.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Gestion de l’extension Adobe Platform Tags | Utilisez la nouvelle fonctionnalité de gestion des extensions pour charger, compresser et publier les extensions de votre organisation pour le développement, la distribution privée et publique. Recherchez les extensions privées partagées avec vos propres extensions dans la vue d’entreprise de niveau supérieur. Cette fonctionnalité prend en charge les extensions web, Edge et mobiles. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [documentation sur la collecte de données](https://experienceleague.adobe.com/en/docs/experience-platform/collection/home).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| [!DNL Snowflake] lot généralement disponible | La destination [!DNL Snowflake] par lots a été déplacée vers la disponibilité générale. Vous pouvez désormais afficher la colonne ID de la politique de fusion dans vos données exportées avec les colonnes existantes telles que la date et l’heure, les attributs de mappage et l’appartenance à l’audience. |
| Prise en charge du chiffrement AES256 pour les destinations [Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) | Vous pouvez désormais configurer le chiffrement AES256 pour vos exportations Amazon S3. Choisissez parmi deux options : <ul><li>**[!UICONTROL Default]** : Experience Platform chiffre les données au repos avec l’algorithme de chiffrement par défaut défini sur votre compartiment.</li><li>**[!UICONTROL SSE-S3/AES256]** : Experience Platform ajoute l’en-tête `s3:x-amz-server-side-encryption": "AES256` à l’exportation et chiffre les données au repos avec l’algorithme AES256 lorsqu’elles arrivent dans S3. **Cette option est prioritaire sur tout algorithme de chiffrement par défaut que vous configurez sur votre compartiment S3**.</li></ul> |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences clientes par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Schéma Organisation et recherche d&#39;inventaire | La page de navigation des schémas comprend désormais une recherche et un filtrage améliorés, des actions intégrées et la prise en charge des balises et des dossiers définis par l’utilisateur. Ces mises à jour facilitent la recherche, l’organisation et la gestion des schémas sur les sandbox tout en réduisant la navigation manuelle et les efforts de maintenance. |
| Modification restreinte des schémas avec des jeux de données | Les opérations de modification qui entraînent des modifications avec rupture sont désormais limitées une fois qu’un jeu de données existe pour un schéma. Lorsqu’un jeu de données est associé, vous ne pouvez plus renommer ou supprimer des champs, modifier des types ou des formats de données de champ, modifier des descripteurs d’identité, gérer des champs associés pour supprimer des champs existants ou modifier la classe affectée. D’autres modifications et l’obsolescence des champs restent prises en charge. |

Pour plus d’informations, consultez la [[!DNL XDM] vue d’ensemble](../xdm/home.md).

## Service de requête {#query-service}

Le service de requête vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Alignement de la date de réinitialisation annuelle du calcul de Data Distiller (version limitée) | Les heures de calcul annuelles de Data Distiller sont désormais réinitialisées à la date anniversaire de votre contrat Data Distiller, en fonction de la date d’achat ou de renouvellement de la licence. Cela aligne le rapport Utilisation de la licence sur les termes de votre contrat et peut entraîner un ajustement ponctuel des valeurs d’utilisation actuelles. |
| Gestion des sessions Data Distiller (version limitée) | En tant qu’administrateur autorisé, vous pouvez afficher et gérer les sessions Query Service et Data Distiller actives au sein de votre organisation et de votre sandbox via l’interface utilisateur. Utilisez la gestion des sessions pour identifier les sessions inactives et les terminer afin de libérer de la capacité. Les sauvegardes intégrées vous empêchent de terminer des sessions avec des requêtes actives. Cette fonctionnalité consigne toutes les actions d’éviction à des fins d’audit et avertit les utilisateurs concernés. Vous avez besoin de l’autorisation **Gérer les sessions de requête** pour accéder à cette fonctionnalité. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de Query Service](../query-service/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| Prise en charge du catalogue Unity dans [!DNL Databricks] connecteur source | Le connecteur source [!DNL Databricks] prend désormais en charge le catalogue Unity. Lisez la documentation [[!DNL Databricks]](../sources/connectors/databases/databricks.md) mise à jour pour savoir comment utiliser le catalogue Unity lorsque vous configurez votre connexion source. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../sources/home.md).
