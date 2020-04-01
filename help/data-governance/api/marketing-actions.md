---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Actions marketing
topic: developer guide
translation-type: tm+mt
source-git-commit: 08d02e7323f75c450e7a250835f26a569685cdd1

---


# Actions marketing

Une action marketing, dans le contexte de la gouvernance des données d’Adobe Experience Platform, est une action que le consommateur de données d’Experience Platform effectue, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

Pour utiliser les actions marketing dans l’API, vous devez utiliser le `/marketingActions` point de fin.

## toutes les actions marketing

Pour  un de toutes les actions marketing, une requête GET peut être envoyée à `/marketingActions/core` ou `/marketingActions/custom` qui renvoie toutes les stratégies pour l’ spécifiée.

**Format API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Requête**

La requête suivante renvoie un  de toutes les actions marketing personnalisées définies par l’organisation IMS.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet response indique le nombre total d’actions marketing dans le  (`count`) du et le `children` tableau contient les détails de chaque action marketing, y compris les `name` et `href` les champs de l’action marketing. Ce chemin (`_links.self.href`) est utilisé pour terminer le `marketingActionsRefs` tableau lors de la [création d’une stratégie](policies.md#create-policy)d’utilisation des données.

```JSON
{
    "_page": {
        "start": "sampleMarketingAction",
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

## Rechercher une action marketing spécifique

Vous pouvez également effectuer une requête GET (recherche) pour les détails d’une action marketing spécifique. Cette opération est effectuée à l’aide `name` de l’action marketing. Si le nom est inconnu, il est possible de le trouver à l&#39;aide de la demande de liste (GET) présentée précédemment.

**Format API**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet response contient les détails de l’action marketing, y compris le chemin (`_links.self.href`) nécessaire pour référencer l’action marketing lors de la définition d’une stratégie d’utilisation des données (`marketingActionsRefs`).

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

## Création ou mise à jour d’une action marketing

L’API Service de stratégie vous permet de définir vos propres actions marketing, ainsi que de mettre à jour les actions existantes. La création et la mise à jour sont toutes deux effectuées à l’aide d’une opération PUT au nom de l’action marketing.

**Format API**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Requête**

Dans la requête qui suit, notez que la charge utile `name` dans la requête est la même que celle `{marketingActionName}` dans l’appel API. Contrairement à une stratégie générée par le système et en lecture seule, la création d’une action marketing requiert que vous fournissiez le nom `id` prévu __ de l’action marketing lors de sa création.

>[!NOTE] Si vous ne fournissez pas le fichier `{marketingActionName}` dans l’appel, une erreur 405 (méthode non autorisée) se produira, car vous n’êtes pas autorisé à effectuer directement un PUT sur le `/marketingActions/custom` point de fin. En outre, si la charge `name` dans la charge ne correspond pas à la `{marketingActionName}` valeur dans le chemin, vous recevrez une erreur 400 (mauvaise requête).

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**Réponse**

Si la création est réussie, vous recevrez un état HTTP 201 (Créé) et le corps de la réponse contiendra les détails de l’action marketing nouvellement créée. Le contenu `name` de la réponse doit correspondre à ce qui a été envoyé dans la requête.

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

## Suppression d’une action marketing

Il est possible de supprimer des actions marketing en envoyant une demande DELETE à l’action `{marketingActionName}` de marketing que vous souhaitez supprimer.

>[!NOTE] Vous ne pouvez pas supprimer les actions marketing référencées par des stratégies de sortie. Si vous tentez de le faire, une erreur 400 (mauvaise requête) s’affichera, ainsi qu’un message d’erreur qui comprend le `id` (ou plusieurs) ID(s) de toute stratégie(s) contenant une référence à l’action marketing que vous tentez de supprimer.

**Format API**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**Requête**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Si l’action marketing a bien été supprimée, le corps de la réponse est vide avec un état HTTP 200 (OK).

Vous pouvez confirmer la suppression en tentant de rechercher (GET) l’action marketing. Vous devez recevoir un message d’erreur HTTP Status 404 (Introuvable) ainsi qu’un message d’erreur &quot;Not Found&quot; (Non trouvé), car l’action marketing a été supprimée.
