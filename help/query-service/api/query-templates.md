---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide du développeur du service '
topic: query templates
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Modèle 

## Exemples d’appels d’API

Maintenant que vous comprenez les en-têtes à utiliser, vous êtes prêt à commencer à lancer des appels à l’API du service . Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API de service . Chaque appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupération d’un  de modèles 

Vous pouvez récupérer un  de tous les modèles de  pour votre organisation IMS en faisant une requête GET au point de `/query-templates` fin.

**Format API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatif*) Paramètres ajoutés au chemin de requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres**

Vous trouverez ci-dessous un  de paramètres de disponibles pour la liste des modèles de  del’. Tous ces paramètres sont facultatifs. Un appel à ce point de fin sans paramètre récupérera tous les modèles de  de disponibles pour votre entreprise.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Indique le champ de commande des résultats. Les champs pris en charge sont `created` et `updated`. Par exemple, `orderby=created` triera les résultats par ordre croissant. L’ajout d’un élément `-` avant création (`orderby=-created`) triera les éléments par création dans l’ordre décroissant. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Default value: 20*) |
| `start` | Décale le  de réponse à l’aide d’une numérotation à base zéro. Par exemple, `start=2` renvoie un  commençant à partir du troisième répertorié. (*Default value: 0*) |
| `property` | Filtrez les résultats en fonction des champs. Le **doit** être une séquence d’échappement HTML. Les virgules sont utilisées pour combiner plusieurs jeux de  de. Les champs pris en charge sont `name` et `userId`. Le seul opérateur pris en charge est `==` (égal à). Par exemple, `name==my_template` renvoie tous les modèles de  portant le nom `my_template`. |

**Requête**

La requête suivante récupère le dernier modèle de créé pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec un de modèles de  pour l’organisation IMS spécifiée. La réponse suivante renvoie le dernier modèle de  de créé pour votre organisation IMS.

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE] Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer votre modèle](#delete-a-specified-query-template)de  de.

### Création d’un modèle de 

Vous pouvez créer un modèle de  de en exécutant une requête POST sur le `/query-templates` point de fin.

**Format API**

```http
POST /query-templates
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `sql` | Le SQL  que vous souhaitez créer. |
| `name` | Nom du modèle de  de. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec les détails de votre modèle de  de nouvellement créé.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer votre modèle](#delete-a-specified-query-template)de  de.

### Récupération d’un modèle  de spécifique

Vous pouvez récupérer un modèle de  de spécifique en faisant une requête GET au point de `/query-templates/{TEMPLATE_ID}` fin et en fournissant l’ID du modèle de  de dans le chemin d’accès de la requête.

**Format API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Propriété | Description |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | Valeur `id` du modèle de  de que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails du modèle de spécifié.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer votre modèle](#delete-a-specified-query-template)de  de.

### Mettre à jour un modèle de  de spécifique

Vous pouvez mettre à jour un modèle de  de spécifique en faisant une requête PUT vers le point de `/query-templates/{TEMPLATE_ID}` fin et en fournissant l’ID du modèle de  de dans le chemin de requête.

**Format API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Valeur `id` du modèle de  de que vous souhaitez récupérer. |

**Requête**

>[!NOTE] La requête PUT exige que le champ sql et le champ de nom soient remplis et **remplace** le contenu actuel de ce modèle de  de.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `sql` | Le SQL  que vous souhaitez mettre à jour. |
| `name` | Nom du  planifié. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec les informations mises à jour pour votre modèle de  de spécifié.

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer votre modèle](#delete-a-specified-query-template)de  de.

### Suppression d’un modèle de  de spécifique

Vous pouvez supprimer un modèle de  de spécifique en faisant une requête DELETE à l’emplacement `/query-templates/{TEMPLATE_ID}` et en indiquant l’ID du modèle de  de dans le chemin d’accès de la requête.

**Format API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Valeur `id` du modèle de  de que vous souhaitez récupérer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
