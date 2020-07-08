---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur Requête Service
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 9%

---


# Requêtes

## Exemples d’appels d’API

Les sections suivantes décrivent les appels que vous pouvez effectuer à l’aide du `/queries` point de terminaison dans l’API Requête Service. Chaque appel comprend le format général de l’API, un exemple de requête indiquant les en-têtes requis et un exemple de réponse.

### Récupérer une liste de requêtes

You can retrieve a list of all queries for your IMS Organization by making a GET request to the `/queries` endpoint.

**Format d’API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}` : (*facultatif*) paramètres ajoutés au chemin de requête configurant les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous.

**Paramètres de requête**

Voici une liste des paramètres de requête disponibles pour la liste des requêtes. Tous ces paramètres sont facultatifs. L&#39;appel à ce point de terminaison sans paramètre récupère toutes les requêtes disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Indique le champ selon lequel les résultats doivent être commandés. Les champs pris en charge sont `created` et `updated`. Par exemple, `orderby=created` triera les résultats par ordre croissant. Ajouter un `-` avant création (`orderby=-created`) triera les éléments par création dans l’ordre décroissant. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Default value: 20*) |
| `start` | Décale la liste de réponse à l’aide d’une numérotation à base zéro. Par exemple, `start=2` renvoie une liste commençant à partir de la troisième requête répertoriée. (*Default value: 0*) |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être une séquence d’échappement HTML. Les virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs pris en charge sont `created`, `updated`, `state`et `id`. La liste des opérateurs pris en charge est `>` (supérieure à), `<` (inférieure à), `>=` (supérieure ou égale à), `<=` (inférieure ou égale à), `==` (égale à), `!=` (non égale à) et `~` (contient). Par exemple, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` renvoie toutes les requêtes avec l’ID spécifié. |
| `excludeSoftDeleted` | Indique s’il convient d’inclure une requête qui a été supprimée de manière souple. Par exemple, `excludeSoftDeleted=false` inclura **** des requêtes supprimées à l’écran. (*Boolean, valeur par défaut : true*) |
| `excludeHidden` | Indique si les requêtes pilotées par des utilisateurs non-utilisateurs doivent être affichées. La définition de cette valeur sur false **inclut** les requêtes non pilotées par l’utilisateur, telles que les définitions CURSOR, FETCH ou les requêtes de métadonnées. (*Boolean, valeur par défaut : true*) |

**Requête**

La requête suivante récupère la dernière requête créée pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec une liste de requêtes pour l’organisation IMS spécifiée en tant que JSON. La réponse suivante renvoie la dernière requête créée pour votre organisation IMS.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### Création d’une requête

You can create a new query by making a POST request to the `/queries` endpoint.

**Format d’API**

```http
POST /queries
```

**Requête**

La requête suivante crée une nouvelle requête, configurée par les valeurs fournies dans la charge utile :

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query"
        "description": "Sample Description"
    }  
```

| Propriété | Description |
| -------- | ----------- |
| `dbName` | Nom de la base de données pour laquelle vous créez une requête SQL. |
| `sql` | requête SQL que vous souhaitez créer. |
| `name` | Nom de votre requête SQL. |
| `description` | Description de votre requête SQL. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec les détails de votre nouvelle requête créée. Une fois la requête activée et exécutée correctement, elle `state` passe de `SUBMITTED` à `SUCCESS`.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.cancel` pour [annuler la requête](#cancel-a-query)créée.

### Récupération d’une requête par ID

You can retrieve detailed information about a specific query by making a GET request to the `/queries` endpoint and providing the query&#39;s `id` value in the request path.

**Format d’API**

```http
GET /queries/{QUERY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_ID}` | The `id` value of the query you want to retrieve. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur la requête spécifiée.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.cancel` pour [annuler la requête](#cancel-a-query)créée.

### Annuler une requête

You can request to delete a specified query by making a PATCH request to the `/queries` endpoint and providing the query&#39;s `id` value in the request path.

**Format d’API**

```http
PATCH /queries/{QUERY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_ID}` | Valeur `id` de la requête à annuler. |


**Requête**

Cette requête d’API utilise la syntaxe de correctif JSON pour sa charge utile. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document de base de l’API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `op` | Pour annuler la requête, vous devez définir le paramètre op avec la valeur `cancel `. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant :

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
