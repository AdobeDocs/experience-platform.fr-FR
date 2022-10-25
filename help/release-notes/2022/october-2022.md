---
title: Notes de mise à jour de Adobe Experience Platform - Octobre 2022
description: Notes de mise à jour d’octobre 2022 pour Adobe Experience Platform.
source-git-commit: 0ea2718247792e997b7a90ab9027946e800c8157
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 52%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 octobre 2022**

- [Clés gérées par le client](#cmk)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Query Service](#query-service)
- [Sources](#sources)

## Clés gérées par le client {#cmk}

Toutes les données stockées sur Adobe Experience Platform sont chiffrées au repos à l’aide de clés au niveau du système. Si vous utilisez une application reposant sur Platform, vous pouvez désormais choisir d’utiliser vos propres clés de chiffrement, ce qui vous permet de mieux contrôler votre sécurité des données.

Consultez la présentation sur [Clés gérées par le client](../../landing/governance-privacy-security/customer-managed-keys.md) pour plus d’informations sur la fonctionnalité.

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Gestion des données sensibles pour les flux de données | Les flux de données exploitent désormais plusieurs technologies Platform pour gérer de manière appropriée les données sensibles telles qu’elles sont mises en oeuvre par des réglementations telles que la Loi sur la transférabilité et la responsabilité de l’assurance-maladie (HIPAA). Voir la section sur [gestion des données sensibles dans les flux de données](../../edge/datastreams/overview.md#sensitive) pour plus d’informations. |
| [!DNL Splunk] extension pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Splunk] à l’aide d’une [transfert d’événement](../../tags/ui/event-forwarding/overview.md) extension . Voir [[!DNL Splunk] présentation de l’extension](../../tags/extensions/web/splunk/overview.md) pour plus d’informations. |
| [!DNL Zendesk] extension pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Zendesk] à l’aide d’une [transfert d’événement](../../tags/ui/event-forwarding/overview.md) extension . Voir [[!DNL Zendesk] présentation de l’extension](../../tags/extensions/web/zendesk/overview.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Type de données | [[!UICONTROL Informations détaillées sur la session]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Mise à jour de la `authorized` d’un type booléen à une chaîne. `season` et `episode` ont été changées d’entiers en chaînes. |
| Type de données | [[!UICONTROL Informations détaillées sur la publicité]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` a été renommé en `friendlyName`, et `ID` a été renommé en `name`. |
| Type de données | [[!UICONTROL Informations détaillés sur les erreurs]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` a été renommé `name`. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans Data Science Workspace ou pour l’ingestion dans Profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Modèle de données d’insights de reporting accéléré de requête | Dans le cadre du SKU de Data Distiller, le magasin accéléré de requêtes vous permet de réduire le temps et la puissance de traitement requis pour obtenir des informations essentielles sur vos données. Avec le magasin accéléré de requêtes, vous pouvez créer un modèle de données personnalisé et/ou étendre sur les modèles de données Adobe Real-time Customer Data Platform existants pour améliorer vos informations de création de rapports et leurs visualisations. Voir [document d’informations sur les rapports de magasin accélérés de requête](https://experienceleague.adobe.com/docs/experience-platform/query/query-accelerated-store/reporting-insights-data-model.html) pour en savoir plus sur cette fonctionnalité. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur Query Service, consultez la section [présentation de Query Service](../../query-service/home.md).
Nouvelles fonctionnalités d’Adobe Experience Platform :

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- | 
| Disponibilité bêta de la source Adobe Workfront | Utilisez la variable [Source Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) pour importer vos données Workfront dans Experience Platform et réaliser des cas d’utilisation, par exemple combiner vos enregistrements de travail avec des données tierces, appliquer des analyses d’historique et de série temporelle aux enregistrements de travail et interroger les données de travail à l’aide de SQL standard. Pour plus d’informations, consultez le guide sur [création d’une connexion source Workfront dans l’interface utilisateur](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Disponibilité bêta de la source Oracle Service Cloud | Utilisez la source Oracle Service Cloud pour ingérer des données de votre compte Oracle Service Cloud vers Experience Platform. Pour plus d’informations, consultez la documentation relative à la [Source Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
