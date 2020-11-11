---
keywords: Experience Platform;home;popular topics;Shopify;shopify;ecommerce
solution: Experience Platform
title: Création d’un connecteur Shopify à l’aide de l’API du service de flux
topic: overview
type: Tutorial
description: Ce didacticiel utilise l’API du service de flux pour vous guider dans les étapes de connexion de Shopify à l’Experience Platform.
translation-type: tm+mt
source-git-commit: b31b7dc04d32129ba5522e1b0d3e52a213347a40
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 26%

---


# Création d’un [!DNL Shopify] connecteur à l’aide de l’ [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL Shopify] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API pour vous guider à travers les étapes de la connexion [!DNL Shopify] à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Sources]](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL Shopify] using the [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] établir une connexion avec [!DNL Shopify], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point final de votre [!DNL Shopify] serveur. |
| `accessToken` | Jeton d&#39;accès de votre compte [!DNL Shopify] utilisateur. |
| `connectionSpec` | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour [!DNL Shopify] est : `4f63aa36-bd48-4e33-bb83-49fbcd11c708` |

Pour plus d&#39;informations sur la prise en main, consultez ce document [d&#39;authentification](https://shopify.dev/concepts/about-apis/authentication)Shopify.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](../../../../../tutorials/authentication.md). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par [!DNL Shopify] compte, car elle peut être utilisée pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une [!DNL Shopify] connexion, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL OData] est `4f63aa36-bd48-4e33-bb83-49fbcd11c708`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | The endpoint of the [!DNL Shopify] server. |
| `auth.params.accessToken` | Jeton d&#39;accès de votre compte [!DNL Shopify] utilisateur. |
| `connectionSpec.id` | ID de spécification de [!DNL Shopify] connexion : `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une [!DNL Shopify] connexion à l’aide de l’ [!DNL Flow Service] API et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer les connexions eCommerce à l’aide de l’API](../../explore/ecommerce.md)Flow Service.