---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;guide api;requêtes;requête;service de requête ;
solution: Experience Platform
title: Point de terminaison de l’API de requêtes
description: Les sections suivantes passent en revue les appels que vous pouvez effectuer à l’aide du point de terminaison /query de l’API Query Service.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 94%

---

# Point de terminaison des requêtes

## Exemples d’appels API

Les sections suivantes passent en revue les appels que vous pouvez effectuer à l’aide du point de terminaison `/queries` dans l’API [!DNL Query Service] Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupération d’une liste de requêtes

Vous pouvez obtenir une liste de toutes les requêtes de votre organisation IMS en effectuant une requête GET vers le point de terminaison `/queries`.

**Format d’API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}` : (*facultatif*) paramètres ajoutés au chemin de requête configurant les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous.

**Paramètres de requête**

Vous trouverez ci-dessous une liste des paramètres de requête disponibles pour répertorier les requêtes. Tous ces paramètres sont facultatifs. En effectuant un appel vers ce point de terminaison sans paramètres, vous récupérerez toutes les requêtes disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Spécifie le champ de référence pour le tri des résultats. Les champs `created` et `updated` sont pris en charge. Par exemple, `orderby=created` triera les résultats par ordre croissant de création. L’ajout d’un `-` devant created (`orderby=-created`) triera les éléments par ordre décroissant de création. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Valeur par défaut : 20*) |
| `start` | Décale la liste de réponses à l’aide d’une numérotation à partir de zéro. Par exemple, `start=2` renvoie une liste commençant par la troisième requête répertoriée. (*Valeur par défaut : 0*) |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être précédés d’une séquence d’échappement HTML. Des virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs `created`, `updated`, `state` et `id` sont pris en charge. Les opérateurs `>` (supérieur à), `<` (inférieur à), `>=` (supérieur ou égal à), `<=` (inférieur ou égal à), `==` (égal à), `!=` (différent de) et `~` (contient). Par exemple, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` renvoie toutes les requêtes avec l’identifiant spécifié. |
| `excludeSoftDeleted` | Indique s’il faut inclure une requête ayant été supprimée de manière réversible. Par exemple, `excludeSoftDeleted=false` inclut **des** requêtes supprimées de manière réversible. (*booléenne, valeur par défaut : true*) |
| `excludeHidden` | Indique si les requêtes formulées par l’utilisateur doivent être affichées. Si cette valeur est définie sur false, cela **inclut** les requêtes qui ne sont pas formulées par l’utilisateur telles que les définitions CURSOR, FETCH ou les requêtes de métadonnées. (*booléenne, valeur par défaut : true*) |

**Requête**

La requête suivante renvoie la dernière requête créée pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de requêtes pour l’organisation IMS spécifiée sous JSON. La réponse suivante renvoie la dernière requête créée pour votre organisation IMS.

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

Vous pouvez créer une requête en effectuant une requête POST vers le point de terminaison `/queries`.

**Format d’API**

```http
POST /queries
```

**Requête**

La requête suivante crée une requête configurée en fonction des valeurs fournies dans le payload :

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| Propriété | Description |
| -------- | ----------- |
| `dbName` | Nom de la base de données pour laquelle vous créez une requête SQL. |
| `sql` | La requête SQL que vous souhaitez créer. |
| `name` | Nom de la requête SQL. |
| `description` | Description de la requête SQL. |

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec les détails de la requête que vous venez de créer. Une fois que la requête est activée et s’exécute correctement, le `state` passe de `SUBMITTED` à `SUCCESS`.

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
>Vous pouvez utiliser la valeur de `_links.cancel` pour [annuler la requête créée](#cancel-a-query).

### Récupération d’une requête par identifiant

Vous pouvez obtenir des informations détaillées sur une requête spécifique en effectuant une requête GET vers le point de terminaison `/queries` et en indiquant la valeur `id` de la requête dans le chemin d’accès à la requête.

**Format d’API**

```http
GET /queries/{QUERY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_ID}` | La valeur `id` de la requête que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la requête spécifiée.

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
>Vous pouvez utiliser la valeur de `_links.cancel` pour [annuler la requête créée](#cancel-a-query).

### Annulation d’une requête

Vous pouvez demander la suppression d’une requête spécifiée en effectuant une requête PATCH vers le point de terminaison `/queries` et en fournissant la valeur `id` de la requête dans le chemin d’accès de la requête.

**Format d’API**

```http
PATCH /queries/{QUERY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_ID}` | La valeur `id` de la requête que vous souhaitez annuler. |


**Requête**

Cette requête API utilise la syntaxe du correctif JSON pour son payload. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document principes de base des API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec le message suivant :

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
