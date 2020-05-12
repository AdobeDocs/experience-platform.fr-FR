---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur Gen2 pour Enregistrement Azure Data Lake à l'aide de l'API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 7ffe560f455973da3a37ad102fbb8cc5969d5043
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 2%

---


# Création d&#39;un connecteur Gen2 d&#39;Enregistrement Azure Data Lake à l&#39;aide de l&#39;API Flow Service

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API Flow Service pour vous guider à travers les étapes de connexion de la plateforme Experience Platform à Azure Data Lake Enregistrement Gen2 (ci-après appelé &quot;ADLS Gen2&quot;).

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plate-forme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir créer un connecteur source ADLS Gen2 à l’aide de l’API Flow Service.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte à ADLS Gen2, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | URL de l’adresse. |
| `servicePrincipalId` | ID client de l’application. |
| `servicePrincipalKey` | La clé de l&#39;application. |
| `tenant` | Informations sur le client qui contient votre application. |

Pour plus d&#39;informations sur ces valeurs, consultez [ce document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte ADLS Gen2, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.url` | Point de terminaison de l’URL pour votre compte ADLS Gen2. |
| `auth.params.servicePrincipalId` | ID principal de service de votre compte ADLS Gen2. |
| `auth.params.servicePrincipalKey` | Clé principale de service de votre compte ADLS Gen2. |
| `auth.params.tenant` | Informations sur le client de votre compte ADLS Gen2. |
| `connectionSpec.id` | ID de spécification de connexion ADLS Gen2 : `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre enregistrement cloud à l’étape suivante.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion ADLS Gen2 à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet ID de connexion pour [explorer les enregistrements de cloud à l’aide de l’API](../../explore/cloud-storage.md) Flow Service ou [assimiler des données de parquet à l’aide de l’API](../../cloud-storage-parquet.md)Flow Service.
