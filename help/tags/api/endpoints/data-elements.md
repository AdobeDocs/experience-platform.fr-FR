---
title: Point d’entrée des éléments de données
description: Découvrez comment effectuer des appels au point d’entrée /data_elements dans l’API Reactor.
exl-id: ea346682-441b-415b-af06-094158eb7c71
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 99%

---

# Point d’entrée des éléments de données

Un élément de données fonctionne comme une variable qui pointe vers une donnée importante dans votre application. Les éléments de données sont utilisés dans les configurations [règles](./rules.md) et [extension](./extensions.md). Lorsqu’une règle est déclenchée au moment de l’exécution dans un navigateur ou une application, la valeur de l’élément de données est résolue et utilisée dans la règle. Les éléments de données fonctionnent de la même manière pour les configurations d’extension.

L’utilisation conjointe de plusieurs éléments de données génère un dictionnaire de données ou un mappage de données. Ce dictionnaire constitue les données connues et exploitables par Adobe Experience Platform.

Un élément de données appartient exactement à une [propriété](./properties.md). Une propriété peut comporter de nombreux éléments de données.

Pour des informations plus générales sur les éléments de données et leur utilisation dans les balises, consultez le [guide des éléments de données](../../ui/managing-resources/data-elements.md) dans la documentation de l’interface utilisateur.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

## Récupération d’une liste d’éléments de données {#list}

Vous pouvez récupérer une liste d’éléments de données pour une propriété en incluant l’identifiant de la propriété dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /properties/{PROPERTY_ID}/data_elements
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | `id` de la propriété appartenant aux éléments de données. |

{style="table-layout:auto"}

>[!NOTE]
>
>À l’aide des paramètres de requête, les éléments de données répertoriés peuvent être filtrés en fonction des attributs suivants :<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>Pour plus d’informations, consultez le guide sur le [filtrage des réponses](../guides/filtering.md).

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste d’éléments de données pour la propriété spécifiée.

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
        "name": "My Data Element 2020-12-14 17:36:08 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
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
        "latest_revision_number": 0
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

## Recherche d’un élément de données {#lookup}

Vous pouvez rechercher un élément de données en fournissant son identifiant dans le chemin d’accès d’une requête GET.

>[!NOTE]
>
>Lorsque des éléments de données sont supprimés, ils sont marqués comme supprimés, mais ils ne sont pas réellement supprimés du système. Il est donc possible de rechercher un élément de données supprimé. Les éléments de données supprimés peuvent être identifiés par la présence d’un attribut `data.meta.deleted_at`.

**Format d’API**

```http
GET /data_elements/{DATA_ELEMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `DATA_ELEMENT_ID` | Le `id` de l’élément de données que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de l&#39;élément de données.

```json
{
  "data": {
    "id": "DE8097636264104451ac3a18c95d5ff833",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:35:54.956Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:35:54 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:35:54.956Z",
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
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/property"
        },
        "data": {
          "id": "PRa5621686159f44c880557e12af412a95",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/origin"
        },
        "data": {
          "id": "DE8097636264104451ac3a18c95d5ff833",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/extension"
        },
        "data": {
          "id": "EX085a465793b54be39b5408d13b50b46e",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension"
        },
        "data": {
          "id": "EXf9a32699efde42e9b9410b43bd660848",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa5621686159f44c880557e12af412a95",
      "origin": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "self": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "extension": "https://reactor.adobe.io/extensions/EX085a465793b54be39b5408d13b50b46e"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Créer un élément de données {#create}

Vous pouvez créer un nouvel élément de données en effectuant une requête POST.

**Format d’API**

```http
POST /properties/{PROPERTY_ID}/data_elements
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | Le `id` de la [propriété](./properties.md) sous laquelle vous définissez l’élément de données. |

{style="table-layout:auto"}

**Requête**

La requête suivante crée un nouvel élément de données pour la propriété spécifiée. L’appel associe également l’élément de données à une extension existante par le biais de la propriété `relationships`. Pour plus d’informations, consultez le guide sur la [relation](../guides/relationships.md).

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Data Element 2020-12-14 17:33:21 +0000",
            "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
            "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}",
            "default_value": "general_label",
            "enabled": true,
            "force_lower_case": true,
            "clean_text": true,
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
                "type": "extensions"
              }
            }
          },
          "type": "data_elements"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes.name` | **(Obligatoire)** Nom lisible par l’utilisateur de l’élément de données. |
| `attributes.delegate_descriptor_id` | **(Obligatoire)** Chaîne formatée qui associe l’élément de données à un package d’extension. Tous les éléments de données doivent être associés à un package d’extension lors de leur première création, car chaque package d’extension définit les types compatibles pour ses éléments de données délégués, ainsi que leur comportement prévu. Pour plus d’informations, consultez le guide sur les [identifiants de descripteur délégué](../guides/delegate-descriptor-ids.md). |
| `attributes.settings` | Un objet JSON de paramétrage représenté sous la forme d’une chaîne. |
| `attributes.default_value` | Valeur par défaut à renvoyer si l’élément de données est évalué sur `undefined`. |
| `attributes.enabled` | Valeur booléenne indiquant si l’élément de données est activé. |
| `attributes.force_lower_case` | Valeur booléenne indiquant si la valeur de l’élément de données doit être convertie en minuscules avant d’être stockée. |
| `attributes.clean_text` | Valeur booléenne indiquant si les espaces de début et de fin doivent être supprimés de la valeur de l’élément de données avant d’être stockés. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `data_elements`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de l’élément de données nouvellement créé.

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Mettre à jour un élément de données {#update}

Vous pouvez mettre à jour un élément de données en incluant son identifiant dans le chemin d’accès d’une requête PATCH.

**Format d’API**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `DATA_ELEMENT_ID` | Le `id` de l’élément de données que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

La requête suivante met à jour `name` pour un élément de données existant.

```shell
curl -X PATCH \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes` | Objet dont les propriétés représentent les attributs à mettre à jour pour l’élément de données. Tous les attributs d’élément de données peuvent être mis à jour. Voir l’exemple d’appel pour [la création d’un élément de données](#create) pour une liste d’attributs et leur cas d’utilisation. |
| `id` | Le `id` de l&#39;élément de données que vous voulez à mettre à jour. Cela doit correspondre à la valeur `{DATA_ELEMENT_ID}` fournie dans le chemin de requête. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `data_elements`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de l&#39;élément de données mis à jour.

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Réviser un élément de données {#revise}

Lorsque vous révisez un élément de données, une nouvelle révision de l’élément de données est créée avec la révision actuelle (head). Chaque révision d’un élément de données possède son propre identifiant. L’élément de données d’origine peut être découvert par le biais d’un lien d’origine.

Vous pouvez réviser un élément de données en fournissant une propriété `meta.action` avec une valeur de `revise` dans le corps d’une requête PATCH.

**Format d’API**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `DATA_ELEMENT_ID` | Le `id` de l’élément de données que vous souhaitez réviser. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X PATCH \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "meta": {
            "action": "revise"
          },
          "id": "DE7d7284657ee540ee8f402277860e9f8a",
          "type": "data_elements"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes` | Objet dont les propriétés représentent les attributs à mettre à jour pour l’élément de données. Tous les attributs d’élément de données peuvent être mis à jour. Voir l’exemple d’appel pour [la création d’un élément de données](#create) pour une liste d’attributs et leur cas d’utilisation. |
| `meta.action` | Lorsqu’elle est incluse avec une valeur `revise`, cette propriété indique qu’une nouvelle révision doit être créée pour l’élément de données. |
| `id` | `id` de l’élément de données que vous souhaitez réviser. Cela doit correspondre à la valeur `{DATA_ELEMENT_ID}` fournie dans le chemin de requête. |
| `type` | Type de ressource en cours de révision. Pour ce point d’entrée, la valeur doit être `data_elements`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle révision de l’élément de données, comme indiqué par l’attribut `meta.latest_revision_number` incrémenté.

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## Supprimer un élément de données

Vous pouvez supprimer un élément de données en incluant son identifiant dans le chemin dʼaccès dʼune requête DELETE.

**Format d’API**

```http
DELETE /data_elements/{DATA_ELEMENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `DATA_ELEMENT_ID` | Le `id` de l’élément de données que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X DELETE \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content) sans corps de réponse, indiquant que l’élément de données a été supprimé.

## Gérer les notes d’un élément de données {#notes}

Les éléments de données sont des ressources « inscriptibles », ce qui signifie que vous pouvez créer et récupérer des notes textuelles sur chaque ressource. Pour plus d’informations sur la gestion des notes pour les éléments de données et d’autres ressources compatibles, reportez-vous au [guide de point d’entrée des notes](./notes.md).

## Récupérer les ressources associées pour un élément de données {#related}

Les appels suivants montrent comment récupérer les ressources associées pour un élément de données. Si [vous recherchez un élément de données](#lookup), ces relations sont répertoriées sous la propriété `relationships`.

Pour plus d’informations sur les relations dans l’API Reactor, consultez le [guide des relations](../guides/relationships.md).

### Liste des bibliothèques associées pour un élément de données {#libraries}

Vous pouvez répertorier les bibliothèques qui utilisent un élément de données en ajoutant `/libraries` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/libraries
```

| Paramètre | Description |
| --- | --- |
| `{DATA_ELEMENT_ID}` | Le `id` de l’élément de données dont vous souhaitez répertorier les bibliothèques. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de bibliothèques qui utilisent l’élément de données spécifié.

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

### Liste des révisions associées pour un élément de données {#revisions}

Vous pouvez répertorier les révisions précédentes d’un élément de données en ajoutant `/revisions` au chemin d&#39;accès d’une requête de recherche.

**Format d’API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/revisions
```

| Paramètre | Description |
| --- | --- |
| `{DATA_ELEMENT_ID}` | Le `id` de l’élément de données dont vous souhaitez répertorier les révisions. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de révisions pour l’élément de données spécifié.

```json
{
  "data": [
    {
      "id": "DEaeceb5164d494c768c18e37ec6f3b091",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:06.488Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:37:06.488Z",
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
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "DE5172417ff56e43d2a99ca149021bf65a",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:05.920Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:37:05.920Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

### Recherche de l’extension associée pour un élément de données {#extension}

Vous pouvez rechercher l’extension qui utilise un élément de données en ajoutant `/extension` au chemin d&#39;accès d’une requête GET.

**Format d’API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/extension
```

| Paramètre | Description |
| --- | --- |
| `{DATA_ELEMENT_ID}` | Le `id` de l’élément de données dont vous souhaitez rechercher l’extension. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de l’extension qui utilise l’élément de données spécifié.

```json
{
  "data": {
    "id": "EX9c7f9f1e826149978f2dadaf4c639679",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:37:31.952Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:31.952Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/property"
        },
        "data": {
          "id": "PR5c15543ef7bb403abc79d65fee0bf1f9",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/origin"
        },
        "data": {
          "id": "EX9c7f9f1e826149978f2dadaf4c639679",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5c15543ef7bb403abc79d65fee0bf1f9",
      "origin": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "self": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Recherche de l’origine associée pour un élément de données {#origin}

Vous pouvez rechercher l’origine d’un élément de données en ajoutant `/origin` au chemin d’une requête GET. L’origine d’un élément de données est la révision précédente qui a été mise à jour pour créer la révision actuelle.

**Format d’API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/origin
```

| Paramètre | Description |
| --- | --- |
| `{DATA_ELEMENT_ID}` | `id` de l’élément de données dont vous souhaitez rechercher l’origine. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de l’origine de l’élément de données spécifié.

```json
{
  "data": {
    "id": "DE790cb76f91594c2082a727b9f97024f6",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:37:19.891Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:37:19 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:19.891Z",
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
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/property"
        },
        "data": {
          "id": "PRf1ac400fb1e04c689e28d5efcd675c94",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/origin"
        },
        "data": {
          "id": "DE790cb76f91594c2082a727b9f97024f6",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/extension"
        },
        "data": {
          "id": "EX2345dba2c8b34d1cbe2795e29c62bf27",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension"
        },
        "data": {
          "id": "EXad7ebb72d721478483b741eebfffda6a",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRf1ac400fb1e04c689e28d5efcd675c94",
      "origin": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "self": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "extension": "https://reactor.adobe.io/extensions/EX2345dba2c8b34d1cbe2795e29c62bf27"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Recherche de la propriété associée pour un élément de données {#property}

Vous pouvez rechercher la propriété propriétaire d’un élément de données en ajoutant `/property` au chemin d’accès d’une requête GET.

**Format d’API**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/property
```

| Paramètre | Description |
| --- | --- |
| `{DATA_ELEMENT_ID}` | `id` de l’élément de données dont vous souhaitez rechercher la propriété. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de la propriété à laquelle l’élément de données spécifié appartient.

```json
{
  "data": {
    "id": "PRae9440b0f3234c4286569485f2b7a6a2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:40.829Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:40.829Z",
      "platform": "web",
      "development": false,
      "token": "42daac072e1e",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments",
      "extensions": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions",
      "rules": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules",
      "self": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
