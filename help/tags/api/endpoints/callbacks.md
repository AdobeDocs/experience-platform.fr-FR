---
title: Point dʼentrée des rappels
description: Découvrez comment effectuer des appels vers le point dʼentrée /callbacks dans lʼAPI Reactor.
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 97%

---

# Point dʼentrée des rappels

Un rappel est un message que lʼAPI Reactor envoie à une URL spécifique (généralement une URL hébergée par votre organisation).

Les rappels sont destinés à être utilisés conjointement avec les [événements dʼaudit](./audit-events.md) afin dʼeffectuer le suivi des activités dans lʼAPI Reactor. Chaque fois quʼun événement dʼaudit dʼun certain type est généré, un rappel peut envoyer un message correspondant à lʼURL spécifiée.

Le service derrière lʼURL spécifiée dans le rappel doit répondre avec le code dʼétat HTTP 200 (OK) ou 201 (Created). Si le service ne répond avec aucun de ces codes dʼétat, la remise du message est à nouveau tentée aux intervalles suivants :

* 1 minute
* 5 minutes
* 30 minutes
* 1 heure
* 12 heures
* 1 jour
* 3 jours

>[!NOTE]
>
>Les intervalles ayant subi une nouvelle tentative dépendent de lʼintervalle précédent. Par exemple, si la nouvelle tentative échoue à une minute, la tentative suivante est planifiée cinq minutes après lʼéchec de la tentative à une minute (six minutes après la génération du message).

Si toutes les tentatives de remise du message échouent, le message est rejeté.

Un rappel appartient à une seule [propriété](./properties.md). Une propriété peut posséder de nombreux rappels.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la manière de sʼauthentifier auprès de lʼAPI.

## Liste des rappels {#list}

Vous pouvez répertorier tous les rappels appartenant à une propriété en effectuant une requête GET.

**Format d’API**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez répertorier les rappels. |

{style="table-layout:auto"}

>[!NOTE]
>
>À lʼaide des paramètres de requête, les rappels répertoriés peuvent être filtrés en fonction des attributs suivants :<ul><li>`created_at`</li><li>`updated_at`</li></ul>Pour plus d’informations, consultez le guide sur le [filtrage des réponses](../guides/filtering.md).

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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

## Recherche dʼun rappel {#lookup}

Vous pouvez rechercher un rappel en fournissant son identifiant dans le chemin dʼaccès dʼune requête GET.

**Format d’API**

```http
GET /callbacks/{CALLBACK_ID}
```

| Paramètre | Description |
| --- | --- |
| `CALLBACK_ID` | Champ `id` du rappel que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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

## Création dʼun rappel {#create}

Vous pouvez créer un rappel en effectuant une requête POST.

**Format d’API**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | Champ `id` de la [propriété](./properties.md) sous laquelle vous définissez le rappel. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
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
| `url` | Destination URL du message de rappel. LʼURL doit utiliser lʼextension de protocole HTTPS. |
| `subscriptions` | Tableau de chaînes indiquant les types dʼévénements dʼaudit qui déclencheront le rappel. Pour obtenir la liste des types dʼévénements possibles, reportez-vous au [guide du point dʼentrée des événements dʼaudit](./audit-events.md). |

{style="table-layout:auto"}

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

## Mise à jour dʼun rappel

Vous pouvez mettre à jour un rappel en incluant son identifiant dans le chemin d’accès d’une requête de PATCH.

**Format d’API**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| Paramètre | Description |
| --- | --- |
| `CALLBACK_ID` | Champ `id` du rappel que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

La requête suivante met à jour le tableau `subscriptions` dʼun rappel existant.

```shell
curl -X PATCH \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.net",
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
| `attributes` | Objet dont les propriétés représentent les attributs à mettre à jour pour le rappel. Chaque clé représente lʼattribut de rappel particulier à mettre à jour, ainsi que la valeur correspondante vers laquelle il doit être mis à jour.<br><br>Les attributs suivants peuvent être mis à jour pour les rappels :<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | Champ `id` du rappel que vous souhaitez mettre à jour. Cela doit correspondre à la valeur `{CALLBACK_ID}` fournie dans le chemin dʼaccès à la demande. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `callbacks`. |

{style="table-layout:auto"}

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

## Suppression dʼun rappel

Vous pouvez supprimer un rappel en incluant son identifiant dans le chemin dʼaccès dʼune requête DELETE.

**Format d’API**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Paramètre | Description |
| --- | --- |
| `CALLBACK_ID` | Champ `id` du rappel que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content) sans corps de réponse, indiquant que le rappel a été supprimé.
