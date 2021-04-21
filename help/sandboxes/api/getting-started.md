---
keywords: Experience Platform ; accueil ; rubriques populaires ; guide du développeur sandbox
solution: Experience Platform
title: Guide de l’API Sandbox
topic-legacy: developer guide
description: L’API Sandbox permet aux développeurs de gérer par programmation les sandbox à Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 88%

---

# Guide de l’API Sandbox

Les environnements de test d’Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des opérations et de créer des configurations personnalisées sans affecter votre environnement de production.

Ce guide de développement décrit les étapes à suivre pour utiliser l’API Sandbox afin de gérer les environnements de test dans Experience Platform. Il inclut des exemples d’appels API pour effectuer diverses opérations.

## Prise en main de l’API Sandbox

Pour gérer les environnements de test de votre organisation IMS, vous devez disposer des droits d’administration pour les environnements de test. Les utilisateurs ne disposant pas d’autorisations d’accès peuvent uniquement utiliser le point de terminaison pour [répertorier les environnements de test actifs de l’utilisateur actuel](./list-active-sandboxes.md). Pour plus d’informations sur l’attribution des autorisations Sandbox pour Experience Platform, reportez-vous à la [présentation du contrôle d’accès](../../access-control/home.md).

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées pour les exemples d’appels API dans la documentation, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Ce guide nécessite que vous ayez suivi le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en) afin d’effectuer des appels aux API de Platform avec succès. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Outre les en-têtes d’authentification, toutes les requêtes nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu :

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes contenant un payload (POST, PUT et PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Étapes suivantes

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points de terminaison et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le format général de l’API, un exemple de requête montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de réponse pour un appel réussi.
