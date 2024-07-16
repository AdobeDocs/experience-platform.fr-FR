---
title: Point d’entrée des packages d’extension
description: Découvrez comment effectuer des appels au point d’entrée /extension_packages dans l’API Reactor.
exl-id: a91c6f32-6c72-4118-a43f-2bd8ef50709f
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 97%

---

# Point d’entrée des packages d’extension

>[!WARNING]
>
>L’implémentation du point d’entrée `/extension_packages` se fait en flux continu à mesure que des fonctionnalités sont ajoutées, supprimées et retravaillées.

Un package d’extension représente une [extension](./extensions.md) telle qu’elle a été créée par un développeur d’extension. Un package d’extension définit des fonctionnalités supplémentaires qui peuvent être mises à la disposition des utilisateurs de balises. La plupart du temps, ces fonctionnalités se présentent sous la forme de [composants de règle](./rule-components.md) (événements, conditions et actions) et [d&#39;éléments de données](./data-elements.md), mais peuvent également inclure des modules principaux et des modules partagés.

Les modules d’extension s’affichent dans le catalogue d’extensions dans l’interface utilisateur de la collecte de données et l’interface utilisateur de Adobe Experience Platform pour que les utilisateurs puissent les installer. L’ajout d’un package d’extension à une propriété s&#39;effectue en créant une extension comportant un lien vers le package d’extension.

Un package d’extension appartient à la [société](./companies.md) du développeur qui l’a créé.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la procédure à suivre pour s’authentifier auprès de l’API.

Il est important de comprendre non seulement comment passer des appels à lʼAPI Reactor, mais également comment les attributs `status` et `availability` dʼun package dʼextension déterminent les actions que vous pouvez effectuer sur celui-ci. Ces actions sont abordées dans les sections ci-dessous.

### État

Les packages dʼextension ont trois états possibles : `pending`, `succeeded` et `failed`.

| État | Description |
| --- | --- |
| `pending` | Lorsquʼun package dʼextension est créé, sa valeur `status` est définie sur `pending`. Cela indique que le système a reçu les informations concernant le package dʼextension et que le traitement va commencer. Les packages dʼextension dont lʼétat est `pending` ne sont pas disponibles. |
| `succeeded` | Lʼétat dʼun package dʼextension est mis à jour vers `succeeded` sʼil a réussi le traitement. |
| `failed` | Lʼétat dʼun package dʼextension est mis à jour vers `failed` sʼil nʼa pas réussi le traitement. Un package dʼextension dont lʼétat est `failed` peut être mis à jour jusquʼà ce que le traitement réussisse. Les packages dʼextension dont lʼétat est `failed` ne sont pas disponibles. |

### Disponibilité

Il existe plusieurs niveaux de disponibilité pour un package dʼextension : `development`, `private` et `public`.

| Disponibilité | Description |
| --- | --- |
| `development` | Un package dʼextension dont le niveau est `development` nʼest visible et disponible quʼau sein de la société qui le possède. En outre, il ne peut être utilisé que sur les propriétés configurées pour le développement dʼextensions. |
| `private` | Un package dʼextension dont le niveau est `private` nʼest visible que par la société qui le possède et ne peut être installé que sur les propriétés détenues par la société. |
| `public` | Un package dʼextension dont le niveau est `public` est visible et disponible pour toutes les sociétés et propriétés. |

>[!NOTE]
>
>Lorsquʼun package dʼextension est créé, la valeur `availability` change en `development`. Une fois les tests terminés, vous pouvez définir le package dʼextension sur `private` ou `public`.

## Récupération d’une liste des packages d’extension {#list}

Vous pouvez récupérer une liste des packages d’extension en effectuant une requête GET sur `/extension_packages`.

**Format d&#39;API**

```http
GET /extension_packages
```

>[!NOTE]
>
>À l’aide des paramètres de requête, les packages d’extension répertoriés peuvent être filtrés en fonction des attributs suivants :<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>Consultez le guide sur le [filtrage des réponses](../guides/filtering.md) pour plus d&#39;informations.

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste des packages d’extension.

```json
{
  "data": [
    {
      "id": "EP6860e2485de2413ea9b295d6f5321ad3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP6860e2485de2413ea9b295d6f5321ad3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:32.694Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944710",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:35.754Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP6860e2485de2413ea9b295d6f5321ad3"
      }
    },
    {
      "id": "EP1b173c8316954e0986e5a405b4e715e3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP1b173c8316954e0986e5a405b4e715e3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:34.632Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944712",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:36.655Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP1b173c8316954e0986e5a405b4e715e3"
      }
    },
    {
      "id": "EPb8eca81769a64af3892af5202a57ce15",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EPb8eca81769a64af3892af5202a57ce15",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T18:32:29.271Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604946740",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T18:32:43.710Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EPb8eca81769a64af3892af5202a57ce15"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 3
    }
  }
}
```

## Recherche d’un package d’extension {#lookup}

Vous pouvez rechercher un package d’extension en fournissant son identifiant dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Le `id` du package d’extension que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les informations relatives au package d’extension, y compris ses ressources déléguées telles que `actions`, `conditions`, `data_elements`, etc. La réponse ci-dessous a été réduite pour gagner de l’espace.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Création dʼun package dʼextension {#create}

Les packages d’extension sont créés à l’aide d’un outil de génération de modèles automatique Node.js et enregistrés sur votre ordinateur local avant d’être soumis à l’API Reactor. Pour plus d’informations sur la configuration d’un package d’extension, consultez le guide de [prise en main du développement d’extension](../../extension-dev/getting-started.md).

Une fois le fichier du package d’extension créé, vous pouvez l’envoyer à l’API Reactor par le biais d’une demande POST.

**Format d’API**

```http
POST /extension_packages
```

**Requête**

La requête suivante crée un package d’extension. Le chemin d’accès local au fichier de package en cours de chargement est référencé en tant que données de formulaire (`package`). Par conséquent, ce point d’entrée nécessite un en-tête `Content-Type` de `multipart/form-data`.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Réponse**

Une réponse réussie renvoie les détails du package d’extension qui vient d’être créé.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Mettre à jour un package d’extension {#update}

Vous pouvez mettre à jour un package dʼextension en incluant son identifiant dans le chemin dʼaccès dʼune requête PATCH.

**Format d’API**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Le `id` du package d’extension que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

Comme pour [la création d’un package d’extension](#create), une version locale du package mis à jour doit être téléchargée via les données de formulaire.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Réponse**

Une réponse réussie renvoie les détails du package d’extension mis à jour.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Publication privée d’un package d’extension {#private-release}

Une fois que vous avez terminé le test de votre package d’extension, vous pouvez le publier de manière privée. Cela permet de la rendre disponible pour n’importe quelle propriété de votre société.

Une fois que vous avez publié votre version privée, vous pouvez lancer le processus de publication publique en remplissant le [formulaire de demande de publication publique](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest).

**Format d’API**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Le `id` du package d’extension que vous souhaitez publier en privé. |

{style="table-layout:auto"}

**Requête**

Une version privée est obtenue en fournissant une `action` avec une valeur de `release_private` dans la balise `meta` des données de la requête.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "meta": {
            "action": "release_private"
          },
          "id": "EP27e9323eb585411fae6086fc78a3b70b",
          "type": "extension_packages"
        }
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du package d’extension.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Arrêt d’un package d’extension {#discontinue}

Vous pouvez arrêter un package d’extension en définissant son attribut `discontinued` sur `true` via une requête PATCH.

**Format d’API**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Le `id` du package d’extension que vous souhaitez arrêter. |

{style="table-layout:auto"}

**Requête**

Une version privée est obtenue en fournissant une `action` avec une valeur de `release_private` dans la balise `meta` des données de la requête.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "discontinued": true
          },
          "id": "EP5705a5d99aba406692e0ac666fcab160",
          "type": "extension_packages"
        }
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du package d’extension.

```json
{
  "data": {
    "id": "EP5705a5d99aba406692e0ac666fcab160",
    "type": "extension_packages",
    "attributes": {
      "actions": [

      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP5705a5d99aba406692e0ac666fcab160",
      "conditions": [

      ],
      "configuration": null,
      "created_at": "2020-12-14T17:39:36.932Z",
      "data_elements": [

      ],
      "description": "Provides nothing.",
      "discontinued": true,
      "display_name": "Kessel Template Test",
      "events": [

      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "test-1607967575",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-12-14T17:39:43.883Z",
      "version": "1.0.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP5705a5d99aba406692e0ac666fcab160"
    }
  }
}
```

## Liste des versions d’un package d’extension

Vous pouvez répertorier les versions d’un package d’extension en ajoutant `/versions` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/versions
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Le `id` du package d’extension dont vous souhaitez répertorier les versions. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172/versions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie un tableau des versions précédentes du package d’extension. Un exemple de réponse a été omis pour l’espace.
