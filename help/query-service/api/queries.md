---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;guide d’api;requêtes;requête;Query service;
solution: Experience Platform
title: Point d’entrée de l’API Queries
description: Les sections suivantes décrivent les appels que vous pouvez effectuer à l’aide du point d’entrée /queries dans l’API Query Service.
role: Developer
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 48%

---

# Point d’entrée des requêtes

## Exemples d’appels API

Les sections suivantes décrivent les appels que vous pouvez effectuer à l’aide du point d’entrée `/queries` dans l’API [!DNL Query Service]. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupération d’une liste de requêtes

Vous pouvez récupérer une liste de toutes les requêtes pour votre organisation en envoyant une requête GET au point d’entrée `/queries`.

**Format d’API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}` : (*facultatif*) paramètres ajoutés au chemin de requête configurant les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous.

**Paramètres de requête**

Vous trouverez ci-dessous une liste des paramètres de requête disponibles pour répertorier les requêtes. Tous ces paramètres sont facultatifs. En effectuant un appel vers ce point d’entrée sans paramètres, vous récupérerez toutes les requêtes disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Spécifie le champ de référence pour le tri des résultats. Les champs `created` et `updated` sont pris en charge. Par exemple, `orderby=created` triera les résultats par ordre croissant de création. L’ajout d’un `-` devant created (`orderby=-created`) triera les éléments par ordre décroissant de création. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Valeur par défaut : 20*) |
| `start` | Spécifiez un horodatage au format ISO pour classer les résultats. Si aucune date de début n’est spécifiée, l’appel API renvoie d’abord la requête créée la plus ancienne, puis continue à répertorier les résultats les plus récents.Les horodatages ISO <br> permettent différents niveaux de granularité de la date et de l’heure. Les horodatages ISO de base prennent le format suivant : `2020-09-07` pour exprimer la date du 7 septembre 2020. Un exemple plus complexe est écrit comme `2022-11-05T08:15:30-05:00` et correspond au 5 novembre 2022, à 8 :15: 30, heure standard des États-Unis d’Amérique. Un fuseau horaire peut être fourni avec un décalage UTC et est désigné par le suffixe « Z » (`2020-01-01T01:01:01Z`). Si aucun fuseau horaire n’est fourni, la valeur par défaut est zéro. |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être précédés d’une séquence d’échappement HTML. Des virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs `created`, `updated`, `state` et `id` sont pris en charge. Les opérateurs `>` (supérieur à), `<` (inférieur à), `>=` (supérieur ou égal à), `<=` (inférieur ou égal à), `==` (égal à), `!=` (différent de) et `~` (contient). Par exemple, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` renvoie toutes les requêtes avec l’identifiant spécifié. |
| `excludeSoftDeleted` | Indique s’il faut inclure une requête ayant été supprimée de manière réversible. Par exemple, `excludeSoftDeleted=false` inclut **des** requêtes supprimées de manière réversible. (*booléenne, valeur par défaut : true*) |
| `excludeHidden` | Indique si les requêtes formulées par l’utilisateur doivent être affichées. Si cette valeur est définie sur false, cela **inclut** les requêtes qui ne sont pas formulées par l’utilisateur telles que les définitions CURSOR, FETCH ou les requêtes de métadonnées. (*booléenne, valeur par défaut : true*) |
| `isPrevLink` | Le paramètre de requête `isPrevLink` est utilisé pour la pagination. Les résultats de l’appel API sont triés à l’aide de leur horodatage `created` et de la propriété `orderby` . Lors de la navigation dans les pages de résultats, `isPrevLink` est défini sur true lors de la pagination vers l’arrière. L’ordre de la requête est inversé. Consultez les liens « suivant » et « précédent » à titre d’exemple. |

**Requête**

La requête suivante récupère la dernière requête créée pour votre organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de requêtes pour l’organisation spécifiée au format JSON. La réponse suivante renvoie la dernière requête créée pour votre organisation.

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

Vous pouvez créer une requête en effectuant une requête POST vers le point d’entrée `/queries`.

**Format d’API**

```http
POST /queries
```

**Requête**

La requête suivante crée une requête avec une instruction SQL fournie dans la payload :

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

L’exemple de requête ci-dessous crée une requête à l’aide d’un identifiant de modèle de requête existant.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
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
| `queryParameters` | Une paire clé-valeur pour remplacer les valeurs paramétrées dans l’instruction SQL. Cela n’est nécessaire que **si** vous utilisez des remplacements de paramètres dans le code SQL que vous fournissez. Aucune vérification de type valeur ne sera effectuée sur ces paires clé-valeur. |
| `templateId` | Identifiant unique d’une requête préexistante. Vous pouvez fournir cette information au lieu d’une instruction SQL. |
| `insertIntoParameters` | (Facultatif) Si cette propriété est définie, cette requête sera convertie en requête INSERT INTO. |
| `ctasParameters` | (Facultatif) Si cette propriété est définie, cette requête sera convertie en requête CTAS. |

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

Vous pouvez obtenir des informations détaillées sur une requête spécifique en effectuant une requête GET vers le point d’entrée `/queries` et en indiquant la valeur `id` de la requête dans le chemin d’accès à la requête.

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

### Annuler ou supprimer de manière réversible une requête

Vous pouvez demander l’annulation ou la suppression réversible d’une requête spécifiée en adressant une requête PATCH au point d’entrée `/queries` et en fournissant la valeur de `id` de la requête dans le chemin de requête.

**Format d’API**

```http
PATCH /queries/{QUERY_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{QUERY_ID}` | Valeur `id` de la requête sur laquelle vous souhaitez effectuer l’opération. |


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
| `op` | Type d’opération à effectuer sur la ressource. Les valeurs acceptées sont `cancel` et `soft_delete`. Pour annuler la requête, vous devez définir le paramètre op avec la valeur `cancel`. Notez que l’opération de suppression réversible empêche le renvoi de la requête sur les requêtes GET , mais ne la supprime pas du système. |

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec le message suivant :

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
