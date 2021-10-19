---
keywords: Experience Platform ; accueil ; rubriques populaires ; Stockage cloud Google ; stockage cloud google ; stockage cloud ; google ; Google
solution: Experience Platform
title: Création d'une connexion de base de stockage Google Cloud à l'aide de l'API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un compte de stockage Google Cloud à l’aide de l’API Flow Service.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 11%

---

# Créer un [!DNL Google Cloud Storage] connexion de base à l’aide de [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous explique les étapes à suivre pour créer une connexion de base pour [!DNL Google Cloud Storage] à l’aide de la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, étiqueter et améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir vous connecter à un compte de stockage Google Cloud à l’aide de l’onglet [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Google Cloud Storage] , vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d&#39;identification | Description |
| ---------- | ----------- |
| `accessKeyId` | Chaîne alphanumérique de 61 caractères utilisée pour authentifier votre [!DNL Google Cloud Storage] compte vers Plateforme. |
| `secretAccessKey` | Chaîne codée en base de 40 caractères utilisée pour authentifier votre [!DNL Google Cloud Storage] compte vers Plateforme. |

Pour plus d’informations sur ces valeurs, consultez la section [Clés HMAC de stockage Google Cloud](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guide. Pour connaître les étapes permettant de générer votre propre ID de clé d’accès et votre clé d’accès secret, consultez la section [[!DNL Google Cloud Storage] présentation](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Utilisation des API de plate-forme

Pour plus d’informations sur la manière d’effectuer des appels vers les API de plate-forme, consultez le guide sur [prise en main des API de plate-forme](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et la plate-forme, y compris les informations d&#39;identification de votre source, l&#39;état actuel de la connexion et votre ID de connexion de base unique. L’ID de connexion de base vous permet d’explorer et de parcourir les fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez assimiler, y compris des informations concernant leurs types et formats de données.

Pour créer un ID de connexion de base, effectuez une demande de POST à l’adresse `/connections` point de terminaison lors de la fourniture de votre [!DNL Google Cloud Storage] les informations d&#39;identification d&#39;authentification dans le cadre des paramètres de demande.

**Format d’API**

```http
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour [!DNL Google Cloud Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage connection",
        "description": "Connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
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
| `auth.params.accessKeyId` | L’ID de clé d’accès associé à votre [!DNL Google Cloud Storage] compte. |
| `auth.params.secretAccessKey` | La clé d’accès secret associée à votre [!DNL Google Cloud Storage] compte. |
| `connectionSpec.id` | Le [!DNL Google Cloud Storage] ID de spécification de connexion : `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet ID est nécessaire pour explorer vos données de stockage dans le cloud dans le didacticiel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un fichier [!DNL Google Cloud Storage] la connexion à l’aide d’API et d’un ID unique a été obtenue dans le corps de la réponse. Vous pouvez utiliser cet ID de connexion pour [exploration des sites de stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
