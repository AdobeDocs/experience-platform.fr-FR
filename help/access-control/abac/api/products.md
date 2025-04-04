---
keywords: Experience Platform;accueil;rubriques populaires;api;Contrôle d’accès basé sur les attributs;contrôle d’accès basé sur les attributs
solution: Experience Platform
title: Point d’entrée de l’API Products
description: Le point d’entrée /products de l’API de contrôle d’accès basé sur les attributs vous permet de gérer les produits dans Adobe Experience Platform par programmation.
role: Developer
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 25%

---

# Point d’entrée de produits

>[!NOTE]
>
>Si un jeton d’utilisateur est transmis, l’utilisateur du jeton doit disposer d’un rôle « administrateur d’organisation » pour l’organisation demandée.

Le point d’entrée `/products` de l’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les produits, ainsi que les catégories d’autorisations et les jeux d’autorisations associés aux produits de votre organisation.

## Commencer

Le point d’entrée de l’API utilisé dans ce guide fait partie de l’API de contrôle d’accès basé sur les attributs. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de produits autorisés {#list}

Vous pouvez récupérer une liste de produits autorisés en effectuant une requête GET au point d’entrée `/products`.

**Format d’API**

```http
GET /products/
```

**Requête**

La requête suivante récupère une liste des produits autorisés appartenant à votre organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie une liste des produits autorisés appartenant à votre organisation.

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant correspondant au produit interrogé. |
| `name` | Nom du produit interrogé. |
| `serviceCode` | Code service correspondant du produit interrogé. |

## Recherche des catégories d’autorisations par ID de produit

Vous pouvez rechercher des catégories d’autorisations pour un produit donné en adressant une requête GET au point d’entrée `/products/{PRODUCT_ID}/categories` lors de la spécification de votre ID de produit.

**Format d’API**

```http
GET /products/{PRODUCT_ID}/categories
```

| Paramètre | Description |
| --- | --- |
| {PRODUCT_ID} | Identifiant du produit associé aux catégories d’autorisations que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère les catégories d’autorisations associées à `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie les catégories d’autorisations associées à l’ID de produit que vous avez interrogé.

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `category` | Catégories d’autorisations disponibles dans l’ID de produit interrogé. |
| `name` | Nom de la catégorie d’autorisations. |

## Rechercher des jeux d’autorisations par ID de produit

Vous pouvez rechercher des jeux d’autorisations pour un produit donné en adressant une requête GET au point d’entrée `/products/{PRODUCT_ID}/permission-sets` lors de la spécification de votre ID de produit.

**Format d’API**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Paramètre | Description |
| --- | --- |
| {PRODUCT_ID} | L’identifiant du produit associé aux jeux d’autorisations que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère les jeux d’autorisations associés à `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie les jeux d’autorisations associés à l’ID de produit que vous avez interrogé.

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| Propriété | Description |
| --- | --- |
| `permission-sets` | Les jeux d’autorisations représentent un groupe d’autorisations qu’un administrateur peut appliquer à un rôle. Un administrateur peut attribuer des jeux d’autorisations à un rôle au lieu d’affecter des autorisations individuelles. Vous pouvez ainsi créer des rôles personnalisés à partir d’un rôle prédéfini contenant un groupe d’autorisations. |
| `id` | L’identifiant correspondant du jeu d’autorisations interrogé. |
| `name` | Nom correspondant au jeu d’autorisations interrogé. |
| `category` | La catégorie d’autorisations disponible. |
| `permissions` | Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Experience Platform, telles que la création de sandbox, la définition de schémas et la gestion des jeux de données. |
| `permissions.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder. Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `permissions.actions` | Action qu’un sujet est autorisé à effectuer sur une ressource interrogée. Les valeurs possibles sont : `view`, `read`, `create`, `edit` et `delete` |
