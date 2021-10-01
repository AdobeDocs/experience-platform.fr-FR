---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;modèles de requête;guide d’api;modèles;service de requête;
solution: Experience Platform
title: Point de terminaison de l’API de modèles de requête
topic-legacy: query templates
description: La documentation suivante décrit les différents appels d’API que vous pouvez effectuer à l’aide de modèles de requête pour l’API Query Service.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 89%

---

# Point de terminaison des modèles de requête

## Exemples d’appels API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API [!DNL Query Service]. Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API [!DNL Query Service]. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupération d’une liste de modèles de requête

Vous pouvez récupérer une liste de tous les modèles de requête pour votre organisation IMS en effectuant une requête GET sur le point de terminaison `/query-templates`.

**Format d’API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatif*) Les paramètres ajoutés au chemin de requête configurant les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres de requête**

Vous trouverez ci-dessous une liste des paramètres de requête disponibles pour répertorier les modèles de requête. Tous ces paramètres sont facultatifs. Un appel à ce point de terminaison sans paramètre permet de récupérer tous les modèles de requête disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Spécifie le champ de référence pour le tri des résultats. Les champs `created` et `updated` sont pris en charge. Par exemple, `orderby=created` triera les résultats par ordre croissant de création. L’ajout d’un `-` devant created (`orderby=-created`) triera les éléments par ordre décroissant de création. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Valeur par défaut : 20*) |
| `start` | Décale la liste de réponses à l’aide d’une numérotation à partir de zéro. Par exemple, `start=2` renvoie une liste commençant par la troisième requête répertoriée. (*Valeur par défaut : 0*) |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être précédés d’une séquence d’échappement HTML. Des virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs `name` et `userId` sont pris en charge. Le seul opérateur pris en charge est `==` (égal à). Par exemple, `name==my_template` renvoie tous les modèles de requête portant le nom `my_template`. |

**Requête**

La requête suivante récupère le dernier modèle de requête créé pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de modèles de requête pour l’organisation IMS spécifiée. La réponse suivante renvoie le dernier modèle de requête créé pour votre organisation IMS.

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

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer votre modèle de requête](#delete-a-specified-query-template).

### Création d’un modèle de requête

Vous pouvez créer un modèle de requête en effectuant une requête POST sur le point de terminaison `/query-templates`.

**Format d’API**

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
| `sql` | La requête SQL que vous souhaitez créer. |
| `name` | Le nom du modèle de requête. |

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec les détails du modèle de requête que vous venez de créer.

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

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer votre modèle de requête](#delete-a-specified-query-template).

### Récupération d’un modèle de requête spécifié

Vous pouvez récupérer un modèle de requête spécifique en effectuant une requête GET sur le point de terminaison `/query-templates/{TEMPLATE_ID}` et en fournissant l’identifiant du modèle de requête du chemin de requête.

**Format d’API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Propriété | Description |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | La valeur `id` du modèle de requête que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de votre modèle de requête spécifié.

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

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer votre modèle de requête](#delete-a-specified-query-template).

### Mise à jour d’un modèle de requête spécifié

Vous pouvez mettre à jour un modèle de requête spécifique en effectuant une requête PUT sur le point de terminaison `/query-templates/{TEMPLATE_ID}` et en fournissant l’identifiant du modèle de requête du chemin de requête.

**Format d’API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{TEMPLATE_ID}` | La valeur `id` du modèle de requête que vous souhaitez récupérer. |

**Requête**

>[!NOTE]
>
>La requête PUT exige que les champs sql et de nom soient remplis, et **remplace** le contenu actuel de ce modèle de requête.

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
| `sql` | La requête SQL que vous souhaitez mettre à jour. |
| `name` | Le nom de la requête planifiée. |

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec les informations mises à jour pour votre modèle de requête spécifié.

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

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer votre modèle de requête](#delete-a-specified-query-template).

### Suppression d’un modèle de requête spécifié

Vous pouvez supprimer un modèle de requête spécifique en effectuant une requête DELETE sur le `/query-templates/{TEMPLATE_ID}` et en fournissant l’identifiant du modèle de requête du chemin de requête.

**Format d’API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{TEMPLATE_ID}` | La valeur `id` du modèle de requête que vous souhaitez récupérer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec le message suivant.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
