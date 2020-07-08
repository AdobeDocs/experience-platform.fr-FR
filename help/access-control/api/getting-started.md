---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur de Contrôles d'accès
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Guide du développeur de Contrôles d&#39;accès

Access control for Experience Platform is administered through the [Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produits en Admin Console, qui lient les utilisateurs avec des autorisations et des sandbox. See the [access control overview](../home.md) for more information.

Ce guide du développeur fournit des informations sur la manière de formater vos requêtes à l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)Contrôle d&#39;accès et couvre les opérations suivantes :

- [Noms de Liste des autorisations et des types de ressources](./permissions-and-resource-types.md)
- [Vue de stratégies efficaces pour l’utilisateur actuel](./effective-policies.md)

## Prise en main

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer l&#39;API de registre du Schéma.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de l’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour passer des appels aux API Platform, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de l&#39;Experience Platform sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Étapes suivantes

Maintenant que vous avez rassemblé les informations d’identification requises, vous pouvez continuer à lire le reste du guide du développeur. Chaque section fournit des informations importantes sur leurs points de terminaison et présente des exemples d’appels d’API pour effectuer des opérations CRUD. Chaque appel comprend le format **général de l’** API, un exemple de **requête** présentant les en-têtes requis et les charges utiles correctement formatées, ainsi qu’un exemple de **réponse** pour un appel réussi.