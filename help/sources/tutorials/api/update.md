---
keywords: Experience Platform;home;popular topics; flow service; update connections
solution: Experience Platform
title: Mise à jour des informations de connexion à l’aide de l’API du service de flux
topic: overview
description: Ce didacticiel décrit les étapes de mise à jour des informations de connexion, y compris leur nom, leur description et leurs informations d’identification à l’aide de l’API du service de flux.
translation-type: tm+mt
source-git-commit: 1292e39ea7682b839ea75dd069ce32f1591345b8
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 13%

---


# Mise à jour des informations de connexion à l’aide de l’API du service de flux

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel décrit les étapes de mise à jour des informations de connexion, y compris le nom, la description et les informations d’identification à l’aide du [!DNL Flow Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce didacticiel nécessite que vous disposiez d’un ID de connexion valide. Si vous ne disposez pas d’un ID de connexion valide, sélectionnez le connecteur de votre choix dans l’aperçu [des](../../home.md) sources et suivez les étapes décrites avant de tenter ce didacticiel.

Ce didacticiel nécessite également une bonne compréhension des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully update your connection&#39;s information using the [!DNL Flow Service] API.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Rechercher les détails de connexion

>[!NOTE]
>Ce didacticiel utilise le connecteur [source](../../connectors/crm/salesforce.md) Salesforce comme exemple, mais les étapes décrites s&#39;appliquent à n&#39;importe lequel des connecteurs [source](../../home.md)disponibles.

La première étape de la mise à jour des informations de connexion consiste à récupérer les détails de connexion à l’aide de votre identifiant de connexion.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur unique `id` de la connexion que vous souhaitez récupérer. |

**Requête**

L&#39;exemple suivant récupère des informations concernant votre ID de connexion.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails actuels de votre connexion, y compris ses informations d&#39;identification, son identifiant unique (`id`) et sa version.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## Mettre à jour la connexion

Une fois que vous disposez d’un ID de connexion existant, exécutez une requête de PATCH sur l’ [!DNL Flow Service] API.

>[!IMPORTANT]
>Une demande de PATCH nécessite l’utilisation de l’ `If-Match` en-tête. La valeur de cet en-tête est la version unique de votre connexion.

**Format d’API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur unique `id` de la connexion à mettre à jour. |

**Requête**

La requête suivante fournit de nouvelles informations pour mettre à jour votre connexion.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Paramètre | Description |
| --------- | ----------- |
| `op` | Appel d&#39;opération utilisé pour définir l&#39;action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace`et `remove`. |
| `path` | Chemin d’accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion et une balise mise à jour.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Rechercher les détails de connexion mis à jour

Vous pouvez récupérer le même ID de connexion que celui que vous avez mis à jour pour voir les modifications que vous avez apportées en adressant une demande de GET à l’ [!DNL Flow Service] API.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur unique `id` de la connexion que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère des informations mises à jour concernant votre ID de connexion.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails mis à jour de votre ID de connexion, y compris son nouveau nom, sa description et sa nouvelle version.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1598038319627,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "Test salesforce connection",
            "description": "A test salesforce connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{NEW_SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "salesforce-connector-username"
                }
            },
            "version": "\"3600e378-0000-0200-0000-5f40212f0000\"",
            "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
        }
    ]
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez mis à jour les informations d’identification et les informations associées à votre connexion à l’aide de l’ [!DNL Flow Service] API. Pour plus d’informations sur l’utilisation des connecteurs de source, voir l’aperçu [des](../../home.md)sources.
