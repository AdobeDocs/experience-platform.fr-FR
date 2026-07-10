---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide de développement des sandbox
solution: Experience Platform
title: Prise en main de l’API Sandbox
description: L’API Sandbox permet aux développeurs de gérer les sandbox par programmation dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
TQID: https://experienceleague.adobe.com/DZk-wbm6bJeiqFbZhxaXQNvhXFwxrIAHqVJGlybbj-E
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: adf04a6a-050f-44bc-a52c-db79ccb22ebf
subfeature_v2: id: a16ec9c0-4484-4842-b9a0-5504cde38e6aid: a9eb38d5-9d89-492f-af4e-b968a07f2d91id: d21bd11d-08df-4cd6-ad8f-cb59a09de5c0
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: cb424651efb1b4d71717c06a4b0d6e9354f0dcc7
workflow-type: tm+mt
source-wordcount: 381
ht-degree: 80%

---

# Prise en main de l’API Sandbox

Les sandbox d’Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des opérations et de créer des configurations personnalisées sans affecter votre environnement de production.

Ce guide de développement décrit les étapes à suivre pour utiliser l’API Sandbox afin de gérer les sandbox dans Experience Platform. Il inclut des exemples d’appels API pour effectuer diverses opérations.

## Conditions préalables

Pour gérer des sandbox pour votre organisation, vous devez disposer d’autorisations d’administration des sandbox. Les utilisateurs sans autorisation d’accès peuvent uniquement utiliser le point d’entrée [sandbox disponibles](./available.md) pour répertorier les sandbox actifs pour l’utilisateur actuel. Pour plus d’informations sur l’attribution des autorisations Sandbox pour Experience Platform, reportez-vous à la [présentation du contrôle d’accès](../../access-control/home.md).

### Lecture d&#39;exemples d&#39;appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées pour les exemples d’appels API dans la documentation, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Ce guide nécessite que vous ayez suivi le tutoriel [authentification](/help/landing/api-authentication.md) pour passer avec succès des appels aux API Experience Platform. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Outre les en-têtes d’authentification, toutes les requêtes nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes contenant un payload (POST, PUT et PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Étapes suivantes

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points d’entrée et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le format général de l’API, un exemple de requête montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de réponse pour un appel réussi.

