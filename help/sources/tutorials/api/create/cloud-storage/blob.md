---
keywords: Experience Platform;accueil;rubriques les plus consultées;Azure;Azure Blob;blob;Blob
solution: Experience Platform
title: Création d’une connexion de base Azure Blob à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Azure Blob à l’aide de l’API Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 9%

---

# Créez une connexion de base [!DNL Azure Blob] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Azure Blob] (ci-après appelée &quot;[!DNL Blob]&quot;) à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour créer une connexion source [!DNL Blob] à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à votre stockage [!DNL Blob], vous devez fournir des valeurs pour la propriété de connexion suivante :

| Credential | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne contenant les informations d’autorisation nécessaires pour authentifier [!DNL Blob] auprès de l’Experience Platform. Le modèle de chaîne de connexion [!DNL Blob] est le suivant : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Pour plus d’informations sur les chaînes de connexion, consultez ce [!DNL Blob] document sur [la configuration des chaînes de connexion](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre compte [!DNL Blob]. Le modèle d’URI SAS [!DNL Blob] est le suivant : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Pour plus d’informations, consultez ce [!DNL Blob] document sur les [URI de signature d’accès partagé](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Blob] est : `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Blob] dans le cadre des paramètres de requête.

### Créer une connexion de base [!DNL Blob] à l’aide de l’authentification par chaîne de connexion

Pour créer une connexion de base [!DNL Blob] à l’aide de l’authentification par chaîne de connexion, envoyez une demande de POST à l’API [!DNL Flow Service] tout en fournissant votre [!DNL Blob] `connectionString`.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Blob] à l’aide de l’authentification par chaîne de connexion :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion requise pour accéder aux données dans votre stockage Blob. Le modèle de chaîne de connexion Blob est le suivant : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | L’identifiant de spécification de connexion de stockage Blob est : `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Créer une connexion de base [!DNL Blob] à l’aide de l’URI de signature d’accès partagé

Un URI de signature d’accès partagé (SAS) permet une délégation sécurisée de l’autorisation à votre compte [!DNL Blob]. Vous pouvez utiliser SAS pour créer des informations d’identification d’authentification avec des degrés d’accès différents, car une authentification SAS vous permet de définir des autorisations, des dates de début et d’expiration, ainsi que des dispositions sur des ressources spécifiques.

Pour créer une connexion blob [!DNL Blob] à l’aide de l’URI de signature d’accès partagé, envoyez une demande de POST à l’API [!DNL Flow Service] tout en fournissant des valeurs pour votre [!DNL Blob] `sasUri`.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Blob] à l’aide de l’URI de signature d’accès partagé :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SasURIAuthentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.connectionString` | URI SAS requis pour accéder aux données dans votre stockage [!DNL Blob]. Le modèle d’URI SAS [!DNL Blob] est le suivant : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | L&#39;identifiant de spécification de connexion de stockage [!DNL Blob] est : `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL Blob] à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet identifiant de connexion pour [explorer le stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md) ou [ingérer des données Parquet à l’aide de l’API Flow Service](../../cloud-storage-parquet.md).
