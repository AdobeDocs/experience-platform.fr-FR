---
keywords: Experience Platform ; accueil ; rubriques populaires ; Azure ; azure blob ; blob ; Blob
solution: Experience Platform
title: Création d’une connexion de base Blob Azure à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Azure Blob à l’aide de l’API Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 9%

---

# Créer un [!DNL Azure Blob] connexion de base à l’aide de [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous explique les étapes à suivre pour créer une connexion de base pour [!DNL Azure Blob] (ci-après dénommés &quot;[!DNL Blob]&quot;) en utilisant la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, étiqueter et améliorer les données entrantes à l’aide des services de la plate-forme.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir créer un fichier [!DNL Blob] connexion source à l’aide de [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Blob] , vous devez fournir des valeurs pour la propriété de connexion suivante :

| Informations d&#39;identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne contenant les informations d’autorisation nécessaires à l’authentification [!DNL Blob] à l’Experience Platform. Le [!DNL Blob] le modèle de chaîne de connexion est : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Pour plus d’informations sur les chaînes de connexion, consultez cette section [!DNL Blob] document sur [configuration des chaînes de connexion](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | L’URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre [!DNL Blob] compte. Le [!DNL Blob] Le modèle d&#39;URI SAS est : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Pour plus d’informations, voir [!DNL Blob] document sur [URI de signature d&#39;accès partagé](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. ID de spécification de connexion pour [!DNL Blob] est : `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### Utilisation des API de plate-forme

Pour plus d’informations sur la manière d’effectuer des appels vers les API de plate-forme, consultez le guide sur [prise en main des API de plate-forme](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et la plate-forme, y compris les informations d&#39;identification de votre source, l&#39;état actuel de la connexion et votre ID de connexion de base unique. L’ID de connexion de base vous permet d’explorer et de parcourir les fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez assimiler, y compris des informations concernant leurs types et formats de données.

Pour créer un ID de connexion de base, effectuez une demande de POST à l’adresse `/connections` point de terminaison lors de la fourniture de votre [!DNL Blob] les informations d&#39;identification d&#39;authentification dans le cadre des paramètres de demande.

### Créer un [!DNL Blob] connexion de base à l&#39;aide de l&#39;authentification basée sur une chaîne de connexion

Pour créer un [!DNL Blob] connexion de base à l&#39;aide de l&#39;authentification basée sur une chaîne de connexion, effectuez une demande de POST à la [!DNL Flow Service] API lors de la fourniture de votre [!DNL Blob] `connectionString`.

**Format d’API**

```http
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour [!DNL Blob] utilisation de l&#39;authentification basée sur une chaîne de connexion :

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
| `auth.params.connectionString` | Chaîne de connexion requise pour accéder aux données de votre stockage Blob. Le modèle de chaîne de connexion Blob est le suivant : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | L&#39;ID de spécification de connexion de stockage Blob est : `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`). Cet ID est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Créer un [!DNL Blob] connexion de base à l&#39;aide de l&#39;URI de signature d&#39;accès partagé

Un URI de signature d&#39;accès partagé (SAS) permet de déléguer des autorisations sécurisées à votre [!DNL Blob] compte. Vous pouvez utiliser SAS pour créer des informations d&#39;identification d&#39;authentification avec différents degrés d&#39;accès, car une authentification SAS vous permet de définir des autorisations, des dates de début et d&#39;expiration, ainsi que des dispositions pour des ressources spécifiques.

Pour créer un [!DNL Blob] connexion blob à l&#39;aide de l&#39;URI de signature d&#39;accès partagé, effectuez une demande de POST vers [!DNL Flow Service] API tout en fournissant des valeurs pour votre [!DNL Blob] `sasUri`.

**Format d’API**

```http
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour [!DNL Blob] à l&#39;aide de l&#39;URI de signature d&#39;accès partagé :

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
| `auth.params.connectionString` | L&#39;URI SAS requis pour accéder aux données dans votre [!DNL Blob] stockage. Le [!DNL Blob] Le modèle d&#39;URI SAS est : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | Le [!DNL Blob] L&#39;ID de spécification de connexion de stockage est : `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`). Cet ID est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un fichier [!DNL Blob] la connexion à l’aide d’API et d’un ID unique a été obtenue dans le corps de la réponse. Vous pouvez utiliser cet ID de connexion pour [exploration des sites de stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
