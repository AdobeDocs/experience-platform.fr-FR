---
keywords: Experience Platform;accueil;rubriques les plus consultées;Kinesis;Genesis;Amazon Kinesis;Amazon kinesis
solution: Experience Platform
title: Création d’une connexion source Kinesis Amazon à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à une source Kinesis Amazon à l’aide de l’API Flow Service.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 8%

---

# Créez un [!DNL Amazon Kinesis] Connexion source à l’aide de l’API Flow Service

Ce tutoriel vous guide tout au long des étapes pour vous connecter. [!DNL Amazon Kinesis] (ci-après dénommés &quot;[!DNL Kinesis]&quot;) à l’Experience Platform, à l’aide de la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md)[!DNL Platform] : Experience  fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Kinesis] vers Platform à l’aide de [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Amazon Kinesis] , vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| ---------- | ----------- |
| `accessKeyId` | L’identifiant de clé d’accès est la moitié de la paire de clés d’accès utilisée pour authentifier votre [!DNL Kinesis] compte à Platform. |
| `secretKey` | La clé d’accès secrète est l’autre moitié de la paire de clés d’accès utilisée pour authentifier votre [!DNL Kinesis] compte à Platform. |
| `region` | La région de votre [!DNL Kinesis] compte . Consultez le guide sur la [Ajout d’adresses IP à votre liste autorisée](../../../../ip-address-allow-list.md) pour plus d’informations sur les régions. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. Le [!DNL Kinesis] l’identifiant de spécification de connexion est : `86043421-563b-46ec-8e6c-e23184711bf6`. |

Pour plus d’informations sur [!DNL Kinesis] les clés d&#39;accès et leur génération, voir à ce sujet [[!DNL AWS] Guide de gestion des clés d’accès pour les utilisateurs IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

La première étape de la création d’une connexion source consiste à authentifier votre [!DNL Kinesis] source et générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL Kinesis] informations d’identification d’authentification dans le cadre des paramètres de requête.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.accessKeyId` | L’identifiant de la clé d’accès pour votre [!DNL Kinesis] compte . |
| `auth.params.secretKey` | La clé d’accès secrète de votre [!DNL Kinesis] compte . |
| `auth.params.region` | La région de votre [!DNL Kinesis] compte . |
| `connectionSpec.id` | Le [!DNL Kinesis] identifiant de spécification de connexion : `86043421-563b-46ec-8e6c-e23184711bf6` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Création d’une connexion source {#source}

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et l’identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation IMS.

Pour créer une connexion source, envoyez une requête de POST au `/sourceConnections` point d’entrée du [!DNL Flow Service] API.

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez fournir pour inclure plus d’informations sur votre connexion source. |
| `baseConnectionId` | L’identifiant de connexion de base de votre [!DNL Kinesis] source générée à l’étape précédente. |
| `connectionSpec.id` | L’identifiant de spécification de connexion fixe pour [!DNL Kinesis]. Cet identifiant est : `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Le format de la variable [!DNL Kinesis] données que vous souhaitez ingérer. Actuellement, le seul format de données pris en charge est `json`. |
| `params.stream` | Nom du flux de données duquel extraire les enregistrements. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |
| `params.reset` | Ce paramètre définit la manière dont les données seront lues. Utilisation `latest` pour commencer la lecture à partir des données les plus récentes et utiliser `earliest` pour commencer la lecture à partir des premières données disponibles dans le flux. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Cet identifiant est requis dans le tutoriel suivant pour créer un flux de données.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Kinesis] connexion source à l’aide de la fonction [!DNL Flow Service] API. Vous pouvez utiliser cet identifiant de connexion source dans le tutoriel suivant pour [créez un flux de données en continu à l’aide de la fonction [!DNL Flow Service] API](../../collect/streaming.md).
