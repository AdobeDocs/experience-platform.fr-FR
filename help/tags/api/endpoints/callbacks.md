---
title: Point de terminaison des rappels
description: Découvrez comment effectuer des appels vers le point de terminaison /callbacks dans l’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# Point de terminaison des rappels

Un rappel est un message que l’API Reactor envoie à une URL spécifique (généralement une URL hébergée par votre organisation).

Les rappels sont destinés à être utilisés conjointement avec les [événements d’audit](./audit-events.md) pour effectuer le suivi des activités dans l’API Reactor. Chaque fois qu’un événement d’audit d’un certain type est généré, un rappel peut envoyer un message correspondant à l’URL spécifiée.

Le service derrière l’URL spécifiée dans le rappel doit répondre avec le code d’état HTTP 200 (OK) ou 201 (Created). Si le service ne répond avec aucun de ces codes d’état, la diffusion du message est retentée aux intervalles suivants :

* 1 minute
* 5 minutes
* 30 minutes
* 1 heure
* 12 heures
* 1 jour
* 3 jours

>[!NOTE]
>
>Les intervalles de reprise sont relatifs à l’intervalle précédent. Par exemple, si la nouvelle tentative échoue à une minute, la tentative suivante est planifiée pendant cinq minutes après l’échec de la tentative d’une minute (six minutes après la génération du message).

Si toutes les tentatives de diffusion échouent, le message est ignoré.

Un rappel appartient exactement à une [propriété](./properties.md). Une propriété peut comporter de nombreux rappels.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’[API Reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

## Rappels de liste {#list}

Vous pouvez répertorier tous les rappels sous une propriété en effectuant une requête de GET.

**Format d&#39;API**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez répertorier les rappels. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>À l’aide des paramètres de requête, les rappels répertoriés peuvent être filtrés en fonction des attributs suivants :<ul><li>`created_at`</li><li>`updated_at`</li></ul>Pour plus d’informations, consultez le guide sur le [filtrage des réponses](../guides/filtering.md) .

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de rappels pour la propriété spécifiée.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Recherche d’un rappel {#lookup}

Vous pouvez rechercher un rappel en fournissant son identifiant dans le chemin d’accès d’une requête de GET.

**Format d&#39;API**

```http
GET /callbacks/{CALLBACK_ID}
```

| Paramètre | Description |
| --- | --- |
| `CALLBACK_ID` | `id` du rappel que vous souhaitez rechercher. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails du rappel.

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## Création d’un rappel {#create}

Vous pouvez créer un rappel en effectuant une requête de POST.

**Format d&#39;API**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | `id` de la [propriété](./properties.md) sous laquelle vous définissez le rappel. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `url` | Destination de l’URL du message de rappel. L’URL doit utiliser l’extension de protocole HTTPS. |
| `subscriptions` | Tableau de chaînes indiquant les types d’événements de contrôle qui déclencheront le rappel. Pour obtenir la liste des types d’événements possibles, reportez-vous au [guide de point de terminaison des événements de contrôle](./audit-events.md) . |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails du rappel que vous venez de créer.

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## Mise à jour d’un rappel

Vous pouvez mettre à jour un rappel en incluant son identifiant dans le chemin d’accès d’une requête de PUT.

**Format d&#39;API**

```http
PUT /callbacks/{CALLBACK_ID}
```

| Paramètre | Description |
| --- | --- |
| `CALLBACK_ID` | `id` du rappel que vous souhaitez mettre à jour. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante met à jour le tableau `subscriptions` pour un rappel existant.

```shell
curl -X PUT \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes` | Objet dont les propriétés représentent les attributs à mettre à jour pour le rappel. Chaque clé représente l’attribut de rappel particulier à mettre à jour, ainsi que la valeur correspondante vers laquelle il doit être mis à jour.<br><br>Les attributs suivants peuvent être mis à jour pour les rappels :<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | `id` du rappel que vous souhaitez mettre à jour. Cela doit correspondre à la valeur `{CALLBACK_ID}` fournie dans le chemin de requête. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point de terminaison, la valeur doit être `callbacks`. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails du rappel mis à jour.

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## Suppression d’un rappel

Vous pouvez supprimer un rappel en incluant son identifiant dans le chemin d’accès d’une requête de DELETE.

**Format d&#39;API**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Paramètre | Description |
| --- | --- |
| `CALLBACK_ID` | `id` du rappel que vous souhaitez supprimer. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content) sans corps de réponse, indiquant que le rappel a été supprimé.
