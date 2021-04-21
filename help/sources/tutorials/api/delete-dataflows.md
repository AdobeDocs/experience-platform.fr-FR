---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de flux ; API ; api ; supprimer ; supprimer des flux de données
solution: Experience Platform
title: Suppression d’un flux de données à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment supprimer des flux de données par lot et en flux continu à l’aide de l’API de service de flux.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 28%

---

# Suppression d’un flux de données à l’aide de l’API du service de flux

Vous pouvez supprimer les flux de données par lot et en flux continu qui contiennent des erreurs ou qui sont devenus obsolètes à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

Ce didacticiel décrit les étapes à suivre pour supprimer les flux de données créés avec des sources par lot et en flux continu à l’aide de [!DNL Flow Service].

## Prise en main

Ce didacticiel nécessite que vous disposiez d’un ID de flux valide. Si vous ne disposez pas d’un ID de flux valide, sélectionnez le connecteur de votre choix dans le [aperçu des sources](../../home.md) et suivez les étapes décrites avant de tenter ce didacticiel.

Ce didacticiel nécessite également une bonne compréhension des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour supprimer un flux de données à l&#39;aide de l&#39;API [!DNL Flow Service].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Suppression d’un flux de données

Avec un ID de flux existant, vous pouvez supprimer un flux de données en exécutant une requête de DELETE à l&#39;API [!DNL Flow Service].

**Format d’API**

```http
DELETE /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | Valeur `id` unique du flux de données à supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’envoyer une demande de recherche (GET) au flux de données. L’API renvoie une erreur HTTP 404 (introuvable), indiquant que le flux de données a été supprimé.

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à utiliser l&#39;API [!DNL Flow Service] pour supprimer un flux de données existant.

Pour savoir comment effectuer ces opérations à l’aide de l’interface utilisateur, consultez le didacticiel de [suppression de flux de données dans l’interface utilisateur](../../tutorials/ui/delete.md).
