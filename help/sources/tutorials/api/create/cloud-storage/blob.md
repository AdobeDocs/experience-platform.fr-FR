---
title: Connecter Azure Blob Storage à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Azure Blob à l’aide de l’API Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 9%

---

# Connexion de [!DNL Azure Blob Storage] à Experience Platform à l’aide de l’API

Lisez ce guide pour savoir comment connecter votre compte [!DNL Azure Blobg Storage] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

### Collecter les informations d’identification requises

Lisez la [[!DNL Azure Blob Storage] présentation](../../../../connectors/cloud-storage/blob.md#authentication) pour plus d’informations sur l’authentification.

## Connexion de votre compte [!DNL Azure Blob Storage] à Experience Platform {#connect}

Pour plus d’informations sur la connexion de votre compte [!DNL Azure Blob Storage] à Experience Platform, lisez les étapes ci-dessous.

### Créer une connexion de base

>[!NOTE]
>
>Une fois créé, vous ne pouvez pas modifier le type d’authentification d’une connexion de base [!DNL Azure Blob Storage]. Pour modifier le type d’authentification, vous devez créer une connexion de base.

Une connexion de base lie votre source à Experience Platform, stockant les détails d’authentification, le statut de connexion et un identifiant unique. Utilisez cet identifiant pour parcourir les fichiers sources et identifier les éléments spécifiques à ingérer, y compris leurs types et formats de données.

Vous pouvez connecter votre compte [!DNL Azure Blob Storage] à Experience Platform à l’aide des types d’authentification suivants :

* **Authentification de la clé de compte** : utilise la clé d’accès du compte de stockage pour s’authentifier et se connecter à votre compte [!DNL Azure Blob Storage].
* **Signature d’accès partagé (SAS)** : utilise un URI SAS pour fournir un accès délégué et limité dans le temps aux ressources de votre compte [!DNL Azure Blob Storage].
* **Authentification basée sur le principal de service** : utilise un principal de service Azure Active Directory (AAD) (identifiant client et secret) pour s’authentifier en toute sécurité sur votre compte de stockage Blob Azure.

**Format d’API**

```https
POST /connections
```

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification dans les paramètres de la requête.

>[!BEGINTABS]

>[!TAB Authentification de la clé de compte]

Pour utiliser l’authentification par clé de compte, saisissez les valeurs de votre `connectionString`, de votre `container` et de votre `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Paramètre | Description |
| --- | --- |
| `connectionString` | Chaîne de connexion de votre compte [!DNL Azure Blob Storage]. Le modèle de chaîne de connexion est : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`. |
| `container` | Nom du conteneur de [!DNL Azure Blob Storage] dans lequel vos fichiers de données sont stockés. |
| `folderPath` | Chemin d’accès dans le conteneur spécifié où se trouvent vos fichiers. |
| `connectionSpec.id` | Identifiant de spécification de connexion de la source de [!DNL Azure Blob Storage]. Cet identifiant est corrigé comme suit : `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Signature d’accès partagé]

Pour utiliser la signature d’accès partagé, saisissez les valeurs de votre `sasUri`, de votre `container` et de votre `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Paramètre | Description |
| --- | --- |
| `sasUri` | URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre compte. Le modèle URI SAS est le suivant : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. |
| `container` | Nom du conteneur de [!DNL Azure Blob Storage] dans lequel vos fichiers de données sont stockés. |
| `folderPath` | Chemin d’accès dans le conteneur spécifié où se trouvent vos fichiers. |
| `connectionSpec.id` | Identifiant de spécification de connexion de la source de [!DNL Azure Blob Storage]. Cet identifiant est corrigé comme suit : `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Authentification basée sur le principal de service]

Pour vous connecter via l’authentification principale de service, indiquez les valeurs suivantes pour votre connexion : `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` et `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Paramètre | Description |
| --- | --- |
| `serviceEndpoint` | URL du point d’entrée de votre compte [!DNL Azure Blob Storage]. Généralement au format : `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `servicePrincipalId` | Identifiant client/d’application du principal de service Azure Active Directory (AAD) utilisé pour l’authentification. |
| `servicePrincipalKey` | Secret client ou mot de passe associé au principal de service Azure. |
| `accountKind` | Type de votre compte [!DNL Azure Blob Storage]. Les valeurs courantes comprennent `StorageV2`, `BlobStorage` ou `Storage`. |
| `tenant` | L’identifiant du client Azure Active Directory (AAD) où le principal de service est enregistré. |
| `container` | Nom du conteneur de [!DNL Azure Blob Storage] dans lequel vos fichiers de données sont stockés. |
| `folderPath` | Chemin d’accès dans le conteneur spécifié où se trouvent vos fichiers. |
| `connectionSpec.id` | Identifiant de spécification de connexion de la source de [!DNL Azure Blob Storage]. Cet identifiant est corrigé comme suit : `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!ENDTABS]

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL Blob] à l’aide d’API et obtenu un identifiant unique dans le cadre du corps de la réponse. Vous pouvez utiliser cet identifiant de connexion pour [explorer les espaces de stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
