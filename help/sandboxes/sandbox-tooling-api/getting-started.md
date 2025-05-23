---
title: Prise en main de l’API d’outils Sandbox
description: Utilisez l’API Sandbox tooling pour examiner les artefacts et exporter et importer un instantané des configurations de sandbox entre les sandbox. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 0b34d153-a603-4397-a375-9cc846efe23a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 63%

---

# Prise en main de l’API d’outils Sandbox {#getting-started}

Ce guide de développement décrit les étapes à suivre pour utiliser l’API d’outils Sandbox afin de gérer les packages et les outils dans Adobe Experience Platform. Il comprend des exemples d’appels API pour effectuer diverses opérations.

## Lecture d’exemples d’appels API {#api-calls}

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. Des exemples de données JSON renvoyées à la réponse de l’API sont également fournis. Pour plus d’informations sur les conventions utilisées pour les exemples d’appels API dans la documentation, consultez la section sur la [lecture d’exemples d’appels API](/help/landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## Collecte des valeurs des en-têtes requis {#headers}

Ce guide nécessite que vous ayez suivi le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour passer avec succès des appels aux API Experience Platform. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Outre les en-têtes d’authentification, toutes les requêtes nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes contenant un payload (POST, PUT et PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Étapes suivantes {#next-steps}

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points d’entrée et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le format général de l’API, un exemple de requête montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de réponse pour un appel réussi.

Consultez les tutoriels d’API suivants pour commencer à effectuer des appels à l’API d’outils Sandbox :

* [Point d’entrée des packages](./packages.md)
* [Point d’entrée des outils](./tools.md)
