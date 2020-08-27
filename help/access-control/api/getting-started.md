---
keywords: Experience Platform;home;popular topics;access control;api;getting started
solution: Experience Platform
title: Guide de développement du contrôle d’accès
topic: developer guide
description: Le contrôle d’accès dans Adobe Experience Platform vous permet de gérer les rôles et les autorisations pour diverses fonctionnalités de Platform à l’aide d’Adobe Admin Console. Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de passer des appels avec succès à l’API Schema Registry.
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 59%

---


# [!DNL Access control] guide du développeur

[!DNL Access control] car [!DNL Experience Platform] est administré par le [Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des environnements de test. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../home.md).

This developer guide provides information on how to format your requests to the [[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml), and covers the following operations:

- [Liste des noms des autorisations et des types de ressources](./permissions-and-resource-types.md)
- [Affichage des stratégies efficaces pour l’utilisateur actuel](./effective-policies.md)

## Prise en main

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Schema Registry] API.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Étapes suivantes

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points de terminaison et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le **format général de l’API**, un exemple de **requête** montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de **réponse** pour un appel réussi.
