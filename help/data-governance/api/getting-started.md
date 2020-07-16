---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de l’API DULE Policy Service
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 54%

---


# DULE [!DNL Policy Service] API developer guide

Data Usage Labeling and Enforcement (DULE) is the core mechanism of Adobe Experience Platform [!DNL Data Governance]. The DULE [!DNL Policy Service] provides a RESTful API that allows you to create and manage data usage policies to determine what marketing actions can be taken against data that has been labeled with certain data usage labels.

This document provides instructions for performing the key operations available in the [!DNL Policy Service] API. Si vous ne l’avez pas encore fait, commencez par examiner la [présentation de la gouvernance des données](../home.md) pour vous familiariser avec le cadre DULE. Pour obtenir des instructions étape par étape sur la création et l’application des stratégies DULE, consultez le [tutoriel sur la stratégie DULE](../policies/create.md).

This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Policy Service] API.

## Getting started with DULE [!DNL Policy Service]

Before beginning to work with the [!DNL Policy Service], data on [!DNL Experience Platform] must have appropriate DULE labels applied. Vous trouverez des instructions étape par étape complètes pour appliquer des libellés d’utilisation des données aux jeux de données et aux champs dans le [guide d’utilisation des libellés DULE](../labels/user-guide.md).

## Conditions préalables

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [!DNL Data Governance](../home.md): Cadre selon lequel [!DNL Experience Platform] applique la conformité à l’utilisation des données.
   * [Étiquettes](../labels/overview.md)DULE : Les libellés d’utilisation des données sont appliqués aux champs de données [!DNL Experience Data Model] (XDM), en spécifiant les restrictions d’accès à ces données.
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
* [!DNL Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

## Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Data Governance], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Ressources de base ou personnalisées

Within the [!DNL Policy Service] API, all policies and marketing actions are referred to as either `core` or `custom` resources.

Les ressources `core` sont définies et gérées par Adobe, alors que les ressources `custom` sont créées et gérées par des clients individuels. Elles sont donc uniques et visibles seulement par l’organisation IMS qui les a créées. Les opérations de liste et de recherche (`GET`) sont donc les seules opérations autorisées sur les ressources `core`, alors que les opérations de liste, de recherche et de mise à jour (`POST`, `PUT`, `PATCH` et `DELETE`) sont disponibles pour les ressources `custom`.

## État des stratégies

Les stratégies d’utilisation des données peuvent avoir l’un des trois états suivants : `DRAFT`, `ENABLED` ou `DISABLED`.

Par défaut, seules les stratégies « ENABLED » participent à l’évaluation des stratégies.

Les stratégies « DRAFT » peuvent aussi être prises en compte dans l’évaluation des stratégies, mais uniquement en définissant le paramètre de requête `?includeDraft=true`. Vous trouverez de plus amples renseignements sur l’évaluation des stratégies dans la section consacrée à l’[application des stratégies](../enforcement/overview.md) à la fin de ce document.

## Noms d’actions marketing {#marketing-actions}

Les noms d’actions marketing sont des identifiants uniques d’actions marketing. Chaque action marketing `core` a un nom unique s’appliquant à toutes les organisations IMS. Ces noms sont définis et gérés par Adobe. En attendant, toutes les actions marketing définies par le client (ressources `custom`) sont uniques au sein de votre organisation spécifique et ne sont ni visibles par d’autres organisations IMS ni partagées avec elles.

Steps for working with marketing actions in the [!DNL Policy Service] API are outlined in the [Marketing Actions](#marketing-actions) section later in this document.

## Étapes suivantes

Maintenant que vous disposez des informations d’identification et des connaissances préalables requises, vous pouvez continuer à lire les exemples d’appels API fournis dans ce guide de développement :

* [Actions marketing](marketing-actions.md)
* [Stratégies](policies.md)