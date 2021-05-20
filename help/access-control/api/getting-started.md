---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;api;prise en main
solution: Experience Platform
title: Guide de l’API Access Control
topic-legacy: developer guide
description: Le contrôle d’accès dans Adobe Experience Platform vous permet de gérer les rôles et les autorisations pour diverses fonctionnalités de Platform à l’aide d’Adobe Admin Console. Les sections suivantes apportent des informations supplémentaires aux développeurs, pour leur permettre de passer des appels avec succès à l’API Schema Registry.
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 100%

---

# Guide de l’API [!DNL Access Control]

[!DNL Access control] pour [!DNL Experience Platform] est géré à l’aide d’[Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des environnements de test. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../home.md).

Ce guide de développement fournit des informations sur la manière de formater vos requêtes dans l’[[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) et couvre les opérations suivantes :

- [Liste des noms des autorisations et des types de ressources](./permissions-and-resource-types.md)
- [Affichage des stratégies efficaces pour l’utilisateur actuel](./effective-policies.md)

## Prise en main

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de passer des appels avec succès à l’API [!DNL Schema Registry].

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Étapes suivantes

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points de terminaison et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le format général de l’API, un exemple de requête montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de réponse pour un appel réussi.
