---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Actions marketing
topic: developer guide
translation-type: tm+mt
source-git-commit: 08d02e7323f75c450e7a250835f26a569685cdd1
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---


# Actions marketing

Une action marketing, dans le contexte de la gouvernance des données de la plateforme Adobe Experience Platform, est une action entreprise par un utilisateur de données Experience Platform, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données.

Pour utiliser les actions marketing dans l’API, vous devez utiliser le `/marketingActions` point de terminaison.

## Liste de toutes les actions marketing

Pour vue d’une liste de toutes les actions marketing, une requête GET peut être envoyée à `/marketingActions/core` ou `/marketingActions/custom` qui renvoie toutes les stratégies pour le conteneur spécifié.

**Format d’API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Requête**

La requête suivante renvoie une liste de toutes les actions marketing personnalisées définies par l&#39;organisation IMS.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet response fournit le nombre total d’actions marketing dans le conteneur (`count`) et la `children` baie contient les détails de chaque action marketing, y compris les `name` et les `href` actions marketing. Ce chemin (`_links.self.href`) est utilisé pour terminer la `marketingActionsRefs` baie lors de la [création d&#39;une stratégie](policies.md#create-policy)d&#39;utilisation des données.

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

Vous pouvez également effectuer une demande de recherche (GET) pour vue les détails d’une action marketing spécifique. Cette opération est effectuée à l’aide `name` de l’action marketing. Si le nom est inconnu, il peut être trouvé à l&#39;aide de la demande d&#39;inscription (GET) présentée précédemment.

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

## Créer ou mettre à jour une action marketing

L’API Service de stratégie vous permet de définir vos propres actions marketing, ainsi que de mettre à jour les actions existantes. La création et la mise à jour sont toutes deux effectuées à l’aide d’une opération PUT sur le nom de l’action marketing.

**Format d’API**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Requête**

Dans la requête qui suit, notez que la charge utile `name` de la requête est la même que celle `{marketingActionName}` de l’appel API. Contrairement à une stratégie générée par le système et en lecture seule, la création d’une action marketing requiert que vous fournissiez le nom `id` prévu __ de l’action marketing au moment de sa création.

>[!NOTE] Si vous ne fournissez pas le `{marketingActionName}` contenu de l’appel, une erreur 405 (méthode non autorisée) se produira, car vous n’êtes pas autorisé à exécuter directement un PUT sur le `/marketingActions/custom` point de terminaison. En outre, si la charge `name` dans la charge ne correspond pas à la `{marketingActionName}` charge dans le chemin, vous recevrez une erreur 400 (mauvaise demande).

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

Si la création est réussie, vous recevrez un état HTTP 201 (créé) et le corps de la réponse contiendra les détails de l’action marketing nouvellement créée. Le `name` contenu de la réponse doit correspondre à ce qui a été envoyé dans la demande.

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

Il est possible de supprimer des actions marketing en envoyant une requête DELETE à l&#39;action marketing que vous souhaitez supprimer. `{marketingActionName}`

>[!NOTE] Vous ne pouvez pas supprimer les actions marketing référencées par des stratégies de sortie. Si vous essayez de le faire, une erreur 400 (mauvaise requête) s’affichera, ainsi qu’un message d’erreur qui comprend le `id` (ou plusieurs ID) d’une ou plusieurs stratégies contenant une référence à l’action marketing que vous tentez de supprimer.

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

Si l’action marketing a été correctement supprimée, le corps de la réponse est vide avec un état HTTP 200 (OK).

Vous pouvez confirmer la suppression en tentant de rechercher (GET) l’action marketing. Vous devez recevoir un état HTTP 404 (introuvable) accompagné d’un message d’erreur &quot;Non trouvé&quot;, car l’action marketing a été supprimée.
