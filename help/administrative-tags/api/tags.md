---
title: Point de terminaison des balises unifiées
description: Découvrez comment créer, mettre à jour, gérer et supprimer des catégories et des balises à l’aide des API Adobe Experience Platform.
role: Developer
source-git-commit: ede314d0cbe50514090915fccf7ef3c2a5254b7a
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 4%

---


# Point d’entrée des balises unifiées

>[!IMPORTANT]
>
>L’URL de point de terminaison de cet ensemble de points de terminaison est : `https://experience.adobe.io`.

Les balises sont une fonctionnalité qui vous permet de gérer des taxonomies de métadonnées afin de classer les objets métier pour une découverte et une catégorisation plus simples. Vous pouvez ensuite organiser ces balises en d’autres groupes en les ajoutant aux catégories de balises.

Ce guide fournit des informations pour vous aider à mieux comprendre les balises et les catégories de balises et inclut des exemples d’appels API pour effectuer des actions de base à l’aide de l’API.

## Commencer

Les points de terminaison utilisés dans ce guide font partie des API Adobe Experience Platform. Avant de poursuivre, veuillez consulter la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels à l’API, notamment les en-têtes requis et la lecture d’exemples d’appels API

### Glossaire

Le glossaire suivant met en évidence la différence entre un **tag** et un **catégorie de balises**.

- **Balise**: une balise vous permet de gérer la taxonomie des métadonnées pour les objets commerciaux, ce qui vous permet de classer ces objets pour une découverte et une catégorisation plus simples.
   - **Balise non classée**: une balise non classée est une balise qui n’appartient pas à une catégorie de balise. Par défaut, les balises créées ne sont pas catégorisées.
- **Catégorie de balise**: une catégorie de balises vous permet de regrouper vos balises dans des ensembles significatifs, ce qui vous permet de fournir plus de contexte à l’objectif de la balise.

## Récupération d’une liste de catégories de balises {#get-tag-categories}

Vous pouvez récupérer une liste des catégories de balises appartenant à votre organisation en adressant une requête GET à la variable `/tagCategory` point de terminaison .

**Format d’API**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

Les paramètres de requête facultatifs suivants peuvent être utilisés lors de la récupération des catégories de balises.

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `start` | L’emplacement à partir duquel commence la liste de résultats. Vous pouvez l’utiliser pour indiquer l’index de départ pour la pagination des résultats. | `start=a` |
| `limit` | Nombre maximal de catégories de balises que vous souhaitez récupérer par page. | `limit=20` |
| `property` | L’attribut que vous souhaitez filtrer lors de la récupération des catégories de balises. Les valeurs prises en charge sont les suivantes : &lt;ul><li>`name`: nom de la catégorie de balises.</li></ul> | `property=name==category` |
| `sortBy` | Ordre dans lequel les catégories de balises sont triées. Les valeurs prises en charge incluent : `name`, `createdAt`, et `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Orientation du tri des catégories de balises. Les valeurs prises en charge incluent : `asc` et `desc`. | `sortOrder=asc` |

**Requête**

+++Exemple de requête pour répertorier toutes les catégories de balises de votre organisation

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de toutes les catégories de balises pour votre organisation.

+++Exemple de réponse contenant une liste de toutes les catégories de balises de votre organisation.

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## Création d’une catégorie de balise {#create-tag-category}

>[!IMPORTANT]
>
>Seul l’administrateur système et l’administrateur de produit peuvent utiliser cet appel d’API.

Vous pouvez créer une catégorie de balise en adressant une requête de POST au `/tagCategory` point de terminaison .

**Format d’API**

```http
POST /tagCategory
```

**Requête**

+++Exemple de requête pour créer une catégorie de balise.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom de la catégorie de balises que vous souhaitez créer. |
| `description` | Description de la catégorie de balises à créer. |

+++

**Réponse**

Un exemple de réponse renvoie un état HTTP 200 avec les détails de la catégorie de balise que vous venez de créer.

+++Exemple de réponse contenant des détails sur la catégorie de balises que vous venez de créer.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Récupération d’une catégorie de balise spécifique {#get-tag-category}

Vous pouvez récupérer une catégorie de balises spécifique qui appartient à votre organisation en envoyant une requête de GET à la variable `/tagCategory` point de terminaison et spécification de l’identifiant de la catégorie de balises.

**Format d’API**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | Identifiant de la catégorie de balises que vous récupérez. |

**Requête**

+++Exemple de requête pour récupérer une catégorie de balise spécifique

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la catégorie de balise spécifiée.

+++Exemple de réponse contenant des détails sur la catégorie de balises spécifiée.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | ID de la catégorie de balise demandée. |
| `name` | Nom de la catégorie de balises demandée. |
| `description` | Description de la catégorie de balises demandée. |
| `createdBy` | Identifiant de l’utilisateur qui a créé la catégorie de balises. |
| `createdAt` | Horodatage de la création de la catégorie de balise. |
| `modifiedBy` | ID de l’utilisateur qui a mis à jour la catégorie de balises pour la dernière fois. |
| `modifiedAt` | Horodatage de la dernière mise à jour de la catégorie de balises. |
| `tagCount` | Nombre de balises appartenant à la catégorie de balises. |

+++

## Mise à jour d’une catégorie de balise spécifique {#update-tag-category}

>[!IMPORTANT]
>
>Seul l’administrateur système et l’administrateur de produit peuvent utiliser cet appel d’API.

Vous pouvez mettre à jour les détails d’une catégorie de balises spécifique qui appartient à votre organisation en adressant une requête de PATCH à la fonction `/tagCategory` point de terminaison et spécification de l’identifiant de la catégorie de balises.

**Format d’API**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | Identifiant de la catégorie de balises que vous récupérez. |

**Requête**

+++Exemple de requête pour mettre à jour une catégorie de balise spécifique

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| Paramètre | Description |
| --------- | ----------- |
| `op` | Opération terminée. Pour mettre à jour une catégorie de balises spécifique, définissez cette valeur sur `replace`. |
| `path` | Chemin du champ qui sera mis à jour. Les valeurs prises en charge incluent : `name` et `description`. |
| `value` | La valeur mise à jour du champ que vous souhaitez mettre à jour. |
| `from` | La valeur d’origine du champ que vous souhaitez mettre à jour. |

+++

**Réponse**

Une réponse réussie : état HTTP 200 avec des informations sur votre nouvelle catégorie de balises mise à jour.

+++Exemple de réponse contenant des détails sur la catégorie de balises que vous venez de mettre à jour.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Suppression d’une catégorie de balise spécifique {#delete-tag-category}

>[!IMPORTANT]
>
>Seul l’administrateur système et l’administrateur de produit peuvent utiliser cet appel d’API.

Vous pouvez supprimer une catégorie de balises spécifique qui appartient à votre organisation en adressant une requête de DELETE à la fonction `/tagCategory` point de terminaison et spécification de l’identifiant de la catégorie de balises.

**Format d’API**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | Identifiant de la catégorie de balises que vous récupérez. |

**Requête**

+++Exemple de requête pour supprimer une catégorie de balise spécifique

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une réponse vide.

## Récupération d’une liste de balises {#get-tags}

Vous pouvez récupérer une liste de balises appartenant à votre organisation en adressant une requête GET à la variable `/tags` point de terminaison et identifiant de la catégorie de balise.

**Format d’API**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

Les paramètres de requête facultatifs suivants peuvent être utilisés lors de la récupération de balises.

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `start` | L’emplacement à partir duquel commence la liste de résultats. Vous pouvez l’utiliser pour indiquer l’index de départ pour la pagination des résultats. | `start=a` |
| `limit` | Nombre maximal de balises que vous souhaitez récupérer par page. | `limit=20` |
| `property` | L’attribut par lequel vous souhaitez filtrer lors de la récupération des balises. Les valeurs prises en charge sont les suivantes :<ul><li>`name`: nom de la balise.</li><li>`archived`: indique si les balises sont archivées ou non. Vous pouvez définir cette valeur sur : `true` ou `false`.</li><li>`tagCategoryId`: identifiant de la catégorie de balise à laquelle la balise appartient.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | Ordre dans lequel les balises sont triées. Les valeurs prises en charge incluent : `name`, `createdAt`, et `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Orientation du tri des catégories de balises. Les valeurs prises en charge incluent : `asc` et `desc`. | `sortOrder=asc` |


**Requête**

+++Exemple de requête pour récupérer toutes les balises appartenant à une catégorie de balises spécifique

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails des balises appartenant à cette catégorie de balises.

+++ Un exemple de réponse contenant les détails des balises demandées.

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## Création d’une balise {#create-tag}

>[!IMPORTANT]
>
>Seul l’administrateur système et l’administrateur de produit peuvent utiliser cet appel d’API pour créer une balise dans une catégorie de balise spécifiée.
>
>Si vous créez une balise non catégorisée, vous le faites **not** nécessite des autorisations d’administrateur.

Vous pouvez créer une balise en adressant une requête de POST à la fonction `/tags` point de terminaison .

**Format d’API**

```http
POST /tags
```

**Requête**

+++Exemple de requête pour créer une balise.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | **Obligatoire**. Nom de la balise que vous souhaitez créer. |
| `tagCategoryId` | *Facultatif*. Identifiant de la catégorie de balises à laquelle vous souhaitez que la balise apparaisse. Si elle n’est pas spécifiée, la balise est créée dans la catégorie Non catégorisée. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de la balise nouvellement créée.

+++Exemple de réponse contenant les détails de la balise que vous venez de créer.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| Paramètre | Description |
| --------- | ----------- |
| `name` | Nom de la balise nouvellement créée. |
| `id` | L’identifiant de la balise nouvellement créée. |
| `org` | ID de l’organisation à laquelle la balise appartient. |
| `createdAt` | Horodatage de la création de la balise. |
| `createdBy` | Identifiant de l’utilisateur qui a créé la balise. |
| `modifiedAt` | Horodatage de la dernière mise à jour de la balise. |
| `modifiedBy` | Identifiant de l’utilisateur qui a mis à jour la balise pour la dernière fois. |
| `tagCategoryId` | Identifiant de la catégorie de balises à laquelle la balise appartient. |
| `tagCategoryName` | Nom de la catégorie de balises à laquelle la balise appartient. |

+++

## Récupération d’une balise spécifique {#get-tag}

Vous pouvez récupérer une balise spécifique qui appartient à votre organisation en adressant une requête de GET à la variable `/tags` point de terminaison et spécification de l’identifiant de la balise que vous souhaitez récupérer.

**Format d’API**

```http
GET /tags/{TAG_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_ID}` | Identifiant de la balise que vous récupérez. |

**Requête**

+++Exemple de requête pour récupérer une balise spécifique

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la balise spécifiée.

+++Exemple de réponse contenant les détails de la balise spécifiée.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| Paramètre | Description |
| --------- | ----------- |
| `name` | Nom de la balise que vous avez récupérée. |
| `id` | L’identifiant de la balise que vous avez récupérée. |
| `org` | ID de l’organisation à laquelle la balise appartient. |
| `createdAt` | Horodatage de la création de la balise. |
| `createdBy` | Identifiant de l’utilisateur qui a créé la balise. |
| `modifiedAt` | Horodatage de la dernière mise à jour de la balise. |
| `modifiedBy` | Identifiant de l’utilisateur qui a mis à jour la balise pour la dernière fois. |
| `tagCategoryId` | Identifiant de la catégorie de balises à laquelle la balise appartient. |
| `tagCategoryName` | Nom de la catégorie de balises à laquelle la balise appartient. |
| `archived` | État d’archivage de la balise. Si la variable est définie sur `true`, cela signifie que la balise est archivée. |

+++

## Validation des balises {#validate-tags}

Vous pouvez vérifier si des balises existent en envoyant une requête de POST au `/tags/validate` point de terminaison .

**Format d’API**

```http
POST /tags/validate
```

**Requête**

+++Exemple de requête pour valider les ID de balise fournis.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `ids` | Tableau contenant une liste d’ID de balise que vous souhaitez valider. |
| `entity` | L’entité qui demande la validation. Vous pouvez utiliser la variable `{API_KEY}` pour ce paramètre. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur les balises valides et non valides.

+++Exemple de réponse affichant les balises valides et non valides.

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `invalidTags` | Tableau contenant une liste des ID de balise non valides. |
| `validTags` | Tableau contenant une liste des ID de balise valides. |

+++

## Mettre à jour une balise spécifique {#update-tag}

Vous pouvez mettre à jour une balise spécifique en adressant une requête de PATCH à la fonction `/tags` point de terminaison et en indiquant l’identifiant de la balise que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /tags/{TAG_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_ID}` | Identifiant de la balise que vous mettez à jour. |

**Requête**

+++Exemple de requête pour mettre à jour une balise spécifique

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| Propriété | Description |
| -------- | ----------- |
| `op` | L’opération qui doit être effectuée. Dans ce cas d’utilisation, il sera toujours défini sur `replace`. |
| `path` | Chemin du champ qui sera mis à jour. Les valeurs prises en charge incluent : `name`, `archived`, et `tagCategoryId`. |
| `value` | La valeur mise à jour du champ que vous souhaitez mettre à jour. |
| `from` | La valeur d’origine du champ que vous souhaitez mettre à jour. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la balise qui vient d’être mise à jour.

+++Exemple de réponse contenant les détails de la balise mise à jour.

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## Supprimer une balise spécifique {#delete-tag}

>[!IMPORTANT]
>
>Seul l’administrateur système et l’administrateur de produit peuvent utiliser cet appel d’API.
>
>En outre, la balise **cannot** être associés à tout objet commercial et **must** être archivés avant de pouvoir supprimer la balise. Vous pouvez archiver la balise à l’aide de la méthode [mettre à jour le point de fin de balise](#update-tag).

Vous pouvez supprimer une balise spécifique en effectuant une balise DELETE sur la balise `/tags` point de terminaison et spécification de l’identifiant de la balise que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /tags/{TAG_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_ID}` | Identifiant de la balise que vous supprimez. |

**Requête**

+++Exemple de requête pour supprimer une balise spécifique

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une réponse vide.

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment créer, gérer et supprimer des balises et des catégories de balises à l’aide des API Adobe Experience Platform. Pour plus d’informations sur la gestion des balises à l’aide de l’interface utilisateur, veuillez lire le [guide de gestion des balises](../ui/managing-tags.md). Pour plus d’informations sur la gestion des catégories de balises à l’aide de l’interface utilisateur, consultez la section [guide des catégories de balises](../ui/tags-categories.md).
