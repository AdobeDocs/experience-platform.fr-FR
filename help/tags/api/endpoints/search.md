---
title: Point dʼentrée de recherche
description: Découvrez comment effectuer des appels vers le point dʼentrée /search dans lʼAPI Reactor.
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
TQID: https://experienceleague.adobe.com/zdBI249cv4BWflCTXBClxvi-zyLabGLwGaZ-rI1Glmc
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 9eb5b266c15495d852a671829d46fd127ad33ac9
workflow-type: tm+mt
source-wordcount: 673
ht-degree: 96%

---

# Point dʼentrée de recherche

Le point dʼentrée `/search` de lʼAPI Reactor permet de trouver des ressources correspondant aux critères souhaités, exprimés sous forme de requête.

Les types de ressources API suivants peuvent faire lʼobjet de recherches, au moyen de la même structure de données que les documents basés sur les ressources renvoyés par lʼAPI :

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

Toutes les requêtes sont limitées à votre entreprise actuelle et aux propriétés accessibles.

>[!IMPORTANT]
>
>La fonctionnalité de recherche comporte les avertissements et exceptions suivants :
>
>* meta ne peut faire lʼobjet de recherches et nʼest pas renvoyé dans les résultats de recherche.
>* Champs de schéma pour les délégués de packages d’extension (actions, conditions, etc.) peuvent faire l’objet de recherches sous forme de texte, et non de structure de données imbriquées.
>* Actuellement, les requêtes de plage ne prennent en charge que les nombres entiers.

Pour plus dʼinformations détaillées sur lʼutilisation de cette fonctionnalité, consultez le [guide de recherche](../guides/search.md).

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://developer.adobe.com/experience-platform-apis/references/reactor). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la procédure à suivre pour s’authentifier auprès de l’API.

## Exécution d’une recherche {#perform}

Vous pouvez effectuer une recherche en faisant une requête POST.

**Format d’API**

```http
POST /search
```

**Requête**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `from` | Nombre de résultats à décaler de la réponse. |
| `size` | Nombre maximal de résultats à renvoyer. Les résultats sont limités à 100 éléments. |
| `query` | Objet représentant la requête. Pour chaque propriété au sein de cet objet, la clé doit représenter un chemin du champ sur lequel portera la requête, et la valeur doit être un objet dont les sous-propriétés déterminent le contenu de la requête.<br><br>Pour chaque chemin du champ, vous pouvez utiliser les sous-propriétés suivantes :<ul><li>`exists` : renvoie « true » si le champ existe dans la ressource.</li><li>`value` : renvoie « true » si la valeur du champ correspond à la valeur de cette propriété.</li><li>`value_operator` : logique booléenne utilisée pour déterminer le traitement dʼune requête `value`. Les valeurs autorisées sont `AND` et `OR`. Lorsquʼelle est exclue, la logique `AND` est supposée. Pour plus dʼinformations, voir la section [Logique de lʼopérateur de valeur](#value-operator).</li><li>`range` Renvoie « true » si la valeur du champ se situe dans une plage numérique spécifique. La plage elle-même est déterminée par les sous-propriétés suivantes :<ul><li>`gt` : supérieure à la valeur fournie, non incluse.</li><li>`gte` : supérieure ou égale à la valeur fournie.</li><li>`lt` : inférieure à la valeur fournie, non incluse.</li><li>`lte` : inférieure ou égale à la valeur fournie.</li></ul></li></ul> |
| `sort` | Tableau dʼobjets indiquant lʼordre dans lequel trier les résultats. Chaque objet doit contenir une seule propriété : la clé représente le chemin du champ à trier et la valeur lʼordre de tri (`asc` pour lʼordre croissant et `desc` pour lʼordre décroissant). |
| `resource_types` | Tableau de chaînes indiquant les types de ressources spécifiques à rechercher. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie une liste de ressources correspondant à la requête. Pour plus dʼinformations sur la manière dont lʼAPI détermine les correspondances pour des valeurs spécifiques, reportez-vous à la section de lʼannexe sur les [conventions de correspondance](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## Annexe

La section suivante contient des informations supplémentaires sur lʼutilisation du point dʼentrée `/search`.

### Logique de lʼopérateur de valeur {#value-operator}

Les valeurs de requête sont séparées en termes afin dʼêtre comparées aux documents indexés. Entre chaque terme, une relation `AND` est supposée.

Lorsque vous utilisez `AND` comme `value_operator`, une valeur de requête `My Rule Holiday Sale` est interprétée comme des documents dont le champ contient `My AND Rule AND Holiday AND Sale`.

Lorsque vous utilisez `OR` comme `value_operator`, une valeur de requête `My Rule Holiday Sale` est interprétée comme des documents dont le champ contient `My OR Rule OR Holiday OR Sale`. Plus le nombre de termes correspondants est élevé, plus le `match_score` est élevé. En raison de la nature de la correspondance partielle des termes, lorsquʼaucune valeur ne correspond exactement à celle souhaitée, vous pouvez obtenir un jeu de résultats pour lequel la valeur ne correspond quʼà un niveau très élémentaire, comme quelques caractères de texte.

### Conventions de correspondance {#conventions}

La recherche consiste à déterminer dans quelle mesure un document est pertinent par rapport à une requête fournie. La manière dont les données des documents sont analysées et indexées a un impact direct sur ce processus.

Le tableau suivant détaille les conventions de correspondance pour les types de champs les plus courants :

| Type de champ | Conventions de correspondance |
| --- | --- |
| Chaînes | Texte avec une analyse partielle des termes, non sensible à la casse |
| Valeurs Enum | Correspondance exacte, sensible à la casse |
| Nombres entiers | Correspondance exacte |
| Nombres à virgule flottante | Correspondance exacte |
| Horodatages | Correspondance exacte (format date et heure) |
| Noms d’affichage | Texte avec une analyse partielle des termes, non sensible à la casse |

Il existe aussi dʼautres conventions propres à des champs spécifiques qui apparaissent dans lʼAPI :

| Champ | Conventions de correspondance |
| --- | --- |
| `id` | Correspondance exacte, sensible à la casse |
| `delegate_descriptor_id` | Correspondance exacte, sensible à la casse, avec les termes séparés sur `::` |
| `name` | Correspondance exacte, sensible à la casse |
| `settings` | Texte avec une analyse partielle des termes, non sensible à la casse |
| `type` | Correspondance exacte, sensible à la casse |
