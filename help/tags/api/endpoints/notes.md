---
title: Point dʼentrée des notes
description: Découvrez comment effectuer des appels au point dʼentrée /notes dans lʼAPI Reactor.
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 99%

---

# Point dʼentrée des notes

Dans lʼAPI Reactor, les notes sont des annotations textuelles que vous pouvez ajouter à certaines ressources. Les notes sont essentiellement des commentaires sur leurs ressources respectives. Le contenu des notes nʼa aucun impact sur le comportement des ressources et peut être utilisé dans divers cas dʼutilisation, notamment :

* Fournir des informations générales
* Faire office de listes de tâches
* Transmettre des conseils sur l’utilisation des ressources
* Donner des instructions aux autres membres de lʼéquipe
* Enregistrer le contexte historique

Le point dʼentrée `/notes` de lʼAPI Reactor vous permet de gérer ces notes par programmation.

Des notes peuvent être appliquées aux ressources suivantes :

* [Éléments de données](./data-elements.md)
* [Extensions](./extensions.md)
* [Bibliothèques](./libraries.md)
* [Propriétés](./properties.md)
* [Composants de règle](./rule-components.md)
* [Règles](./rules.md)
* [Secrets](./secrets.md)

Ces six types de ressources sont communément appelés ressources « annotables ». Lorsquʼune ressource annotable est supprimée, ses notes associées le sont également.

>[!NOTE]
>
>Pour les ressources disposant de plusieurs révisions, les notes doivent être créées sur la révision actuelle (head). Elles ne peuvent pas être jointes à dʼautres révisions.
>
>Toutefois, les notes peuvent toujours être lues à partir des révisions. Dans de tels cas, lʼAPI renvoie uniquement les notes qui existaient avant la création de la révision. Elles fournissent un instantané des annotations telles quʼelles étaient au moment où la révision a été effectuée. En revanche, la lecture de notes de la révision actuelle (head) renvoie toutes ses notes.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la manière de sʼauthentifier auprès de lʼAPI.

## Récupération dʼune liste de notes {#list}

Vous pouvez récupérer une liste de notes dʼune ressource en ajoutant `/notes` au chemin dʼaccès dʼune requête GET de la ressource en question.

**Format d’API**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Paramètre | Description |
| --- | --- |
| `RESOURCE_TYPE` | Type de ressource pour lequel vous récupérez des notes. Doit être lʼune des valeurs suivantes : <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | `id` de la ressource spécifique dont vous souhaitez répertorier les notes. |

{style="table-layout:auto"}

**Requête**

La requête suivante répertorie les notes jointes à une bibliothèque.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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

## Recherche dʼune note {#lookup}

Vous pouvez rechercher une note en indiquant son identifiant dans le chemin dʼaccès dʼune requête GET.

**Format d’API**

```http
GET /notes/{NOTE_ID}
```

| Paramètre | Description |
| --- | --- |
| `NOTE_ID` | Champ `id` de la note que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
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
>Avant de créer une note, gardez à lʼesprit que les notes ne sont pas modifiables et que la seule façon de les supprimer est de supprimer la ressource correspondante.

Vous pouvez créer une note en ajoutant `/notes` au chemin dʼaccès dʼune requête POST de la ressource en question.

**Format d’API**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Paramètre | Description |
| --- | --- |
| `RESOURCE_TYPE` | Type de ressource pour lequel vous créez une note. Doit être lʼune des valeurs suivantes : <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | Champ `id` de la ressource spécifique pour laquelle vous souhaitez créer une note. |

{style="table-layout:auto"}

**Requête**

La requête suivante crée une note pour une propriété.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | **(Obligatoire)** Type de ressource mis à jour. Pour ce point dʼentrée, la valeur doit être `notes`. |
| `attributes.text` | **(Obligatoire)** Texte qui comprend la note. Chaque note est limitée à 512 caractères Unicode. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la note créée.

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
