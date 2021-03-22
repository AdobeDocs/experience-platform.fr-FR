---
keywords: Experience Platform ; accueil ; rubriques populaires ; Enregistrement Google Cloud ; enregistrement Google Cloud ; google ; Google ; Google
solution: Experience Platform
title: Création d’une connexion à la source d’Enregistrement Google Cloud à l’aide de l’API du service de flux
topic: aperçu
type: Tutoriel
description: Découvrez comment connecter Adobe Experience Platform à un compte d’Enregistrement Google Cloud à l’aide de l’API de service de flux.
translation-type: tm+mt
source-git-commit: f6a63ca1e21b3c3f6a55574f31fdf04038b7e5c4
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 24%

---


# Créez une connexion source [!DNL Google Cloud Storage] à l’aide de l’API [!DNL Flow Service].

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider dans les étapes de connexion de [!DNL Experience Platform] à un compte [!DNL Google Cloud Storage].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à un compte d’Enregistrement Google Cloud à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à votre compte [!DNL Google Cloud Storage], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| ID de clé d&#39;accès | Chaîne alphanumérique de 61 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] sur la plateforme. |
| Clé d&#39;accès secrète | Chaîne codée en base de 40 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] sur Plateforme. |

Pour plus d’informations sur ces valeurs, voir le guide [Cloud Enregistrement HMAC keys](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour obtenir des instructions sur la génération de votre propre ID de clé d&#39;accès et de votre clé d&#39;accès secret, consultez la section [[!DNL Google Cloud Storage] présentation](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte [!DNL Google Cloud Storage], car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion [!DNL Google Cloud Storage], l&#39;identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL Google Cloud Storage] est `32e8f412-cdf7-464c-9885-78184cb113fd`.

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
| `auth.params.accessKeyId` | ID de clé d&#39;accès associé à votre compte [!DNL Google Cloud Storage]. |
| `auth.params.secretAccessKey` | Clé d&#39;accès secrète associée à votre compte [!DNL Google Cloud Storage]. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Google Cloud Storage] : `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données d’enregistrement de cloud dans le didacticiel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion [!DNL Google Cloud Storage] à l&#39;aide d&#39;API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet ID de connexion pour [explorer les enregistrements de cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md) ou [assimiler des données Parquet à l’aide de l’API Flow Service](../../cloud-storage-parquet.md).