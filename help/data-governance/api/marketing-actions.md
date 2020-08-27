---
keywords: Experience Platform;home;popular topics;Policy enforcement;marketing actions api;API-based enforcement;data governance
solution: Experience Platform
title: Actions marketing
topic: developer guide
description: Dans le cadre de la gouvernance des données Adobe Experience Platform, une action marketing est une action entreprise par un utilisateur de données Experience Platform pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 14%

---


# Point de terminaison des actions marketing

A marketing action, in the context of the Adobe Experience Platform [!DNL Data Governance], is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies.

Vous pouvez gérer les actions marketing pour votre organisation à l’aide du `/marketingActions` point de terminaison dans l’API Policy Service.

## Prise en main

The API endpoints used in this guide are part of the [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Avant de continuer, consultez le guide [de](./getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute [!DNL Experience Platform] API.

## Récupération d’une liste d’actions marketing {#list}

Vous pouvez récupérer une liste d’actions marketing de base ou personnalisées en adressant une demande de GET `/marketingActions/core` ou `/marketingActions/custom`, respectivement.

**Format d’API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Requête**

La requête suivante récupère une liste d’actions marketing personnalisées conservées par votre organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie les détails de chaque action marketing récupérée, y compris son `name` et `href`. La `href` valeur sert à identifier l’action marketing lors de la [création d’une stratégie](policies.md#create-policy)d’utilisation des données.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `_page.count` | Nombre total d’actions marketing renvoyées. |
| `children` | Tableau d’objets contenant les détails des actions marketing récupérées. |
| `name` | Nom de l’action marketing, qui agit comme identifiant unique lors de la [recherche d’une action](#lookup)marketing spécifique. |
| `_links.self.href` | Référence URI pour l’action marketing, qui peut être utilisée pour compléter le `marketingActionsRefs` tableau lors de la [création d’une stratégie](policies.md#create-policy)d’utilisation des données. |

## Recherche d’une action marketing spécifique {#lookup}

Vous recherchez les détails d’une action marketing spécifique en incluant la `name` propriété de l’action marketing dans le chemin d’une demande de GET.

**Format d’API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | The `name` property of the marketing action you want to look up. |

**Requête**

La requête suivante récupère une action marketing personnalisée nommée `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet de réponse contient les détails de l’action marketing, y compris le chemin d’accès (`_links.self.href`[) nécessaire pour référencer l’action marketing lorsque vous définissez une stratégie d’utilisation des données](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Create or update a custom marketing action {#create-update}

Vous pouvez créer une action marketing personnalisée ou en mettre à jour une existante en incluant le nom existant ou prévu de l’action marketing dans le chemin d’une demande de PUT.

**Format d’API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à créer ou à mettre à jour. Si une action marketing portant le nom fourni existe déjà dans le système, elle est mise à jour. S’il n’en existe pas, une nouvelle action marketing est créée pour le nom fourni. |

**Requête**

La requête suivante crée une nouvelle action marketing nommée `crossSiteTargeting`, à condition qu’une action marketing du même nom n’existe pas encore dans le système. S’il existe une action `crossSiteTargeting` marketing, cet appel met à jour cette action en fonction des propriétés fournies dans la charge utile.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de l’action marketing à créer ou à mettre à jour. <br><br>**IMPORTANT**: Cette propriété doit correspondre au chemin `{MARKETING_ACTION_NAME}` d’accès, faute de quoi une erreur HTTP 400 (Mauvaise requête) se produira. En d’autres termes, une fois qu’une action marketing a été créée, sa `name` propriété ne peut plus être modifiée. |
| `description` | Description facultative afin de fournir un contexte supplémentaire pour l’action marketing. |

**Réponse**

Une réponse positive renvoie les détails de l’action marketing. Si une action marketing existante a été mise à jour, la réponse renvoie l’état HTTP 200 (OK). Si une nouvelle action marketing a été créée, la réponse renvoie l’état HTTP 201 (Créé).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Delete a custom marketing action {#delete}

Vous pouvez supprimer une action marketing personnalisée en incluant son nom dans le chemin d’une requête de DELETE.

>[!NOTE]
>
>Les actions marketing référencées par des stratégies existantes ne peuvent pas être supprimées. Toute tentative de suppression de l’une de ces actions marketing provoquera une erreur HTTP 400 (Mauvaise requête), ainsi qu’un message contenant les ID de toutes les stratégies qui font référence à l’action marketing.

**Format d’API**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à supprimer. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie HTTP Status 200 (OK) avec un corps de réponse vide.

You can confirm the deletion by attempting to [look up the marketing action](#look-up). Vous devriez recevoir une erreur HTTP 404 (introuvable) si l’action marketing a été supprimée du système.
