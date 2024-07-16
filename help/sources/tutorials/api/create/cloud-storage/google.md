---
title: Création d’une connexion de base de stockage dans le cloud Google à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un compte de stockage dans le cloud Google à l’aide de l’API Flow Service.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 48%

---

# Créez une connexion de base à [!DNL Google Cloud Storage] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Google Cloud Storage] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à un compte de stockage dans le cloud Google à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] se connecte à votre compte [!DNL Google Cloud Storage], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `accessKeyId` | Chaîne alphanumérique de 61 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] sur Platform. |
| `secretAccessKey` | Chaîne codée en base 64 caractères de 40 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] sur Platform. |
| `bucketName` | Nom de votre compartiment [!DNL Google Cloud Storage]. Vous devez spécifier un nom de compartiment si vous souhaitez accorder l’accès à un sous-dossier spécifique de votre espace de stockage dans le cloud. |
| `folderPath` | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |

Pour plus d’informations sur ces valeurs, consultez le guide [Clés HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour savoir comment générer votre propre ID de clé d’accès et votre clé d’accès secrète, reportez-vous à la [[!DNL Google Cloud Storage] présentation](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Google Cloud Storage] dans les paramètres de la requête.

>[!TIP]
>
>Au cours de cette étape, vous pouvez également désigner les sous-dossiers auxquels votre compte aura accès en définissant le nom du compartiment et le chemin d’accès au sous-dossier.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Google Cloud Storage] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
          }
      },
      "connectionSpec": {
          "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.accessKeyId` | ID de clé d’accès associé à votre compte [!DNL Google Cloud Storage]. |
| `auth.params.secretAccessKey` | Clé d’accès secrète associée à votre compte [!DNL Google Cloud Storage]. |
| `auth.params.bucketName` | Nom de votre compartiment [!DNL Google Cloud Storage]. Vous devez spécifier un nom de compartiment si vous souhaitez accorder l’accès à un sous-dossier spécifique de votre espace de stockage dans le cloud. |
| `auth.params.folderPath` | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Google Cloud Storage] : `32e8f412-cdf7-464c-9885-78184cb113fd`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données de stockage dans le cloud dans le tutoriel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL Google Cloud Storage] à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet identifiant de connexion pour [ explorer le stockage dans le cloud à l’aide de l’API Flow Service ](../../explore/cloud-storage.md).
