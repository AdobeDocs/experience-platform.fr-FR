---
title: Point de terminaison Notes
description: Découvrez comment effectuer des appels au point de terminaison /notes dans l’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 8%

---

# Point de terminaison Notes

Dans l’API Reactor, les notes sont des annotations textuelles que vous pouvez ajouter à certaines ressources. Les notes sont essentiellement des commentaires sur leurs ressources respectives. Le contenu des notes n’a aucun impact sur le comportement des ressources et peut être utilisé dans divers cas d’utilisation, notamment :

* Fournir des informations générales
* Fonctionnement en tant que listes de tâches
* Transmission de conseils sur l’utilisation des ressources
* Donner des instructions à d’autres membres de l’équipe
* Enregistrement du contexte historique

Le point d’entrée `/notes` de l’API Reactor vous permet de gérer ces notes par programmation.

Les notes peuvent être appliquées aux ressources suivantes :

* [Éléments de données](./data-elements.md)
* [Extensions](./extensions.md)
* [Bibliothèques](./libraries.md)
* [Propriétés](./properties.md)
* [Composants de  règle](./rule-components.md)
* [Règles](./rules.md)

Ces six types de ressources sont communément appelés ressources &quot;remarquables&quot;. Lorsqu’une ressource notable est supprimée, ses notes associées sont également supprimées.

>[!NOTE]
>
>Pour les ressources qui peuvent avoir plusieurs révisions, toute note doit être créée sur la révision actuelle (head). Elles ne peuvent pas être jointes à d’autres révisions.
>
>Toutefois, les notes peuvent toujours être lues à partir des révisions. Dans ce cas, l’API renvoie uniquement les notes qui existaient avant la création de la révision. Elles fournissent un instantané des annotations telles qu’elles étaient lorsque la révision a été coupée. En revanche, la lecture de notes de la révision actuelle (head) renvoie toutes ses notes.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’[API Reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

## Récupération d’une liste de notes {#list}

Vous pouvez récupérer une liste de notes pour une ressource en ajoutant `/notes` au chemin d’accès d’une demande de GET pour la ressource en question.

**Format d&#39;API**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Paramètre | Description |
| --- | --- |
| `RESOURCE_TYPE` | Type de ressource pour lequel vous récupérez des notes. Doit être l’une des valeurs suivantes : <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | `id` de la ressource spécifique dont vous souhaitez répertorier les notes. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante répertorie les notes jointes à une bibliothèque.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de notes jointes à la ressource spécifiée.

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
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

## Rechercher une note {#lookup}

Vous pouvez rechercher une note en fournissant son identifiant dans le chemin d’accès d’une demande de GET.

**Format d&#39;API**

```http
GET /notes/{NOTE_ID}
```

| Paramètre | Description |
| --- | --- |
| `NOTE_ID` | `id` de la note que vous souhaitez rechercher. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de la note.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## Création d’une note {#create}

>[!WARNING]
>
>Avant de créer une nouvelle note, gardez à l’esprit que les notes ne sont pas modifiables et que la seule façon de les supprimer est de supprimer la ressource correspondante.

Vous pouvez créer une nouvelle note en ajoutant `/notes` au chemin d’accès d’une requête de POST pour la ressource en question.

**Format d&#39;API**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Paramètre | Description |
| --- | --- |
| `RESOURCE_TYPE` | Type de ressource pour lequel vous créez une note. Doit être l’une des valeurs suivantes : <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | `id` de la ressource spécifique pour laquelle vous souhaitez créer une note. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante crée une nouvelle note pour une propriété.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `type` | **(Obligatoire)** Type de ressource mise à jour. Pour ce point de terminaison, la valeur doit être `notes`. |
| `attributes.text` | **(Obligatoire)** Texte qui comprend la note. Chaque note est limitée à 512 caractères Unicode. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle note créée.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
