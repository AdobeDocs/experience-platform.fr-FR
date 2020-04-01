---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide du développeur du service '
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Requêtes

## Exemples d’appels d’API

Les sections suivantes passent en revue les appels que vous pouvez effectuer à l’aide du `/queries` point de fin dans l’API du service de  de. Chaque appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupérer un  de 

Vous pouvez récupérer un  de tous les  pour votre organisation IMS en envoyant une requête GET au point de `/queries` terminaison.

**Format API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facultatif*) Paramètres ajoutés au chemin de requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous.

**Paramètres**

Vous trouverez ci-dessous un  des paramètres de disponibles pour la liste des. Tous ces paramètres sont facultatifs. Un appel à ce point de fin sans paramètre récupérera tous les  de disponibles pour votre entreprise.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Indique le champ de commande des résultats. Les champs pris en charge sont `created` et `updated`. Par exemple, `orderby=created` triera les résultats par ordre croissant. L’ajout d’un élément `-` avant création (`orderby=-created`) triera les éléments par création dans l’ordre décroissant. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Default value: 20*) |
| `start` | Décale le  de réponse à l’aide d’une numérotation à base zéro. Par exemple, `start=2` renvoie un  commençant à partir du troisième répertorié. (*Default value: 0*) |
| `property` | Filtrez les résultats en fonction des champs. Le **doit** être une séquence d’échappement HTML. Les virgules sont utilisées pour combiner plusieurs jeux de  de. Les champs pris en charge sont `created`, `updated`, `state`et `id`. Les  des opérateurs pris en charge sont `>` (plus grand que), `<` (moins que), `>=` (plus grand ou égal à), `<=` (moins ou égal à), `==` (égal à), `!=` (différent de) et `~` (contient). Par exemple, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` renvoie tous les avec l’ID spécifié. |
| `excludeSoftDeleted` | Indique s’il faut inclure un  qui a été supprimé de manière souple. Par exemple, `excludeSoftDeleted=false` inclura **des**  de supprimés. (*Boolean, valeur par défaut : true*) |
| `excludeHidden` | Indique si les  de non pilotées par l’utilisateur doivent être affichées. La définition de cette valeur sur false **inclut** les  de non-utilisateur, telles que les définitions CURSOR, FETCH ou les de métadonnées. (*Boolean, valeur par défaut : true*) |

**Requête**

La requête suivante récupère le dernier créé pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec un de  de pour l’organisation IMS spécifiée en tant que JSON. La réponse suivante renvoie le dernier créé pour votre organisation IMS.

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

### Création d’un 

Vous pouvez créer un nouveau  en envoyant une requête POST au point de `/queries` fin.

**Format API**

```http
POST /queries
```

**Requête**

La requête suivante crée un nouveau  de, configuré par les valeurs fournies dans la charge :

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
| `dbName` | Nom de la base de données pour laquelle vous créez un SQL. |
| `sql` | Le SQL  que vous souhaitez créer. |
| `name` | Nom de votre SQL. |
| `description` | Description de votre SQL. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec les détails de votre  nouvellement créé. Une fois l’activation du terminée et son exécution réussie, le `state` passage de `SUBMITTED` à `SUCCESS`.

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

>[!NOTE] Vous pouvez utiliser la valeur de `_links.cancel` pour [annuler le](#cancel-a-query)créé.

### Récupération d’un par ID

Vous pouvez récupérer des informations détaillées sur un spécifique en envoyant une requête GET au point de `/queries` `id` fin et en indiquant la valeur de l’ de dans le chemin d’accès à la requête.

**Format API**

```http
GET /queries/{QUERY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_ID}` | La `id` valeur du à récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur le  spécifié.

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

>[!NOTE] Vous pouvez utiliser la valeur de `_links.cancel` pour [annuler le](#cancel-a-query)créé.

### Annuler un 

Vous pouvez demander de supprimer un spécifié en faisant une requête PATCH sur le `/queries` `id` point de fin et en fournissant la valeur  dans le chemin d’accès de la requête.

**Format API**

```http
PATCH /queries/{QUERY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_ID}` | La `id` valeur du à annuler. |


**Requête**

Cette requête d’API utilise la syntaxe du correctif JSON pour sa charge utile. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le des fondamentaux de l’API.

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
| `op` | Pour annuler le  du, vous devez définir le paramètre op avec la valeur `cancel `. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant :

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
