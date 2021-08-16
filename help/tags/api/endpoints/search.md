---
title: Point de terminaison de recherche
description: Découvrez comment effectuer des appels vers le point de terminaison /search dans l’API Reactor.
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 2%

---

# Point de terminaison de recherche

Le point d’entrée `/search` de l’API Reactor permet de trouver des ressources correspondant aux critères souhaités, exprimés sous forme de requête.

Les types de ressources d’API suivants peuvent faire l’objet de recherches, en utilisant la même structure de données que les documents basés sur les ressources renvoyés dans l’API :

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

Toutes les requêtes sont incluses dans la portée de votre société actuelle et les propriétés accessibles.

>[!IMPORTANT]
>
>La fonctionnalité de recherche comporte les avertissements et exceptions suivants :
>* meta n’est pas consultable et n’est pas renvoyé dans les résultats de recherche.
>* Champs de schéma pour les délégués de package d’extension (actions, conditions, etc.) peuvent faire l’objet de recherches sous forme de texte, et non en tant que structure de données imbriquées.
>* Actuellement, les requêtes de plage ne prennent en charge que les entiers.


Pour plus d’informations sur l’utilisation de cette fonctionnalité, consultez le [guide de recherche](../guides/search.md).

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’[API Reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

## Exécution d’une recherche {#perform}

Vous pouvez effectuer une recherche en effectuant une requête de POST.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
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
| `from` | Le nombre de résultats à décaler de la réponse. |
| `size` | Nombre maximal de résultats à renvoyer. Les résultats ne doivent pas dépasser 100 éléments. |
| `query` | Objet représentant la requête de recherche. Pour chaque propriété de cet objet, la clé doit représenter un chemin d’accès au champ à partir duquel effectuer la requête, et la valeur doit être un objet dont les sous-propriétés déterminent ce pour quoi effectuer la requête.<br><br>Pour chaque chemin d’accès au champ, vous pouvez utiliser les sous-propriétés suivantes :<ul><li>`exists`: Renvoie &quot;true&quot; si le champ existe dans la ressource.</li><li>`value`: Renvoie true si la valeur du champ correspond à la valeur de cette propriété.</li><li>`value_operator`: Logique booléenne utilisée pour déterminer le traitement d’une  `value` requête. Les valeurs autorisées sont `AND` et `OR`. Lorsqu’elle est exclue, la logique `AND` est supposée. Voir la section [logique de l’opérateur de valeur](#value-operator) pour plus d’informations.</li><li>`range` Renvoie &quot;true&quot; si la valeur du champ correspond à une plage numérique spécifique. La plage elle-même est déterminée par les sous-propriétés suivantes :<ul><li>`gt`: Supérieur à la valeur fournie, non incluse.</li><li>`gte`: Supérieur ou égal à la valeur fournie.</li><li>`lt`: Inférieur à la valeur fournie, non incluse.</li><li>`lte`: Inférieur ou égal à la valeur fournie.</li></ul></li></ul> |
| `sort` | Tableau d’objets indiquant l’ordre dans lequel trier les résultats. Chaque objet doit contenir une seule propriété : la clé représente le chemin d’accès au champ à trier, et la valeur représente l’ordre de tri (`asc` pour l’ordre croissant, `desc` pour l’ordre décroissant). |
| `resource_types` | Tableau de chaînes indiquant les types de ressources spécifiques à rechercher. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie une liste de ressources correspondantes pour la requête. Pour plus d’informations sur la manière dont l’API détermine les correspondances pour des valeurs spécifiques, reportez-vous à la section de l’annexe sur les [conventions correspondantes](#conventions).

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

La section suivante contient des informations supplémentaires sur l’utilisation du point de terminaison `/search`.

### Logique de l’opérateur de valeur {#value-operator}

Les valeurs de requête de recherche sont fractionnées en termes pour correspondre aux documents indexés. Entre chaque terme, une relation `AND` est supposée.

Lorsque vous utilisez `AND` comme `value_operator`, une valeur de requête `My Rule Holiday Sale` est interprétée comme des documents avec un champ contenant `My AND Rule AND Holiday AND Sale`.

Lorsque vous utilisez `OR` comme `value_operator`, une valeur de requête `My Rule Holiday Sale` est interprétée comme des documents avec un champ contenant `My OR Rule OR Holiday OR Sale`. Plus la correspondance est élevée, plus `match_score` est élevé. En raison de la nature de la correspondance partielle des termes, lorsque rien ne correspond exactement à la valeur souhaitée, vous pouvez obtenir un jeu de résultats pour lequel la valeur n’est trouvée qu’à un niveau très élémentaire, comme quelques caractères de texte.

### Correspondance de conventions {#conventions}

La recherche consiste à répondre à la pertinence d’un document par rapport à une requête fournie. La manière dont les données du document sont analysées et indexées affecte directement cette situation.

Le tableau suivant ventile les conventions de correspondance pour les types de champ courants :

| Type de champ | Conventions de correspondance |
| --- | --- |
| Chaînes | Texte avec analyse de terme partielle, non-respect de la casse |
| Valeurs d’énumération | Correspondance exacte, respect de la casse |
| Entiers | Correspondance exacte |
| Flottes | Correspondance exacte |
| Horodatages | Correspondance exacte (format DateTime ) |
| Noms d’affichage | Texte avec analyse de terme partielle, non-respect de la casse |

Il existe d’autres conventions pour des champs spécifiques qui apparaissent dans l’API :

| Champ | Conventions de correspondance |
| --- | --- |
| `id` | Correspondance exacte, respect de la casse |
| `delegate_descriptor_id` | Correspondance exacte, sensible à la casse, avec des termes fractionnés sur `::` |
| `name` | Correspondance exacte, respect de la casse |
| `settings` | Texte avec analyse de terme partielle, non-respect de la casse |
| `type` | Correspondance exacte, respect de la casse |