---
title: Point d’entrée de balises unifiées
description: Découvrez comment créer, mettre à jour, gérer et supprimer des catégories de balises et des balises à l’aide des API Adobe Experience Platform.
role: Developer
exl-id: 6687d1da-a5e4-435a-9f99-1b0f9ac98088
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 4%

---

# Point d’entrée de balises unifiées

>[!IMPORTANT]
>
>L’URL du point d’entrée pour ce jeu de points d’entrée est `https://experience.adobe.io`.

Les balises sont une fonctionnalité de gestion des taxonomies des métadonnées permettant de classer les objets d’entreprise pour une découverte et un classement plus faciles. Vous pouvez ensuite organiser ces balises en groupes supplémentaires en les ajoutant à des catégories de balises.

Ce guide fournit des informations pour vous aider à mieux comprendre les balises et les catégories de balises. Il comprend des exemples d’appels API pour exécuter des actions de base à l’aide de l’API .

## Prise en main

Les points d’entrée utilisés dans ce guide font partie des API Adobe Experience Platform. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et la manière de lire des exemples d’appels API

### Glossaire

Le glossaire suivant met en évidence la différence entre une **balise** et une **catégorie de balises**.

- **Balise** : une balise vous permet de gérer la taxonomie des métadonnées pour les objets métier, ce qui vous permet de classer ces objets pour une découverte et une catégorisation plus faciles.
   - **Balise non classée** : une balise non classée est une balise qui n’appartient à aucune catégorie de balises. Par défaut, les balises créées ne sont pas classées.
- **Catégorie de balises** : une catégorie de balises vous permet de regrouper vos balises dans des ensembles significatifs, ce qui vous permet de fournir plus de contexte à l’objectif de la balise.

## Récupération d’une liste de catégories de balises {#get-tag-categories}

Vous pouvez récupérer une liste de catégories de balises appartenant à votre organisation en envoyant une requête GET au point d’entrée `/tagCategory`.

**Format d’API**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

Les paramètres de requête facultatifs suivants peuvent être utilisés lors de la récupération de catégories de balises.

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `start` | Emplacement de départ de la liste des résultats. Vous pouvez l’utiliser pour indiquer l’index de départ pour la pagination des résultats. | `start=a` |
| `limit` | Nombre maximal de catégories de balises à récupérer par page. | `limit=20` |
| `property` | Attribut selon lequel vous souhaitez filtrer lors de la récupération de catégories de balises. Les valeurs prises en charge sont : &lt;ul≥<li>`name` : nom de la catégorie de balises.</li></ul> | `property=name==category` |
| `sortBy` | Ordre de tri des catégories de balises. Les valeurs prises en charge sont `name`, `createdAt` et `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Sens du tri des catégories de balises. Les valeurs prises en charge comprennent `asc` et `desc`. | `sortOrder=asc` |

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

## Créer une catégorie de balises {#create-tag-category}

>[!IMPORTANT]
>
>Seuls l’administrateur système et l’administrateur produit peuvent utiliser cet appel API.

Vous pouvez créer une catégorie de balises en effectuant une requête POST vers le point d’entrée `/tagCategory`.

**Format d’API**

```http
POST /tagCategory
```

**Requête**

+++Exemple de requête pour créer une catégorie de balises.

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
| `name` | Nom de la catégorie de balises à créer. |
| `description` | Description de la catégorie de balises que vous souhaitez créer. |

+++

**Réponse**

Un exemple de réponse renvoie le statut HTTP 200 avec les détails de la catégorie de balises que vous venez de créer.

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

## Récupération d’une catégorie de balises spécifique {#get-tag-category}

Vous pouvez récupérer une catégorie de balises spécifique qui appartient à votre organisation en adressant une requête GET au point d’entrée `/tagCategory` et en spécifiant l’identifiant de la catégorie de balises.

**Format d’API**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | L’identifiant de la catégorie de balises que vous récupérez. |

**Requête**

+++Exemple de requête pour récupérer une catégorie de balises spécifique

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la catégorie de balises spécifiée.

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
| `id` | L’identifiant de la catégorie de balises demandée. |
| `name` | Nom de la catégorie de balises demandée. |
| `description` | Description de la catégorie de balises demandée. |
| `createdBy` | ID de l’utilisateur qui a créé la catégorie de balises. |
| `createdAt` | Date et heure de création de la catégorie de balises. |
| `modifiedBy` | ID du dernier utilisateur à avoir mis à jour la catégorie de balises. |
| `modifiedAt` | Date et heure de la dernière mise à jour de la catégorie de balises. |
| `tagCount` | Nombre de balises appartenant à la catégorie de balises. |

+++

## Mise à jour d’une catégorie de balises spécifique {#update-tag-category}

>[!IMPORTANT]
>
>Seuls l’administrateur système et l’administrateur produit peuvent utiliser cet appel API.

Vous pouvez mettre à jour les détails d’une catégorie de balises spécifique qui appartient à votre organisation en envoyant une requête PATCH au point d’entrée `/tagCategory` et en spécifiant l’identifiant de la catégorie de balises.

**Format d’API**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | L’identifiant de la catégorie de balises que vous récupérez. |

**Requête**

+++Exemple de requête pour mettre à jour une catégorie de balises spécifique

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
| `path` | Chemin d’accès au champ qui sera mis à jour. Les valeurs prises en charge comprennent `name` et `description`. |
| `value` | Valeur mise à jour du champ à mettre à jour. |
| `from` | Valeur d’origine du champ à mettre à jour. |

+++

**Réponse**

Réponse réussie État HTTP 200 avec des informations sur votre catégorie de balises nouvellement mise à jour.

+++Exemple de réponse contenant des détails sur votre catégorie de balises nouvellement mise à jour.

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

## Supprimer une catégorie de balises spécifique {#delete-tag-category}

>[!IMPORTANT]
>
>Seuls l’administrateur système et l’administrateur produit peuvent utiliser cet appel API.

Vous pouvez supprimer une catégorie de balises spécifique qui appartient à votre organisation en adressant une requête DELETE au point d’entrée `/tagCategory` et en spécifiant l’identifiant de la catégorie de balises.

**Format d’API**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | L’identifiant de la catégorie de balises que vous récupérez. |

**Requête**

+++Exemple de requête pour supprimer une catégorie de balises spécifique

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

## Récupérer une liste de balises {#get-tags}

Vous pouvez récupérer une liste de balises appartenant à votre organisation en envoyant une requête GET au point d’entrée `/tags` et à l’identifiant de la catégorie de balises.

**Format d’API**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

Les paramètres de requête facultatifs suivants peuvent être utilisés lors de la récupération de balises.

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `start` | Emplacement de départ de la liste des résultats. Vous pouvez l’utiliser pour indiquer l’index de départ pour la pagination des résultats. | `start=a` |
| `limit` | Nombre maximal de balises à récupérer par page. | `limit=20` |
| `property` | Attribut selon lequel vous souhaitez filtrer lors de la récupération de balises. Les valeurs prises en charge sont les suivantes :<ul><li>`name` : nom de la balise.</li><li>`archived` : indique si les balises sont archivées ou non. Vous pouvez définir cette valeur sur `true` ou `false`.</li><li>`tagCategoryId` : ID de la catégorie de balises à laquelle appartient la balise.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | Ordre de tri des balises. Les valeurs prises en charge sont `name`, `createdAt` et `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Sens du tri des catégories de balises. Les valeurs prises en charge comprennent `asc` et `desc`. | `sortOrder=asc` |


**Requête**

+++Exemple de requête permettant de récupérer toutes les balises appartenant à une catégorie de balises spécifique

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

+++ Exemple de réponse contenant les détails des balises demandées.

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

## Créer une balise {#create-tag}

>[!IMPORTANT]
>
>Seuls l’administrateur système et l’administrateur de produit peuvent utiliser cet appel API pour créer une balise dans une catégorie de balises spécifiée.
>
>Si vous créez une balise non classée, vous n’avez **besoin**’autorisations d’administrateur.

Vous pouvez créer une balise en effectuant une requête POST vers le point d’entrée `/tags`.

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
| `name` | **Obligatoire**. Nom de la balise à créer. |
| `tagCategoryId` | *Facultatif*. L’identifiant de la catégorie de balises à laquelle vous souhaitez que la balise appartienne. Si elle n’est pas spécifiée, la balise est créée dans la catégorie Non classé . |

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 201 avec les détails de la balise que vous venez de créer.

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
| `org` | Identifiant de l’organisation à laquelle appartient la balise. |
| `createdAt` | Date et heure de création de la balise. |
| `createdBy` | Identifiant de l’utilisateur qui a créé la balise. |
| `modifiedAt` | Date et heure de la dernière mise à jour de la balise. |
| `modifiedBy` | ID du dernier utilisateur à avoir mis à jour la balise. |
| `tagCategoryId` | Identifiant de la catégorie de balises à laquelle appartient la balise. |
| `tagCategoryName` | Nom de la catégorie de balises à laquelle appartient la balise. |

+++

## Récupération d’une balise spécifique {#get-tag}

Vous pouvez récupérer une balise spécifique appartenant à votre organisation en adressant une requête GET au point d’entrée `/tags` et en spécifiant l’identifiant de la balise à récupérer.

**Format d’API**

```http
GET /tags/{TAG_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_ID}` | L’identifiant de la balise que vous récupérez. |

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

+++Exemple de réponse contenant des détails sur la balise spécifiée. 

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
| `id` | L’identifiant de la balise que vous avez récupéré. |
| `org` | Identifiant de l’organisation à laquelle appartient la balise. |
| `createdAt` | Date et heure de création de la balise. |
| `createdBy` | Identifiant de l’utilisateur qui a créé la balise. |
| `modifiedAt` | Date et heure de la dernière mise à jour de la balise. |
| `modifiedBy` | ID du dernier utilisateur à avoir mis à jour la balise. |
| `tagCategoryId` | Identifiant de la catégorie de balises à laquelle appartient la balise. |
| `tagCategoryName` | Nom de la catégorie de balises à laquelle appartient la balise. |
| `archived` | Statut d’archivage de la balise. Si elle est définie sur `true`, cela signifie que la balise est archivée. |

+++

## Validation des balises {#validate-tags}

Vous pouvez vérifier s’il existe des balises en effectuant une requête POST vers le point d’entrée `/tags/validate`.

**Format d’API**

```http
POST /tags/validate
```

**Requête**

+++Exemple de requête pour valider les identifiants de balise fournis.

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
| `ids` | Un tableau contenant une liste d’ID de balise à valider. |
| `entity` | L’entité qui demande la validation. Vous pouvez utiliser la valeur `{API_KEY}` pour ce paramètre. |

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
| `invalidTags` | Un tableau contenant une liste des ID de balise non valides. |
| `validTags` | Un tableau contenant une liste des ID de balise valides. |

+++

## Mettre à jour une balise spécifique {#update-tag}

Vous pouvez mettre à jour une balise spécifiée en adressant une requête PATCH au point d’entrée `/tags` et en fournissant l’identifiant de la balise que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /tags/{TAG_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_ID}` | L’identifiant de la balise que vous mettez à jour. |

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
| `op` | Opération qui doit être effectuée. Dans ce cas d’utilisation, elle sera toujours définie sur `replace`. |
| `path` | Chemin d’accès au champ qui sera mis à jour. Les valeurs prises en charge sont `name`, `archived` et `tagCategoryId`. |
| `value` | Valeur mise à jour du champ à mettre à jour. |
| `from` | Valeur d’origine du champ à mettre à jour. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la balise nouvellement mise à jour.

+++Exemple de réponse contenant des détails sur la balise mise à jour.

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
>Seuls l’administrateur système et l’administrateur produit peuvent utiliser cet appel API.
>
>En outre, la balise **ne peut pas** être associée à des objets métier et **doit** être archivée avant de pouvoir la supprimer. Vous pouvez archiver la balise à l’aide du point d’entrée de balise [update](#update-tag).

Vous pouvez supprimer une balise spécifique en ajoutant une balise DELETE au point d’entrée `/tags` et en spécifiant l’identifiant de la balise à supprimer.

**Format d’API**

```http
DELETE /tags/{TAG_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{TAG_ID}` | L’identifiant de la balise que vous supprimez. |

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

Vous êtes arrivé au bout de ce guide. À présent, vous comprenez mieux comment créer, gérer et supprimer des balises et des catégories de balises à l’aide des API Adobe Experience Platform. Pour plus d’informations sur la gestion des balises à l’aide de l’interface utilisateur, consultez le [guide de gestion des balises](../ui/managing-tags.md). Pour plus d’informations sur la gestion des catégories de balises à l’aide de l’interface utilisateur, consultez le [&#x200B; guide des catégories de balises](../ui/tags-categories.md).
