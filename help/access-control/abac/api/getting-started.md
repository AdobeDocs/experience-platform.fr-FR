---
keywords: Experience Platform;accueil;rubriques les plus consultées;Contrôle d’accès basé sur les attributs;contrôle d’accès basé sur les attributs
title: Prise en main de l’API de contrôle d’accès basé sur les attributs
description: L’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les rôles et les politiques d’accès dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 63%

---

# Prise en main de l’API de contrôle d’accès basé sur les attributs

Ce guide de développement décrit les étapes à suivre pour utiliser l’API de contrôle d’accès basé sur les attributs afin de gérer les rôles, les produits, les catégories d’autorisations et les jeux d’autorisations dans Adobe Experience Platform. Il comprend des exemples d’appels API pour effectuer diverses opérations.

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées pour les exemples d’appels API dans la documentation, consultez la section sur la [lecture d’exemples d’appels API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## Collecte des valeurs des en-têtes requis

Ce guide nécessite que vous ayez suivi le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour passer avec succès des appels aux API Experience Platform. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Outre les en-têtes d’authentification, toutes les requêtes nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes contenant un payload (POST, PUT et PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Étapes suivantes

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points d’entrée et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le format général de l’API, un exemple de requête montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de réponse pour un appel réussi.

Consultez les tutoriels d’API suivants pour commencer à lancer des appels à l’API de contrôle d’accès basé sur les attributs :

* [Point d’entrée des rôles](./roles.md)
* [Point d’entrée de produits](./products.md)
