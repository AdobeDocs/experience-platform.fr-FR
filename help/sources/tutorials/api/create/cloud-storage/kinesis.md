---
title: Créer une connexion Source Amazon Kinesis à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à une source Amazon Kinesis à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 50%

---

# Créer une connexion source [!DNL Amazon Kinesis] à l’aide de l’API Flow Service

>[!IMPORTANT]
>
>La source [!DNL Amazon Kinesis] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Ce tutoriel vous guide tout au long des étapes de connexion de [!DNL Amazon Kinesis] (ci-après dénommé « [!DNL Kinesis] ») à Experience Platform à l’aide de l’API [[!DNL Flow Service] &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à connecter [!DNL Kinesis] à Experience Platform à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puissiez vous connecter à votre compte [!DNL Amazon Kinesis], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `accessKeyId` | L’ID de clé d’accès correspond à la moitié de la paire de clés d’accès utilisée pour authentifier votre compte [!DNL Kinesis] auprès d’Experience Platform. |
| `secretKey` | La clé d’accès secrète est l’autre moitié de la paire de clés d’accès utilisée pour authentifier votre compte [!DNL Kinesis] auprès d’Experience Platform. |
| `region` | Région de votre compte [!DNL Kinesis]. Pour plus d’informations sur les régions[&#128279;](../../../../ip-address-allow-list.md) consultez le guide sur l’ajout d’adresses IP à une liste autorisée de données . |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion [!DNL Kinesis] est : `86043421-563b-46ec-8e6c-e23184711bf6`. |

Pour plus d’informations sur la [!DNL Kinesis] des clés d’accès et leur génération, reportez-vous à ce [[!DNL AWS] guide sur la gestion des clés d’accès pour les utilisateurs IAM](https://docs.aws.amazon.com/fr_fr/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

La première étape de création d’une connexion source consiste à authentifier votre source [!DNL Kinesis] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL Kinesis] dans le cadre des paramètres de requête.

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
| `auth.params.accessKeyId` | Identifiant de clé d’accès de votre compte [!DNL Kinesis]. |
| `auth.params.secretKey` | Clé d’accès secrète de votre compte [!DNL Kinesis]. |
| `auth.params.region` | Région de votre compte [!DNL Kinesis]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Kinesis] : `86043421-563b-46ec-8e6c-e23184711bf6`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Créer une connexion source {#source}

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et l’identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation.

Pour créer une connexion source, envoyez une requête POST au point d’entrée `/sourceConnections` de l’API [!DNL Flow Service].

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Nom de votre connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez fournir pour inclure plus d’informations sur votre connexion source. |
| `baseConnectionId` | Identifiant de connexion de base de votre source [!DNL Kinesis] générée à l’étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion fixe pour [!DNL Kinesis]. Cet ID est le suivant : `86043421-563b-46ec-8e6c-e23184711bf6`. |
| `data.format` | Format des données [!DNL Kinesis] que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |
| `params.stream` | Nom du flux de données à partir duquel extraire les enregistrements. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |
| `params.reset` | Ce paramètre définit la manière dont les données seront lues. Utilisez `latest` pour commencer la lecture à partir des données les plus récentes et `earliest` pour commencer la lecture à partir des premières données disponibles dans le flux. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Le tutoriel suivant requiert cet ID pour créer un flux de données.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>Après avoir créé ou mis à jour un flux de données en continu, une brève pause de 5 minutes dans l’ingestion des données est nécessaire pour éviter toute instance potentielle de perte de données ou d’abandon de données.

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion source [!DNL Kinesis] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet ID de connexion source dans le tutoriel suivant pour [créer un flux de données en continu à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../collect/streaming.md).
