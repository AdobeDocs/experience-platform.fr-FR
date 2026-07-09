---
title: Point dʼentrée des notes
description: Découvrez comment effectuer des appels au point dʼentrée /notes dans lʼAPI Reactor.
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
TQID: https://experienceleague.adobe.com/lBdOgFlp6aM1wB2UK8xDZis2HXTKgKCE4z21yplUDo0
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2: id: bef6f891-2e8a-425e-8f99-7ddf22070daaid: c132d929-fa62-4271-803e-b823be07b914id: e08599ea-8888-4294-ba74-3ba0a7762a46id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 9eb5b266c15495d852a671829d46fd127ad33ac9
workflow-type: tm+mt
source-wordcount: 520
ht-degree: 98%

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

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://developer.adobe.com/experience-platform-apis/references/reactor). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la manière de sʼauthentifier auprès de lʼAPI.

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
