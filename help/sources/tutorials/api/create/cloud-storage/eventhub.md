---
keywords: Experience Platform;accueil;rubriques populaires;hub d’événements Azure;hub d’événements
solution: Experience Platform
title: Création d’une connexion source Azure Event Hubs à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un compte Azure Event Hubs à l’aide de l’API Flow Service.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 61%

---


# Créez un [!DNL Azure Event Hubs] connexion source à l’aide de la fonction [!DNL Flow Service] API

Ce tutoriel vous guide tout au long des étapes de connexion de [!DNL Azure Event Hubs] (ci-après dénommé « [!DNL Event Hubs] ») à Experience Platform à l’aide de l’API [[!DNL Flow Service] ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
- [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à connecter [!DNL Event Hubs] à Platform à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Event Hubs] , vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `sasKeyName` | Nom de la règle d’autorisation, également appelé nom de clé SAS. |
| `sasKey` | La clé Principale de la variable [!DNL Event Hubs] espace de noms. Le `sasPolicy` que la variable `sasKey` correspond à `manage` les droits configurés pour [!DNL Event Hubs] liste à renseigner. |
| `namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Pour plus d’informations sur ces valeurs, reportez-vous à la section [ce document Événements Hub](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

La première étape de création d’une connexion source consiste à authentifier votre source [!DNL Event Hubs] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL Event Hubs] dans le cadre des paramètres de requête.

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.sasKeyName` | Nom de la règle d’autorisation, également appelé nom de clé SAS. |
| `auth.params.sasKey` | Signature d’accès partagé générée. |
| `auth.params.namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. |
| `connectionSpec.id` | Le [!DNL Event Hubs] l’identifiant de spécification de connexion est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant de connexion de est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Créer une connexion source

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et un identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation.

Pour créer une connexion source, envoyez une requête POST au point d’entrée `/sourceConnections` de l’API [!DNL Flow Service].

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Azure Event Hubs source connection",
        "description": "A source connection for Azure Event Hubs",
        "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez fournir pour inclure plus d’informations sur votre connexion source. |
| `baseConnectionId` | Identifiant de connexion de de votre source [!DNL Event Hubs] générée à l’étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion fixe pour [!DNL Event Hubs]. Cet ID est le suivant : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`.. |
| `data.format` | Format des données [!DNL Event Hubs] que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |
| `params.eventHubName` | Le nom de votre [!DNL Event Hubs] source. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |
| `params.reset` | Ce paramètre définit la manière dont les données seront lues. Utilisation `latest` pour commencer la lecture à partir des données les plus récentes et utiliser `earliest` pour commencer la lecture à partir des premières données disponibles dans le flux. Ce paramètre est facultatif et la valeur par défaut est `earliest` si non fourni. |
| `params.consumerGroup` | Le mécanisme de publication ou d’abonnement à utiliser pour [!DNL Event Hubs]. Ce paramètre est facultatif et la valeur par défaut est `$Default` si non fourni. Consultez cette section [[!DNL Event Hubs] guide sur les consommateurs d’événements](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) pour plus d’informations. |

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Event Hubs] connexion source à l’aide de la fonction [!DNL Flow Service] API. Vous pouvez utiliser cet ID de connexion source dans le tutoriel suivant pour [créer un flux de données en continu à l’aide de l’API  [!DNL Flow Service] ](../../collect/streaming.md).
