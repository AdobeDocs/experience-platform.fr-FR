---
title: Créer une connexion de base Microsoft Dynamics à l’aide de l’API Flow Service
description: Découvrez comment connecter Experience Platform à un compte Microsoft Dynamics à l’aide de l’API Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 14%

---

# Connexion de [!DNL Microsoft Dynamics] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Lisez ce guide pour savoir comment connecter votre source [!DNL Microsoft Dynamics] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de connecter Experience Platform à un compte Dynamics à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL Dynamics], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB  Authentification de base ]

| Informations d’identification | Description |
| --- | --- |
| `serviceUri` | URL du service de votre instance [!DNL Dynamics]. |
| `username` | Nom d’utilisateur de votre compte utilisateur [!DNL Dynamics]. |
| `password` | Mot de passe de votre compte [!DNL Dynamics]. |

>[!TAB Authentification principale et par clé du service]

| Informations d’identification | Description |
| --- | --- |
| `servicePrincipalId` | Identifiant client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation du principal de service et de l’authentification par clé. |
| `servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation du principal de service et de l’authentification par clé. |

>[!ENDTABS]

Pour plus d’informations sur la prise en main, consultez [ce [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Créer une connexion de base

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d’authentification d’une connexion de base [!DNL Dynamics]. Pour modifier le type d’authentification, vous devez créer une connexion de base.

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Dynamics] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Authentification de base ]

Pour créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification de base, envoyez une requête POST à l’API [!DNL Flow Service] tout en fournissant des valeurs pour les `serviceUri`, `username` et `password` de votre connexion.

**Requête**

La requête suivante crée une connexion de base pour une source [!DNL Dynamics] à l’aide de l’authentification de base.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.serviceUri` | URI de service associé à votre instance [!DNL Dynamics]. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Dynamics]. |
| `auth.params.password` | Mot de passe associé à votre compte [!DNL Dynamics]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Dynamics] : `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

+++

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Sélectionner pour afficher l’exemple de réponse

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Authentification basée sur la clé principale du service]

Pour créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification par clé de service principale, envoyez une requête POST à l’API [!DNL Flow Service] tout en fournissant des valeurs pour les `serviceUri`, `servicePrincipalId` et `servicePrincipalKey` de votre connexion.

**Requête**

La requête suivante crée une connexion de base pour une source [!DNL Dynamics] à l’aide de l’authentification par clé principale du service de base.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.serviceUri` | URI de service associé à votre instance [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | Identifiant client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation du principal de service et de l’authentification par clé. |
| `auth.params.servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation du principal de service et de l’authentification par clé. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Dynamics] : `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

+++

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant unique (`id`).

+++Sélectionner pour afficher l’exemple de réponse

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## Explorer vos tableaux de données

Pour explorer vos tableaux de données [!DNL Dynamics], envoyez une requête GET au point d’entrée `/connections/{BASE_CONNECTION_ID}/explore` et indiquez votre identifiant de connexion de base dans les paramètres de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètres de requête | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de la connexion de base. Utilisez cet identifiant pour explorer le contenu et la structure de votre source. |

**Requête**

La requête suivante récupère la liste des tables et des vues disponibles pour une source de [!DNL Dynamics] avec l’identifiant de connexion de base : `dd668808-25da-493f-8782-f3433b976d1e`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie le répertoire des tables et des vues [!DNL Dynamics] au niveau racine.

+++Sélectionner pour afficher l’exemple de réponse

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++

### Utilisation de la clé primaire pour optimiser l’exploration des données

>[!NOTE]
>
>Vous pouvez uniquement utiliser des attributs autres que de recherche lors de l’utilisation de l’approche par clé primaire de l’optimisation.

Vous pouvez optimiser vos requêtes d’exploration en fournissant des `primaryKey` dans le cadre de vos paramètres de requête. Vous devez spécifier la clé primaire de la table [!DNL Dynamics] lors de l’inclusion de `primaryKey` en tant que paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?preview=true&object={OBJECT}&objectType={OBJECT_TYPE}&previewCount=10&primaryKey={PRIMARY_KEY}
```

| Paramètres de requête | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de la connexion de base. Utilisez cet identifiant pour explorer le contenu et la structure de votre source. |
| `preview` | Valeur booléenne qui active la prévisualisation des données. |
| `{OBJECT}` | Objet [!DNL Dynamics] à explorer. |
| `{OBJECT_TYPE}` | Type de l’objet. |
| `previewCount` | Restriction qui limite l’aperçu renvoyé à un certain nombre d’enregistrements uniquement. |
| `{PRIMARY_KEY}` | Clé primaire de la table que vous récupérez pour prévisualisation. |

**Requête**

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform-stage.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?preview=true&object=lead&objectType=table&previewCount=10&primaryKey=leadid' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

## Examiner la structure d’un tableau

Pour examiner la structure d’une table spécifique, envoyez une requête GET à `/connections/{BASE_CONNECTION_ID}/explore` et indiquez le chemin d’accès à la table spécifique comme paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| Paramètre de requête | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de la connexion de base. Utilisez cet identifiant pour explorer le contenu et la structure de votre source. |
| `{TABLE_PATH}` | Chemin d’accès à la table spécifique que vous souhaitez explorer. |

**Requête**

La requête suivante récupère la structure et le contenu d’une table [!DNL Dynamics] avec le chemin `workflowdependency`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie le contenu du chemin `workflowdependency`.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## Examiner la structure d’une vue

Dans [!DNL Dynamics], une vue fait référence aux colonnes à afficher, à la largeur de chaque colonne, au système par défaut dans lequel une liste d&#39;enregistrements est triée et aux filtres par défaut appliqués pour limiter les enregistrements qui apparaîtront dans la liste.

Pour inspecter la structure d’une vue, envoyez une requête GET à `/connections/{BASE_CONNECTION_ID}/explore` et spécifiez le chemin de vue dans vos paramètres de requête. En outre, vous devez spécifier `objectType` comme `view`.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| Paramètre de requête | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de la connexion de base. Utilisez cet identifiant pour explorer le contenu et la structure de votre source. |
| `{VIEW_PATH}` | Chemin d&#39;accès à la vue à inspecter. |

**Requête**

La requête suivante récupère `accountView1`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie la structure de l’`accountView1`.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## Aperçu de la vue du type d’entité

Pour prévisualiser le contenu d’une vue, envoyez une requête GET à `/connections/{BASE_CONNECTION_ID}/explore` et incluez le chemin de vue ainsi que la `preview=true` dans vos paramètres de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| Paramètre de requête | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de la connexion de base. Utilisez cet identifiant pour explorer le contenu et la structure de votre source. |
| `{VIEW_PATH}` | Chemin d&#39;accès à la vue à inspecter. |


**Requête**

La requête suivante prévisualise le contenu de `accountView1`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie le contenu de `accountView1`.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## Créer une connexion source pour ingérer la vue

Pour créer une connexion source et ingérer une vue, envoyez une requête POST au point d’entrée `/sourceConnections`, indiquez le nom de la table et spécifiez les `entityType` comme `view` dans le corps de la requête.

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

La requête suivante crée une connexion source [!DNL Dynamics] et ingère des vues.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**Réponse**

Une réponse réussie renvoie l’identifiant de connexion source nouvellement généré et son etag correspondant.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

### Utilisation de la clé primaire pour optimiser votre flux de données

Vous pouvez également optimiser votre flux de données [!DNL Dynamics] en spécifiant la clé primaire dans les paramètres du corps de la requête.

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

La requête suivante crée une connexion source [!DNL Dynamics] lors de la spécification de la clé primaire comme `contactid`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular"
      },
      "params": {
          "tableName": "contact",
          "primaryKey": "contactid"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `baseConnectionId` | Identifiant de la connexion de base. |
| `data.format` | Format des données. |
| `params.tableName` | Nom de la table en [!DNL Dynamics]. |
| `params.primaryKey` | Clé primaire de la table qui optimisera les requêtes. |
| `connectionSpec.id` | Identifiant de spécification de connexion correspondant à la source [!DNL Dynamics]. |

+++

**Réponse**

Une réponse réussie renvoie l’identifiant de connexion source nouvellement généré et son etag correspondant.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++


## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Microsoft Dynamics] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créer un flux de données pour importer des données CRM dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/crm.md)
