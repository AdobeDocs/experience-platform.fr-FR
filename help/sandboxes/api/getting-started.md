---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur d’API Sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c

---


# Guide du développeur d’API Sandbox

Les sandbox d’Adobe Experience Platform fournissent des de développement  isolés qui vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter vos  de production.

Ce guide du développeur décrit les étapes à suivre pour vous aider à utiliser l’API Sandbox pour gérer les sandbox dans la plateforme d’expérience et inclut des exemples d’appels d’API pour effectuer diverses opérations.

## Prise en main de l’API Sandbox

Pour gérer les sandbox pour votre organisation IMS, vous devez disposer des autorisations d’administration Sandbox. Les utilisateurs ne disposant pas d’autorisations d’accès peuvent uniquement utiliser le point de fin pour [répertorier les sandbox actifs pour l’utilisateur](./list-active-sandboxes.md)actuel. Pour plus d’informations sur l’attribution des autorisations de sandbox pour la plateforme d’expérience, reportez-vous à l’aperçu [du ](../../access-control/home.md) .

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Ce guide nécessite que vous ayez suivi le didacticiel [d’](../../tutorials/authentication.md) authentification afin d’effectuer des appels aux API de plateforme. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Outre les en-têtes d’authentification, toutes les requêtes nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT et PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Étapes suivantes

Maintenant que vous avez rassemblé les informations d’identification requises, vous pouvez continuer à lire le reste du guide du développeur. Chaque section fournit des informations importantes sur leurs points de fin et présente des exemples d’appels d’API pour effectuer des opérations CRUD. Chaque appel comprend le format **général de l’** API, un exemple de **requête** montrant les en-têtes requis et les charges utiles correctement formatées, ainsi qu’un exemple de **réponse** pour un appel réussi.