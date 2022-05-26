---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Création d’un flux de données pour Zendesk à l’aide de l’API Flow Service
topic-legacy: tutorial
description: Découvrez comment connecter Adobe Experience Platform à Zendesk à l’aide de l’API Flow Service.
exl-id: 3e00e375-c6f8-407c-bded-7357ccf3482e
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 78%

---

# (Version bêta) Création d’un flux de données pour [!DNL Zendesk] en utilisant la variable [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL Zendesk] La source est en version bêta. Voir [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Le tutoriel suivant vous guide à travers les étapes de création dʼune connexion source et dʼun flux de données pour importer des données [!DNL Zendesk] dans Platform à l’aide de lʼ[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources ](../../../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Environnements de test](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Zendesk] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour accéder à [!DNL Zendesk] sur Platform, vous devez fournir des valeurs pour les informations d’identification suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `host` | Domaine unique spécifique à votre compte créé lors du processus d’enregistrement. | `https://yoursubdomain.zendesk.com` |
| `accessToken` | Jeton d’API Zendesk. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Pour plus d’informations sur l’authentification [!DNL Zendesk] source, voir [[!DNL Zendesk] présentation de la source](../../../../connectors/customer-success/zendesk.md).

## Connexion [!DNL Zendesk] vers Platform à l’aide de [!DNL Flow Service] API

Le tutoriel suivant vous guide tout au long des étapes de création d’un [!DNL Zendesk] connexion source et créer un flux de données à importer [!DNL Zendesk] données vers Platform à l’aide de la fonction [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Créer une connexion de base {#base-connection}

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL Zendesk] informations d’identification d’authentification dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Zendesk] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk base connection",
        "description": "Zendesk base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "0a27232b-2c6e-4396-b8c6-c9fc24e37ba4",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth2 Refresh Code",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion de base. Assurez-vous que le nom de votre connexion de base est explicite, car vous pouvez lʼutiliser pour rechercher des informations sur votre connexion de base. |
| `description` | Une valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `connectionSpec.id` | Identifiant de spécification de connexion de votre source. Cet identifiant peut être récupéré une fois que votre source est enregistrée et approuvée par le biais de l’API [!DNL Flow Service]. |
| `auth.specName` | Type d’authentification que vous utilisez pour authentifier votre source sur Platform. |
| `auth.params.` | Contient les informations d’identification requises pour authentifier votre source. |
| `auth.params.host` | Domaine unique spécifique à votre compte créé lors du processus d’enregistrement. Le format du sous-domaine est `https://yoursubdomain.zendesk.com`. |
| `auth.params.accessToken` | Jeton d’accès correspondant utilisé pour authentifier la source. Ceci est requis pour l’authentification basée sur OAuth. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de base, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer la structure de fichiers et le contenu de votre source à l’étape suivante.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Explorer votre source {#explore}

À l’aide de l’identifiant de connexion de base généré à l’étape précédente, vous pouvez explorer les fichiers et répertoires en exécutant des requêtes GET.
Utilisez les appels suivants pour trouver le chemin d’accès au fichier que vous souhaitez importer. [!DNL Platform]:

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Lors de l’exécution de requêtes GET pour explorer la structure et le contenu des fichiers de votre source, vous devez inclure les paramètres de requête répertoriés dans le tableau ci-dessous :


| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base généré à l’étape précédente. |
| `objectType=rest` | Type d’objet que vous souhaitez explorer. Actuellement, cette valeur est toujours définie sur `rest`. |
| `{OBJECT}` | Ce paramètre est requis uniquement lors de l’affichage d’un répertoire spécifique. Sa valeur représente le chemin dʼaccès au répertoire que vous souhaitez explorer. |
| `fileType=json` | Type de fichier du fichier que vous souhaitez importer dans Platform. Actuellement, `json` est le seul type de fichier pris en charge. |
| `{PREVIEW}` | Valeur booléenne qui définit si le contenu de la connexion prend en charge la prévisualisation. |
| `{SOURCE_PARAMS}` | Définit les paramètres du fichier source que vous souhaitez importer dans Platform. Pour récupérer le type de format accepté pour `{SOURCE_PARAMS}`, vous devez coder l’intégralité de la chaîne `parameter` en base64. Dans l’exemple ci-dessous, `"{}"` encodé en base64 équivaut à `e30`. |


**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure du fichier interrogé. Dans l’exemple ci-dessous, dans la fonction ``data[]`` payload, un seul enregistrement s’affiche, mais il peut y avoir plusieurs enregistrements.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "result": {
                "type": "object",
                "properties": {
                    "organization_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "external_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "role_type": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "custom_role_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "default_group_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "phone": {
                        "type": "string"
                    },
                    "shared_phone_number": {
                        "type": "boolean"
                    },
                    "alias": {
                        "type": "string"
                    },
                    "last_login_at": {
                        "type": "string"
                    },
                    "signature": {
                        "type": "string"
                    },
                    "details": {
                        "type": "string"
                    },
                    "notes": {
                        "type": "string"
                    },
                    "photo": {
                        "type": "string",
                        "media": {
                            "binaryEncoding": "base64",
                            "type": "image/png"
                        }
                    },
                    "active": {
                        "type": "boolean"
                    },
                    "created_at": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    },
                    "iana_time_zone": {
                        "type": "string"
                    },
                    "id": {
                        "type": "integer"
                    },
                    "locale": {
                        "type": "string"
                    },
                    "locale_id": {
                        "type": "integer"
                    },
                    "moderator": {
                        "type": "boolean"
                    },
                    "name": {
                        "type": "string"
                    },
                    "only_private_comments": {
                        "type": "boolean"
                    },
                    "report_csv": {
                        "type": "boolean"
                    },
                    "restricted_agent": {
                        "type": "boolean"
                    },
                    "result_type": {
                        "type": "string"
                    },
                    "role": {
                        "type": "integer"
                    },
                    "shared": {
                        "type": "boolean"
                    },
                    "shared_agent": {
                        "type": "boolean"
                    },
                    "suspended": {
                        "type": "boolean"
                    },
                    "ticket_restriction": {
                        "type": "string"
                    },
                    "time_zone": {
                        "type": "string"
                    },
                    "two_factor_auth_enabled": {
                        "type": "boolean"
                    },
                    "updated_at": {
                        "type": "string"
                    },
                    "url": {
                        "type": "string"
                    },
                    "verified": {
                        "type": "boolean"
                    },
                    "tags": {
                        "type": "array",
                        "items": {
                            "type": "string"
                        }
                    }
                }
            }
        }
    },
    "data": [
        {
            "result": {
                "id": 6106699702801,
                "url": "https://d3v-dxinfosys.zendesk.com/api/v2/users/6106699702801.json",
                "name": "test",
                "email": "test@org.com",
                "created_at": "2022-05-13T08:04:22Z",
                "updated_at": "2022-05-13T08:04:22Z",
                "time_zone": "Asia/Kolkata",
                "iana_time_zone": "Asia/Kolkata",
                "locale_id": 1,
                "locale": "en-US",
                "role": "end-user",
                "verified": false,
                "active": true,
                "shared": false,
                "shared_agent": false,
                "two_factor_auth_enabled": false,
                "moderator": false,
                "ticket_restriction": "requested",
                "only_private_comments": false,
                "restricted_agent": true,
                "suspended": false,
                "report_csv": false,
                "result_type": "user"
            }
        }
    ]
}
```

### Créer une connexion source {#source-connection}

Vous pouvez créer une connexion source en effectuant une requête POST à l’API [!DNL Flow Service]. Une connexion source se compose d’un identifiant de connexion, d’un chemin d’accès au fichier de données source et d’un identifiant de spécification de connexion.

**Format d’API**

```https
POST /sourceConnections
```

**Requête**

La requête suivante crée une connexion source pour [!DNL Zendesk] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk Source Connection",
        "description": "Zendesk Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "0a27232b-2c6e-4396-b8c6-c9fc24e37ba4",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {}
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion source. |
| `baseConnectionId` | Identifiant de connexion de base de [!DNL Zendesk]. Cet identifiant a été généré lors d’une étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion correspondant à votre source. |
| `data.format` | Format des données [!DNL Zendesk] que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

## Créer un schéma XDM cible {#target-schema}

Pour que les données sources soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Le schéma cible est ensuite utilisé pour créer un jeu de données Platform contenant les données sources.

Un schéma XDM cible peut être créé en adressant une requête POST à l’[API Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, suivez le tutoriel sur la [création d’un schéma à l’aide de l’API](../../../../../xdm/api/schemas.md).

### Créer un jeu de données cible {#target-dataset}

Un jeu de données cible peut être créé en adressant une requête POST à l’[API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) et en fournissant l’identifiant du schéma cible dans la payload.

Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, suivez le tutoriel sur la [création d’un jeu de données à l’aide de l’API](../../../../../catalog/api/create-dataset.md).

### Créer une connexion cible {#target-connection}

Une connexion cible représente la connexion à la destination vers laquelle les données ingérées doivent être stockées. Pour créer une connexion cible, vous devez fournir l’identifiant de spécification de connexion fixe qui correspond au lac de données. Cet identifiant est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma cible d’un jeu de données cible et de l’identifiant de spécification de connexion au lac de données. À lʼaide de ces identifiants, vous pouvez créer une connexion cible à l’aide de l’API [!DNL Flow Service] pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

```https
POST /targetConnections
```

**Requête**

La requête suivante crée une connexion cible pour Zendesk :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk Target Connection",
        "description": "Zendesk Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "624bf42e16519d19496e3f67"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom de la connexion cible. Assurez-vous que le nom de votre connexion cible est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion cible. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion cible. |
| `connectionSpec.id` | L’identifiant de spécification de connexion qui correspond au lac de données. Cet ID fixe est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Format des données [!DNL Zendesk] que vous souhaitez importer dans Platform. |
| `params.dataSetId` | Identifiant du jeu de données cible récupéré lors d’une étape précédente. |


**Réponse**

Une réponse réussie renvoie l’identifiant unique de la nouvelle connexion cible (`id`). Cet identifiant est requis aux étapes suivantes.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Créer un mappage {#mapping}

Pour que les données sources soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible se rattache. Pour ce faire, il vous suffit d’adresser une requête de POST à [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) avec des mappages de données définis dans le payload de la requête.

**Format d’API**

```http
POST /conversion/mappingSets
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.id",
                "destination": "_extconndev.id",
                "name": "id",
                "description": "Zendesk"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.external_id",
                "destination": "_extconndev.external_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.role_type",
                "destination": "_extconndev.role_type"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.custom_role_id",
                "destination": "_extconndev.custom_role_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.default_group_id",
                "destination": "_extconndev.default_group_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.phone",
                "destination": "_extconndev.phone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared_phone_number",
                "destination": "_extconndev.shared_phone_number"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.verified",
                "destination": "_extconndev.verified"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.alias",
                "destination": "_extconndev.alias"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.last_login_at",
                "destination": "_extconndev.last_login_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.signature",
                "destination": "_extconndev.signature"
            },        {
                "sourceType": "ATTRIBUTE",
                "source": "result.details",
                "destination": "_extconndev.details"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.notes",
                "destination": "_extconndev.notes"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.active",
                "destination": "_extconndev.active"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.created_at",
                "destination": "_extconndev.created_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.email",
                "destination": "_extconndev.email"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.iana_time_zone",
                "destination": "_extconndev.iana_time_zone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.organization_id",
                "destination": "_extconndev.organization_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.locale",
                "destination": "_extconndev.locale"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.locale_id",
                "destination": "_extconndev.locale_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.moderator",
                "destination": "_extconndev.moderator"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.name",
                "destination": "_extconndev.name"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.only_private_comments",
                "destination": "_extconndev.only_private_comments"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.report_csv",
                "destination": "_extconndev.report_csv"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.restricted_agent",
                "destination": "_extconndev.restricted_agent"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.result_type",
                "destination": "_extconndev.result_type"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.role",
                "destination": "_extconndev.role"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared",
                "destination": "_extconndev.shared"
            },        {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared_agent",
                "destination": "_extconndev.shared_agent"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.time_zone",
                "destination": "_extconndev.time_zone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.two_factor_auth_enabled",
                "destination": "_extconndev.two_factor_auth_enabled"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.suspended",
                "destination": "_extconndev.suspended"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.updated_at",
                "destination": "_extconndev.updated_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.url",
                "destination": "_extconndev.url"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.verified",
                "destination": "_extconndev.verified"
            }
        ]
    }'
```

| Propriété | Description |
| --- | --- |
| `xdmSchema` | Identifiant du [schéma XDM cible](#target-schema) généré lors d’une étape précédente. |
| `mappings.destinationXdmPath` | Chemin XDM de destination vers lequel l’attribut source est mappé. |
| `mappings.sourceAttribute` | Attribut source qui doit être mappé à un chemin XDM de destination. |
| `mappings.identity` | Valeur booléenne qui indique si le jeu de mappage sera marqué pour [!DNL Identity Service]. |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Cette valeur est requise lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Créer un flux {#flow}

La dernière étape pour apporter des données de Zendesk vers Platform consiste à créer un flux de données. Vous disposez à présent des valeurs requises suivantes :

* [ID de connexion source](#source-connection)
* [ID de connexion cible](#target-connection)
* [Identifiant de mappage](#mapping)

Un flux de données est chargé de planifier et de collecter les données provenant d’une source. Vous pouvez créer un flux de données en exécutant une requête POST et en fournissant les valeurs mentionnées précédemment dans la payload.

Pour planifier une ingestion, vous devez d’abord définir la valeur de l’heure de début en temps Unix en secondes. Vous devez ensuite définir la valeur de fréquence sur l’une des cinq options suivantes : `once`, `minute`, `hour`, `day` ou `week`. La valeur interval désigne toutefois la période entre deux ingestion consécutives, la création d’une ingestion unique ne nécessite pas de définition d’un intervalle. Pour toutes les autres fréquences, la valeur de l’intervalle doit être égale ou supérieure à `15`.


**Format d’API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk dataflow",
        "description": "Zendesk dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "246d052c-da4a-494a-937f-a0d17b1c6cf5"
        ],
        "targetConnectionIds": [
            "7c96c827-3ffd-460c-a573-e9558f72f263"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1625040887",
            "frequency": "minute",
            "interval": 15
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du flux de données. Assurez-vous que le nom de votre flux de données est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre flux de données. |
| `description` | Une valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre flux de données. |
| `flowSpec.id` | Identifiant de spécification de flux requis pour créer un flux de données. Cet ID fixe est `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Version correspondante de l’identifiant de spécification de flux. Cette valeur est définie par défaut sur `1.0`. |
| `sourceConnectionIds` | L’[identifiant de connexion source](#source-connection) généré lors d’une étape précédente. |
| `targetConnectionIds` | [Identifiant de connexion cible](#target-connection) généré lors d’une étape précédente. |
| `transformations` | Cette propriété contient les différentes transformations qui doivent être appliquées à vos données. Cette propriété est requise lors de l’importation de données non conformes à XDM dans Platform. |
| `transformations.name` | Nom attribué à la transformation. |
| `transformations.params.mappingId` | [Identifiant de mappage](#mapping) généré lors d’une étape précédente. |
| `transformations.params.mappingVersion` | Version correspondante de l’identifiant de mappage. Ce paramètre est défini par défaut sur `0`. |
| `scheduleParams.startTime` | Cette propriété contient des informations sur la planification de l’ingestion du flux de données. |
| `scheduleParams.frequency` | Fréquence de collecte des données par le flux de données. Les valeurs possibles sont les suivantes : `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un nombre entier non nul. L’intervalle n’est pas requis lorsque la fréquence est définie sur `once` et doit être supérieur ou égal à `15` pour d’autres valeurs de fréquence. |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du flux de données nouvellement créé. Vous pouvez utiliser cet identifiant pour surveiller, mettre à jour ou supprimer votre flux de données.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les exécutions du flux, le statut d’achèvement et les erreurs.

**Format d’API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**Requête**

La requête suivante récupère les spécifications d’un flux de données existant.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des informations concernant votre exécution de flux, notamment : la date de création, les connexions source et cible ainsi que l’identifiant unique de l’exécution de flux (`id`).

```json
{
    "items": [
        {
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
            "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| Propriété | Description |
| -------- | ----------- |
| `items` | Contient une seule payload de métadonnées associée à votre exécution de flux spécifique. |
| `metrics` | Définit les caractéristiques des données dans l’exécution du flux. |
| `activities` | Définit la manière dont les données sont transformées. |
| `durationSummary` | Définit les heures de début et de fin de l’exécution du flux. |
| `sizeSummary` | Définit le volume des données en octets. |
| `recordSummary` | Définit le nombre d’enregistrements des données. |
| `fileSummary` | Définit le nombre de fichiers des données. |
| `statusSummary` | Définit si l’exécution du flux est une réussite ou un échec. |

### Mettre à jour votre flux de données

Pour mettre à jour le planning d’exécution, le nom et la description de votre flux de données, envoyez une requête PATCH à l’API [!DNL Flow Service] et indiquez votre ID de flux, de version et du nouveau planning que vous souhaitez utiliser.

>[!IMPORTANT]
>
>L’en-tête `If-Match` est requis lors de l’exécution d’une requête PATCH. La valeur de cet en-tête est l’etag unique du flux de données que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

La requête suivante met à jour votre planning d’exécution de flux, ainsi que le nom et la description de votre flux de données.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "New dataflow name"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Updated dataflow description"
            }
        ]'
```

| Paramètre | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Chemin d’accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

### Supprimer le flux de données

À lʼaide dʼun identifiant de flux existant, vous pouvez supprimer un flux de données en adressant une requête DELETE à l’API [!DNL Flow Service].

**Format d’API**

```http
DELETE /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | Valeur `id` unique du flux de données à supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au flux de données. L’API renvoie une erreur HTTP 404 (Introuvable), indiquant que le flux de données a été supprimé.

### Mettre à jour votre connexion

Pour mettre à jour le nom, la description et les informations d’identification de votre connexion, envoyez une requête PATCH à l’API [!DNL Flow Service] et indiquez votre identifiant de connexion de base et de version ainsi que les nouvelles informations que vous souhaitez utiliser.

>[!IMPORTANT]
>
>L’en-tête `If-Match` est requis lors de l’exécution d’une requête PATCH. La valeur de cet en-tête est la version unique de la connexion que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Valeur `id` unique pour la connexion que vous souhaitez mettre à jour. |

**Requête**

La requête suivante fournit un nouveau nom, une nouvelle description et un nouveau jeu d’informations d’identification, avec lesquels vous allez mettre à jour votre connexion.

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
                "username": "{USERNAME}",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Zendesk connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "Zendesk connection"
        }
    ]'
```

| Paramètre | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Chemin d’accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion de base et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en fournissant votre identifiant de connexion.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

### Supprimer votre connexion

Une fois que vous disposez d’un identifiant de connexion de base existant, effectuez une requête DELETE à l’API [!DNL Flow Service].

**Format d’API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Valeur `id` unique de la connexion de base à supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) à la connexion.
