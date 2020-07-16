---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Actions marketing
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 90%

---


# Actions marketing

A marketing action, in the context of the Adobe Experience Platform [!DNL Data Governance], is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies.

Pour pouvoir travailler avec les actions marketing dans l’API, vous devez utiliser le point de terminaison `/marketingActions`.

## Répertorier toutes les actions marketing

Pour afficher une liste de toutes les actions marketing, vous pouvez envoyer une requête GET à `/marketingActions/core` ou `/marketingActions/custom`, qui renvoie toutes les stratégies pour le conteneur spécifié.

**Format d’API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Requête**

La requête suivante renverra une liste de toutes les actions marketing définies par l’organisation IMS.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet de réponse indique le nombre total d’actions marketing dans le conteneur (`count`) et le tableau `children` contient les détails de chaque action marketing, notamment le `name` et un `href` pour l’action marketing. Ce chemin d’accès (`_links.self.href`) est utilisé pour compléter le tableau `marketingActionsRefs` lors de la [création d’une stratégie d’utilisation des données](policies.md#create-policy).

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

## Recherche d’une action marketing spécifique

Vous pouvez également effectuer une requête de recherche (GET) pour afficher les détails d’une action marketing spécifique. Cette opération s’effectue à l’aide du `name` de l’action marketing. Si vous n’en connaissez pas le nom, vous pouvez trouver celui-ci à l’aide de la requête de liste (GET) affichée précédemment.

**Format d’API**

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

L’objet de réponse contient les détails de l’action marketing, y compris le chemin d’accès (`_links.self.href`) nécessaire pour référencer l’action marketing lorsque vous définissez une stratégie d’utilisation des données (`marketingActionsRefs`).

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

The [!DNL Policy Service] API allows you to define your own marketing actions, as well as update existing ones. La création et la mise à jour sont toutes deux effectuées à l’aide d’une opération PUT au nom de l’action marketing.

**Format d’API**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Requête**

Dans la requête qui suit, notez que le `name` du payload de la requête est le même que le `{marketingActionName}` dans l’appel API. Contrairement à l’`id` d’une stratégie qui est en lecture seule et généré par le système, la création d’une action marketing nécessite que vous fournissiez le nom _attendu_ de l’action marketing à sa création.

>[!NOTE]
>
> L’impossibilité à fournir le `{marketingActionName}` dans l’appel entraînera une erreur 405 (Method Not Allowed), car vous n’êtes pas autorisé à effectuer directement une requête PUT sur le point de terminaison `/marketingActions/custom`. En outre, si le `name` dans le payload ne correspond pas au `{marketingActionName}` dans le chemin d’accès, vous recevrez une erreur 400 (Bad Request).

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

Si la création est réussie, vous recevez un état HTTP 201 (Created) et le corps de la réponse contient les détails de l’action marketing que vous venez de créer. Le `name` de la réponse doit correspondre à celui envoyé dans la requête.

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

Il est possible de supprimer des actions marketing en envoyant une requête DELETE sur le `{marketingActionName}` de l’action marketing que vous souhaitez supprimer.

>[!NOTE]
>
>Vous ne pouvez pas supprimer des actions marketing auxquelles des stratégies existantes font référence. Si vous tentez de le faire, vous recevrez une erreur 400 (Bad Request) ainsi qu’un message d’erreur incluant l’`id` (ou plusieurs identifiants) d’une stratégie (ou stratégies) contenant une référence à l’action marketing que vous essayez de supprimer.

**Format d’API**

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

Si l’action marketing a bien été supprimée, le corps de la réponse sera vide avec un état HTTP 200 (OK).

Vous pouvez confirmer la suppression de l’action en la recherchant à l’aide de GET. Vous devriez recevoir un état HTTP 404 (Not Found), ainsi qu’un message d’erreur indiquant que l’action marketing est introuvable, puisqu’elle a été supprimée.
