---
keywords: Experience Platform;accueil;rubriques populaires;Application des stratégies;API des actions marketing;Application basée sur les API;gouvernance des données
solution: Experience Platform
title: Point d’entrée de l’API des actions marketing
description: Dans le cadre de la gouvernance des données Adobe Experience Platform, une action marketing est une action entreprise par un utilisateur de données Experience Platform pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: ht
source-wordcount: '732'
ht-degree: 100%

---

# Point d’entrée des actions marketing

Dans le cadre de la gouvernance des données d’Adobe Experience Platform, une action marketing est une action entreprise par un utilisateur de données [!DNL Experience Platform] pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

Vous pouvez gérer les actions marketing pour votre organisation en utilisant le point d’entrée `/marketingActions` de l’API Policy Service.

## Prise en main

Les points d’entrée d’API utilisés dans ce guide font partie de l’[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Récupération d’une liste d’actions marketing {#list}

Vous pouvez récupérer une liste d’actions marketing de base ou personnalisées en adressant respectivement une requête GET à `/marketingActions/core` ou `/marketingActions/custom`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de chaque action marketing récupérée, y compris son `name` et son `href`. La valeur `href` est utilisée pour identifier l’action marketing lors de la [création d’une stratégie d’utilisation des données](policies.md#create-policy).

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `name` | Nom de l’action marketing, qui agit comme identifiant unique lors de la [recherche d’une action marketing spécifique](#lookup). |
| `_links.self.href` | Référence URI de l’action marketing, qui peut être utilisée pour terminer le tableau `marketingActionsRefs` lors de la [création d’une stratégie d’utilisation des données](policies.md#create-policy). |

## Recherche d’une action marketing spécifique {#lookup}

Vous recherchez les détails d’une action marketing spécifique en incluant la propriété `name` de l’action marketing dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | La propriété `name` de l’action marketing que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère une action marketing personnalisée nommée `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet de réponse contient les détails de l’action marketing, y compris le chemin d’accès (`_links.self.href`) nécessaire pour référencer l’action marketing lorsque [vous définissez une stratégie d’utilisation des données](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
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

## Création ou mise à jour d’une action marketing {#create-update}

Vous pouvez créer une action marketing personnalisée ou mettre à jour une action marketing existante en incluant le nom existant ou prévu de l’action marketing dans le chemin d’accès d’une requête PUT.

**Format d’API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à créer ou à mettre à jour. Si une action marketing portant le nom fourni existe déjà dans le système, elle est mise à jour. S’il n’en existe pas, une action marketing est créée pour le nom fourni. |

**Requête**

La requête suivante crée une action marketing nommée `crossSiteTargeting`, à condition qu’une action marketing du même nom n’existe pas déjà dans le système. S’il existe une action marketing `crossSiteTargeting`, cet appel la met à jour à la place, en fonction des propriétés fournies dans la payload.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de l’action marketing à créer ou à mettre à jour. <br><br>**IMPORTANT** : cette propriété doit correspondre à la propriété `{MARKETING_ACTION_NAME}` du chemin d’accès. Autrement, une erreur HTTP 400 (Bad Request) apparaît. En d’autres termes, une fois qu’une action marketing a été créée, sa propriété `name` ne peut pas être modifiée. |
| `description` | Description facultative afin de fournir un contexte supplémentaire pour l’action marketing. |

**Réponse**

Une réponse réussie renvoie les détails de l’action marketing. Si une action marketing existante a été mise à jour, la réponse renvoie l’état HTTP 200 (OK). Si une nouvelle action marketing a été créée, la réponse renvoie l’état HTTP 201 (Created).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
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

## Suppression d’une action marketing {#delete}

Vous pouvez supprimer une action marketing personnalisée en incluant son nom dans le chemin d’une requête DELETE.

>[!NOTE]
>
>Les actions marketing référencées par des stratégies existantes ne peuvent pas être supprimées. Toute tentative de suppression de l’une de ces actions marketing provoquera une erreur HTTP 400 (Bad Request), ainsi qu’un message contenant les identifiants de toutes les stratégies qui font référence à l’action marketing.

**Format d’API**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 (OK) avec un corps de réponse vide.

Vous pouvez confirmer la suppression de l’action en essayant de [rechercher l’action marketing](#look-up). Vous recevez une erreur HTTP 404 (Not Found) lorsque l’action marketing a été supprimée du système.
