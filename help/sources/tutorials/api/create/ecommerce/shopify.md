---
keywords: Experience Platform ; accueil ; sujets populaires ; Shopify ; shopify ; ecommerce
solution: Experience Platform
title: Création d’une connexion source du connecteur Shopify à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Shopify à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 27%

---

# Créez une connexion source [!DNL Shopify] à l’aide de l’API [!DNL Flow Service].

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) pour vous guider dans les étapes de connexion de [!DNL Shopify] à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Sources]](../../../../home.md):  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Shopify] à l&#39;aide de l&#39;API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL Shopify], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point de terminaison de votre serveur [!DNL Shopify]. |
| `accessToken` | Jeton d&#39;accès de votre compte utilisateur [!DNL Shopify]. |
| `connectionSpec` | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour [!DNL Shopify] est : `4f63aa36-bd48-4e33-bb83-49fbcd11c708` |

Pour plus d&#39;informations sur la prise en main, consultez ce [document d&#39;authentification Shopify](https://shopify.dev/concepts/about-apis/authentication).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte [!DNL Shopify], car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion [!DNL Shopify], l&#39;identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL Shopify] est `4f63aa36-bd48-4e33-bb83-49fbcd11c708`.

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
| `auth.params.host` | Point de terminaison du serveur [!DNL Shopify]. |
| `auth.params.accessToken` | Jeton d&#39;accès de votre compte utilisateur [!DNL Shopify]. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Shopify] : `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion [!DNL Shopify] à l&#39;aide de l&#39;API [!DNL Flow Service] et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer les connexions eCommerce à l’aide de l’API Flow Service](../../explore/ecommerce.md).
