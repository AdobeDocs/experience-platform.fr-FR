---
title: Point d’entrée de versions
description: Découvrez comment effectuer des appels vers le point d’entrée /versions dans l’API Reactor.
exl-id: 476abea0-efff-478a-b87f-ef6b91bfcca5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 100%

---

# Point d’entrée de versions

Les extensions, les règles et les éléments de données sont les blocs de construction des balises dans Adobe Experience Platform. Lorsque vous souhaitez que votre application fasse quelque chose, ces blocs de construction sont ajoutés à une [bibliothèque](./libraries.md). Pour déployer une bibliothèque sur votre application d’expérience, cette bibliothèque est compilée dans une version. Le point d’entrée `/builds` de l’API Reactor vous permet de gérer par programmation les versions de votre application d’expérience.

Une version est constituée du ou des fichiers chargés dans votre application web et mobile. Le contenu de chaque version varie en fonction des facteurs suivants :

* Ressources incluses dans la bibliothèque
* Configuration de l’[environnement](./environments.md) dans lequel la bibliothèque est créée.
* Plateforme de la [propriété](./properties.md) à laquelle appartient la version.

Une version appartient exactement à une seule bibliothèque. Une bibliothèque peut posséder plusieurs versions.

Pour plus d’informations sur les versions et leur compatibilité avec le processus de publication des flux de travaux pour Balises, reportez-vous à la [présentation de la publication](../../ui/publishing/overview.md).

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la procédure à suivre pour s’authentifier auprès de l’API.

## Récupération dʼune liste de versions {#list}

Vous pouvez répertorier les versions d’une bibliothèque spécifique en incluant l’identifiant de la bibliothèque dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /libraries/{LIBRARY_ID}/builds
```

| Paramètre | Description |
| --- | --- |
| `LIBRARY_ID` | `id` de la bibliothèque dont vous souhaitez répertorier les versions. |

{style="table-layout:auto"}

>[!NOTE]
>
>À l’aide des paramètres de requête, les versions répertoriées peuvent être filtrées en fonction des attributs suivants :<ul><li>`created_at`</li><li>`status`</li><li>`token`</li><li>`updated_at`</li></ul>Consultez le guide sur le [filtrage des réponses](../guides/filtering.md) pour plus d&#39;informations.

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBad32d71feff844b7b5a11dd0bf030964/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de versions pour la bibliothèque spécifiée.

```json
{
  "data": [
    {
      "id": "BL654195b78ac84f00b633a0ef4cdde484",
      "type": "builds",
      "attributes": {
        "created_at": "2020-12-14T17:32:29.002Z",
        "status": "pending",
        "updated_at": "2020-12-14T17:32:29.002Z",
        "token": "83407e650dbf"
      },
      "relationships": {
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/rules"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/environment"
          },
          "data": {
            "id": "EN7d73baa7b287421685a3ba5a447754df",
            "type": "environments"
          }
        },
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/library"
          },
          "data": {
            "id": "LBad32d71feff844b7b5a11dd0bf030964",
            "type": "libraries"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484/property"
          },
          "data": {
            "id": "PR7dbf185ba81f4698811f6e650c862492",
            "type": "properties"
          }
        }
      },
      "links": {
        "environment": "https://reactor.adobe.io/environments/EN7d73baa7b287421685a3ba5a447754df",
        "library": "https://reactor.adobe.io/libraries/LBad32d71feff844b7b5a11dd0bf030964",
        "self": "https://reactor.adobe.io/builds/BL654195b78ac84f00b633a0ef4cdde484"
      },
      "meta": {
        "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/bf45601a3b3d/launch-678767d5a218-development.min.js",
        "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/bf45601a3b3d/83407e650dbf/launch-678767d5a218-development.min.js",
        "archive": false,
        "host_type_of": "akamai"
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

## Recherche d’une version {#lookup}

Vous pouvez rechercher une version en fournissant son identifiant dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /builds/{BUILD_ID}
```

| Paramètre | Description |
| --- | --- |
| `BUILD_ID` | Champ `id` de la version que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de la version.

```json
{
  "data": {
    "id": "BL8238895201d548718bda2d0bf2b83467",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:32:14.671Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:32:14.671Z",
      "token": "ae8c9574e8d4"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/environment"
        },
        "data": {
          "id": "EN2fe1274add61492a983ad7322d1b3010",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/library"
        },
        "data": {
          "id": "LBd8eaef8283fe40738348db65a8984475",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467/property"
        },
        "data": {
          "id": "PRb75b4216130e469abf1eb1795da8048b",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN2fe1274add61492a983ad7322d1b3010",
      "library": "https://reactor.adobe.io/libraries/LBd8eaef8283fe40738348db65a8984475",
      "self": "https://reactor.adobe.io/builds/BL8238895201d548718bda2d0bf2b83467"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/5fc05b7c8e8f/launch-32129df48f5b-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/5fc05b7c8e8f/ae8c9574e8d4/launch-32129df48f5b-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## Création d’une version {#create}

Vous pouvez créer une version pour une bibliothèque en incluant l’identifiant de la bibliothèque, dans le chemin d’accès d’une requête POST.

**Format d’API**

```http
POST /libraries/{LIBRARY_ID}/builds
```

| Paramètre | Description |
| --- | --- |
| `LIBRARY_ID` | `id` de la bibliothèque sous laquelle vous définissez la version. |

{style="table-layout:auto"}

**Requête**

La requête suivante crée une version pour la bibliothèque spécifiée dans le chemin d’accès de la requête. Aucun payload de requête n’est requis.

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBd8eaef8283fe40738348db65a8984475/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle version.

```json
{
  "data": {
    "id": "BL5b3fbb0dfd66480abb55a376005ec3f7",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:32:00.021Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:32:00.021Z",
      "token": "65bbda194025"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/environment"
        },
        "data": {
          "id": "EN867c480dc5ea4158be3ea68e5543bd85",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/library"
        },
        "data": {
          "id": "LBdd2f55e9c3bb4ce0a582a0b0c586a6f5",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7/property"
        },
        "data": {
          "id": "PRa41874e4d1604efd9c3c67d7a123f4c6",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85",
      "library": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5",
      "self": "https://reactor.adobe.io/builds/BL5b3fbb0dfd66480abb55a376005ec3f7"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/bd007122e3e3/65bbda194025/launch-4d5a31f6ca53-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## Republication d’une version {#republish}

Vous pouvez republier une version à partir d’une [bibliothèque publiée](./libraries.md#publish) en incluant son identifiant dans le chemin d’accès d’une requête PATCH.

**Format d’API**

```http
PATCH /builds/{BUILD_ID}
```

| Paramètre | Description |
| --- | --- |
| `BUILD_ID` | `id` de la version que vous souhaitez republier. |

{style="table-layout:auto"}

**Requête**

La requête suivante met à jour le `app_id` pour une configuration d’application existante.

```shell
curl -X PATCH \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "BLb408c04c20ba4a82b6df496969a99781",
          "type": "builds",
          "meta": {
            "action": "republish"
          }
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `id` | `id` de la version à mettre à jour. Cela doit correspondre à la valeur `{BUILD_ID}` fournie dans le chemin d’accès de la requête. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `builds`. |
| `meta.action` | Type d’action PATCH à exécuter. Doit être défini sur `republish`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la version republiée.

```json
{
  "data": {
    "id": "BLb408c04c20ba4a82b6df496969a99781",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:34:08.558Z",
      "status": "succeeded",
      "updated_at": "2020-12-14T17:34:16.190Z",
      "token": "951e1b7911e8"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/environment"
        },
        "data": {
          "id": "EN51a1b47d737341b1b742cbd62504bb5a",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/library"
        },
        "data": {
          "id": "LBa503843ac6e64df0ad18604adad78600",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/property"
        },
        "data": {
          "id": "PR00abebfe39f84dc2a0ca13410e0a1751",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN51a1b47d737341b1b742cbd62504bb5a",
      "library": "https://reactor.adobe.io/libraries/LBa503843ac6e64df0ad18604adad78600",
      "self": "https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/f812fa6d64df/launch-9b1b8e461782.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/f812fa6d64df/951e1b7911e8/launch-9b1b8e461782.min.js",
      "archive": false,
      "republish_status": "pending",
      "host_type_of": "akamai"
    }
  }
}
```

## Récupération des ressources associées à une version {#related}

Les appels suivants montrent comment récupérer les ressources associées à une version. Lors de la [recherche d’une version](#lookup), ces relations sont répertoriées sous la propriété `relationships`.

Pour plus d’informations sur les relations dans l’API Reactor, consultez le [guide des relations](../guides/relationships.md).

### Liste des éléments de données associés à une version {#data-elements}

Vous pouvez répertorier les éléments de données associés à une version en ajoutant `/data_elements` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /builds/{BUILD_ID}/data_elements
```

| Paramètre | Description |
| --- | --- |
| `{BUILD_ID}` | `id` de la version dont vous souhaitez répertorier les éléments de données. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste des éléments de données associés à la version.

```json
{
  "data": [
    {
      "id": "DE4139bfd5c2194254b5c1af254d421262",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:33:22.668Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:33:21 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:33:22.668Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/property"
          },
          "data": {
            "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/origin"
          },
          "data": {
            "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/extension"
          },
          "data": {
            "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262/updated_with_extension"
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
        "self": "https://reactor.adobe.io/data_elements/DE4139bfd5c2194254b5c1af254d421262",
        "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
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
      "total_count": 1
    }
  }
}
```

### Liste des extensions associées à une version {#extensions}

Vous pouvez répertorier les extensions associées à une version en ajoutant `/extensions` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /builds/{BUILD_ID}/extensions
```

| Paramètre | Description |
| --- | --- |
| `{BUILD_ID}` | `id` de la version dont vous souhaitez répertorier les extensions. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste d’extensions associées à la version.

```json
{
  "data": [
    {
      "id": "EXf6242ef93c1c47e6971ed6ea85912b11",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:32:56.163Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:32:56.163Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/property"
          },
          "data": {
            "id": "PRcf1f3e4c218b4caab8191fab003a8355",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/origin"
          },
          "data": {
            "id": "EX8ce7ced633f34bd48d33089ff8fad082",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRcf1f3e4c218b4caab8191fab003a8355",
        "origin": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
        "self": "https://reactor.adobe.io/extensions/EXf6242ef93c1c47e6971ed6ea85912b11",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
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
      "total_count": 1
    }
  }
}
```

### Liste des règles associées à une version {#rules}

Vous pouvez répertorier les règles associées à une version en ajoutant `/rules` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /builds/{BUILD_ID}/rules
```

| Paramètre | Description |
| --- | --- |
| `{BUILD_ID}` | `id` de la version dont vous souhaitez répertorier les règles. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de règles associées à la version.

```json
{
  "data": [
    {
      "id": "RL8429f3fee98b44c68f7a538e68e21747",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:56:44.109Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:56:44.109Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/property"
          },
          "data": {
            "id": "PR41f64d2a9d9b4862b0582c5ff6a07504",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/origin"
          },
          "data": {
            "id": "RL8429f3fee98b44c68f7a538e68e21747",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504",
        "origin": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "self": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "rule_components": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
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

### Recherche de la bibliothèque associée à une version {#library}

Vous pouvez récupérer la bibliothèque associée à une version en ajoutant `/library` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /builds/{BUILD_ID}/library
```

| Paramètre | Description |
| --- | --- |
| `{BUILD_ID}` | `id` de la version dont vous souhaitez rechercher la bibliothèque. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

```json
{
  "data": {
    "id": "LB6ce27064ebe04ceab3d6942e9de563db",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:50:06.695Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:50:06.695Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/builds"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/environment",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/environment"
        },
        "data": {
          "id": "EN3287da6fafa143c289afd2f578b4d33d",
          "type": "environments"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/extensions",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/rules",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/property"
        },
        "data": {
          "id": "PR95eaa16990c745a78f5bee8439fe4c34",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR95eaa16990c745a78f5bee8439fe4c34",
      "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

### Recherche de l’environnement associé à une version {#environment}

Vous pouvez récupérer l’environnement associé à une version en ajoutant `/environment` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /builds/{BUILD_ID}/environment
```

| Paramètre | Description |
| --- | --- |
| `{BUILD_ID}` | `id` de la version dont vous souhaitez rechercher l’environnement. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/builds/BLb408c04c20ba4a82b6df496969a99781/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

```json
{
  "data": {
    "id": "EN11e6b85c0af14f0fb99f0c192a22e5e2",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:39:25.179Z",
      "library_path": "f9fd106ab399/5a1ebaf3db58",
      "library_name": "launch-f0e3e49544fe-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-f0e3e49544fe-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/5a1ebaf3db58/launch-f0e3e49544fe-development.min.js"
          ],
          "license_path": "f9fd106ab399/5a1ebaf3db58/launch-f0e3e49544fe-development.js"
        },
        {
          "library_name": "launch-f0e3e49544fe-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/5a1ebaf3db58/launch-f0e3e49544fe-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:39:26.221Z",
      "status": "succeeded",
      "token": "f0e3e49544fe"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/library"
        },
        "data": {
          "id": "LB6e0f7904575f489497b959fd6b81dce8",
          "type": "libraries"
        }
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/host",
          "self": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/relationships/host"
        },
        "data": {
          "id": "HT33afd835e6da4533a4b07d39e916d3be",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2/property"
        },
        "data": {
          "id": "PRe686c8ac90b343f98bbd14e990952605",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRe686c8ac90b343f98bbd14e990952605",
      "self": "https://reactor.adobe.io/environments/EN11e6b85c0af14f0fb99f0c192a22e5e2"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```
