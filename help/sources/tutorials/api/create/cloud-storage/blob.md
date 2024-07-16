---
title: Création d’une connexion de base Azure Blob à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Azure Blob à l’aide de l’API Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 41%

---

# Créez une connexion de base [!DNL Azure Blob] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel décrit les étapes à suivre pour créer une connexion de base pour [!DNL Azure Blob] (ci-après appelée &quot;[!DNL Blob]&quot;) à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour créer une connexion source [!DNL Blob] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] se connecte à votre stockage [!DNL Blob], vous devez fournir des valeurs pour la propriété de connexion suivante :

>[!BEGINTABS]

>[!TAB Authentification de chaîne de connexion]

| Informations d’identification | Description |
| --- | --- |
| `connectionString` | Chaîne contenant les informations d’autorisation nécessaires pour authentifier [!DNL Blob] sur Experience Platform. Le modèle de chaîne de connexion [!DNL Blob] est : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Pour plus d&#39;informations sur les chaînes de connexion, consultez ce document [!DNL Blob] sur la [configuration des chaînes de connexion](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Blob] est `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!TAB Authentification URI SAS]

| Informations d’identification | Description |
| --- | --- |
| `sasUri` | URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre compte [!DNL Blob]. Le modèle d’URI SAS [!DNL Blob] est : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Pour plus d’informations, consultez ce document [!DNL Blob] sur les [ URI de signature d’accès partagé ](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Nom du conteneur auquel vous souhaitez attribuer l’accès. Lors de la création d’un compte avec la source [!DNL Blob], vous pouvez fournir un nom de conteneur pour spécifier l’accès de l’utilisateur au sous-dossier de votre choix. |
| `folderPath` | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Blob] est `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!ENDTABS]

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d&#39;authentification d&#39;une connexion de base [!DNL Blob]. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

La source [!DNL Blob] prend en charge l’authentification de la chaîne de connexion et de la signature d’accès partagée (SAS). Un URI de signature d’accès partagé (SAS) permet une délégation sécurisée de l’autorisation de votre compte [!DNL Blob]. Vous pouvez utiliser SAS pour créer des informations d’identification d’authentification avec des degrés d’accès différents, car une authentification SAS vous permet de définir des autorisations, des dates de début et d’expiration, ainsi que des dispositions sur des ressources spécifiques.

Au cours de cette étape, vous pouvez également désigner les sous-dossiers auxquels votre compte aura accès en définissant le nom du conteneur et le chemin d’accès au sous-dossier.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL Blob] dans le cadre des paramètres de requête.

**Format d’API**

```http
POST /connections
```

**Requête**

>[!BEGINTABS]

>[!TAB Chaîne de connexion]

La requête suivante crée une connexion de base pour [!DNL Blob] à l’aide de l’authentification par chaîne de connexion :

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
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

| Propriété | Description |
| -------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion requise pour accéder aux données dans votre stockage Blob. Le modèle de chaîne de connexion Blob est : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | L’identifiant de spécification de connexion de stockage Blob est : `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB Authentification URI SAS]

Pour créer une connexion [!DNL Blob] à l’aide de l’URI de signature d’accès partagé, envoyez une demande de POST à l’API [!DNL Flow Service] tout en fournissant des valeurs pour votre [!DNL Blob] `sasUri`.

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
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

| Propriété | Description |
| -------- | ----------- |
| `auth.params.connectionString` | URI SAS requis pour accéder aux données de votre stockage [!DNL Blob]. Le modèle URI SAS [!DNL Blob] est : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | L&#39;identifiant de spécification de connexion de stockage [!DNL Blob] est : `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL Blob] à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet identifiant de connexion pour [ explorer le stockage dans le cloud à l’aide de l’API Flow Service ](../../explore/cloud-storage.md).
