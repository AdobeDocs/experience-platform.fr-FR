---
keywords: Experience Platform;accueil;rubriques les plus consultées;Kinesis;Genesis;Amazon Kinesis;Amazon kinesis
solution: Experience Platform
title: Création d’une connexion source Kinesis Amazon à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à une source Kinesis Amazon à l’aide de l’API Flow Service.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 7%

---

# Créer une connexion source [!DNL Amazon Kinesis] à l’aide de l’API Flow Service

Ce tutoriel vous guide tout au long des étapes permettant de connecter [!DNL Amazon Kinesis] (ci-après appelé &quot;[!DNL Kinesis]&quot;) à l’Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md)[!DNL Platform] : Experience fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour connecter [!DNL Kinesis] à Platform à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à votre compte [!DNL Amazon Kinesis], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| ---------- | ----------- |
| `accessKeyId` | L’ID de clé d’accès correspond à la moitié de la paire de clés d’accès utilisée pour authentifier votre compte [!DNL Kinesis] sur Platform. |
| `secretKey` | La clé d’accès secrète est l’autre moitié de la paire de clés d’accès utilisée pour authentifier votre compte [!DNL Kinesis] sur Platform. |
| `region` | La région de votre compte [!DNL Kinesis]. Pour plus d’informations sur les régions, consultez le guide sur l’[ajout d’adresses IP à votre liste autorisée ](../../../../ip-address-allow-list.md) . |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion [!DNL Kinesis] est : `86043421-563b-46ec-8e6c-e23184711bf6`. |

Pour plus d’informations sur les [!DNL Kinesis] clés d’accès et la manière de les générer, consultez ce [[!DNL AWS] guide sur la gestion des clés d’accès pour les utilisateurs IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

La première étape de la création d’une connexion source consiste à authentifier votre source [!DNL Kinesis] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Kinesis] dans le cadre des paramètres de requête.

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
| `auth.params.accessKeyId` | Identifiant de la clé d’accès pour votre compte [!DNL Kinesis]. |
| `auth.params.secretKey` | Clé d’accès secrète pour votre compte [!DNL Kinesis]. |
| `auth.params.region` | La région de votre compte [!DNL Kinesis]. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Kinesis] : `86043421-563b-46ec-8e6c-e23184711bf6` |

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

Pour créer une connexion source, envoyez une requête de POST au point de terminaison `/sourceConnections` de l’API [!DNL Flow Service].

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
| `baseConnectionId` | L’identifiant de connexion de base de votre source [!DNL Kinesis] qui a été généré à l’étape précédente. |
| `connectionSpec.id` | L’identifiant de spécification de connexion fixe pour [!DNL Kinesis]. Cet identifiant est : `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Format des données [!DNL Kinesis] que vous souhaitez ingérer. Actuellement, le seul format de données pris en charge est `json`. |
| `params.stream` | Nom du flux de données duquel extraire les enregistrements. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |
| `params.reset` | Ce paramètre définit la manière dont les données seront lues. Utilisez `latest` pour commencer la lecture à partir des données les plus récentes et utilisez `earliest` pour commencer la lecture à partir des premières données disponibles dans le flux. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est requis dans le tutoriel suivant pour créer un flux de données.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion source [!DNL Kinesis] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion source dans le tutoriel suivant pour [créer un flux de données en continu à l’aide de l’ [!DNL Flow Service] API](../../collect/streaming.md).
