---
keywords: Experience Platform ; accueil ; rubriques populaires ; Application des stratégies ; API des actions marketing ; Application basée sur les API ; gouvernance des données
solution: Experience Platform
title: Point de terminaison de l’API Actions marketing
topic-legacy: developer guide
description: Dans le cadre de la gouvernance des données Adobe Experience Platform, une action marketing est une action entreprise par un utilisateur de données Experience Platform pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 14%

---

# Point de terminaison des actions marketing

Une action marketing, dans le contexte de la Adobe Experience Platform [!DNL Data Governance], est une action entreprise par un utilisateur de données [!DNL Experience Platform], pour laquelle il est nécessaire de vérifier les violations des stratégies d&#39;utilisation des données.

Vous pouvez gérer les actions marketing pour votre organisation en utilisant le point de terminaison `/marketingActions` de l’API de service de stratégie.

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l&#39;[[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API [!DNL Experience Platform].

## Récupérer une liste d&#39;actions marketing {#list}

Vous pouvez récupérer une liste d’actions marketing de base ou personnalisées en adressant une demande de GET à `/marketingActions/core` ou `/marketingActions/custom`, respectivement.

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

Une réponse réussie renvoie les détails de chaque action marketing récupérée, y compris ses `name` et `href`. La valeur `href` est utilisée pour identifier l&#39;action marketing lorsque [crée une stratégie d&#39;utilisation des données](policies.md#create-policy).

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
| `name` | Nom de l’action marketing, qui agit comme identifiant unique lorsque [recherche une action marketing spécifique](#lookup). |
| `_links.self.href` | Référence URI pour l’action marketing, qui peut être utilisée pour terminer le tableau `marketingActionsRefs` lorsque [crée une stratégie d’utilisation des données](policies.md#create-policy). |

## Recherche d’une action marketing spécifique {#lookup}

Vous recherchez les détails d’une action marketing spécifique en incluant la propriété `name` de l’action marketing dans le chemin d’une demande de GET.

**Format d’API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | La propriété `name` de l&#39;action marketing que vous souhaitez rechercher. |

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

## Créer ou mettre à jour une action marketing personnalisée {#create-update}

Vous pouvez créer une action marketing personnalisée ou en mettre à jour une existante en incluant le nom existant ou prévu de l’action marketing dans le chemin d’une demande de PUT.

**Format d’API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing à créer ou à mettre à jour. Si une action marketing portant le nom fourni existe déjà dans le système, elle est mise à jour. S’il n’en existe pas, une nouvelle action marketing est créée pour le nom fourni. |

**Requête**

La requête suivante crée une nouvelle action marketing appelée `crossSiteTargeting`, à condition qu&#39;une action marketing du même nom n&#39;existe pas encore dans le système. S’il existe une action marketing `crossSiteTargeting`, cet appel met à jour cette action marketing en fonction des propriétés fournies dans la charge utile.

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
| `name` | Nom de l’action marketing à créer ou à mettre à jour. <br><br>**IMPORTANT** : Cette propriété doit correspondre à celle  `{MARKETING_ACTION_NAME}` du chemin d’accès, sinon une erreur HTTP 400 (Mauvaise requête) se produira. En d’autres termes, une fois qu’une action marketing a été créée, sa propriété `name` ne peut pas être modifiée. |
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

## Supprimer une action marketing personnalisée {#delete}

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

Vous pouvez confirmer la suppression en tentant de [rechercher l&#39;action marketing](#look-up). Vous devriez recevoir une erreur HTTP 404 (introuvable) si l’action marketing a été supprimée du système.
