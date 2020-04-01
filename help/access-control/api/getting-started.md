---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide du développeur des '
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Guide du développeur des 

Access control for Experience Platform is administered through the [Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité tire parti des  de produits dans la Console d’administration, qui relient les utilisateurs à des autorisations et des sandbox. See the [access control overview](../home.md) for more information.

Ce guide du développeur fournit des informations sur la manière de formater vos requêtes à l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)et couvre les opérations suivantes :

- [des noms des autorisations et des types de ressources](./permissions-and-resource-types.md)
- [des stratégies efficaces pour l’utilisateur actuel](./effective-policies.md)

## Prise en main

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels vers l&#39;API de Registre du .

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Étapes suivantes

Maintenant que vous avez rassemblé les informations d’identification requises, vous pouvez continuer à lire le reste du guide du développeur. Chaque section fournit des informations importantes sur leurs points de fin et présente des exemples d’appels d’API pour effectuer des opérations CRUD. Chaque appel comprend le format **général de l’** API, un exemple de **requête** montrant les en-têtes requis et les charges utiles correctement formatées, ainsi qu’un exemple de **réponse** pour un appel réussi.