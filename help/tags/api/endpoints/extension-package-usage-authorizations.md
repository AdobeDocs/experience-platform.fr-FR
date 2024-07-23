---
title: Point de terminaison des autorisations d’utilisation du package d’extension
description: Découvrez comment effectuer des appels au point de terminaison /extension_package_usage des autorisations dans l’API Reactor.
exl-id: ad3fb704-7d2f-45ec-b80b-ea4d327f2205
source-git-commit: 9cdd349e0eccb4498d88f24a84b0f1c116b0adfe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 16%

---

# Point d’entrée des autorisations d’utilisation des modules d’extension

Un package d’extension représente une [extension](./extensions.md) telle qu’elle a été créée par un développeur d’extension. Les fonctionnalités supplémentaires qui peuvent être mises à la disposition des utilisateurs de balises sont définies par un package d’extension. Ces fonctionnalités peuvent inclure des modules principaux et des modules partagés, bien qu’ils soient le plus souvent fournis en tant que [composants de règle](./rule-components.md) (événements, conditions et actions) et [éléments de données](./data-elements.md).

Un package d’extension est détenu par la [société](./companies.md) du développeur. Les propriétaires des packages d’extension peuvent autoriser d’autres entreprises à utiliser leurs versions privées des packages. Chaque entreprise autorisée dispose d’une autorisation d’utilisation pour un package d’extension unique, valide pour toutes les versions privées futures et actuelles du package.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la procédure à suivre pour s’authentifier auprès de l’API.

## Récupérer les autorisations d’utilisation des modules d’extension pour un module d’extension {#list}

Pour récupérer une liste des autorisations d’utilisation d’un package d’extension, envoyez une requête GET au point de terminaison suivant.

**Format d’API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `ID` de la propriété dont vous souhaitez répertorier l’autorisation d’utilisation du package d’extension. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
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
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
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

## Création d’une autorisation d’utilisation de package d’extension {#create}

Créez une autorisation d’utilisation de package d’extension pour chaque [package d’extension](./extension-packages.md) et `{ORG_ID}` de l’organisation que vous souhaitez autoriser. Pour créer une autorisation d’utilisation de package d’extension, envoyez une requête de POST au point de terminaison ci-dessous.

**Format d’API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` du package d’extension pour lequel vous souhaitez créer une autorisation.&quot; |

{style="table-layout:auto"}

**Requête**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Propriété | Description |
| --- | --- |
| `attributes.authorized_org_id` | `ID` de l’organisation à autoriser. |

**Réponse**

Une réponse réussie renvoie les détails de l’autorisation d’utilisation du package d’extension nouvellement créée.

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>Dans l’exemple de réponse ci-dessus, l’autorisation se trouve actuellement à l’étape `pending_approval` . Avant d’utiliser le package d’extension, l’organisation doit approuver l’autorisation. Les utilisateurs de l’organisation peuvent parcourir le package d’extension privé pendant que l’autorisation est en attente d’approbation, mais ils ne peuvent pas l’installer et ne peuvent pas le trouver dans leur catalogue d’extensions.

## Récupérer une liste des autorisations d’utilisation des packages d’extension {#list-authorizations}

Vous pouvez récupérer une liste des autorisations d’utilisation de package d’extension en effectuant une requête de GET.

**Format d’API**

```http
GET /extension_package_usage_authorizations
```

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
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
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## Suppression d’une autorisation d’utilisation de package d’extension {#delete}

Pour supprimer une autorisation d’utilisation de package d’extension, incluez son `ID` dans le chemin d’accès d’une requête de DELETE. Cela empêche l’organisation autorisée d’afficher les versions privées du package d’extension dans le catalogue et de l’installer sur leurs propriétés.

>[!NOTE]
>
>Toutes les versions privées précédemment installées continueront à fonctionner comme prévu.

**Format d’API**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| Paramètre | Description |
| --- | --- |
| `ID` | `ID` de l’autorisation d’utilisation du package d’extension que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content) sans corps de réponse. Cela indique que l’extension a été supprimée.

## Mettre à jour une autorisation d’utilisation de package d’extension {#update}

Pour approuver ou rejeter une autorisation d’utilisation de package d’extension, incluez son `ID` dans le chemin d’une demande de PATCH.

>[!NOTE]
>
>Pour approuver ou rejeter une autorisation d’utilisation de package d’extension pour votre entreprise, vous devez disposer des droits `manage_properties`.

**Format d’API**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| Paramètre | Description |
| --- | --- |
| `ID` | `ID` de l’autorisation d’utilisation du package d’extension que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| Propriété | Description |
| --- | --- |
| `attributes` | Attributs que vous souhaitez réviser. Pour les autorisations d’utilisation de package d’extension, vous pouvez réviser leur `state`. |

**Réponse**

Une réponse réussie renvoie les détails de l’autorisation d’utilisation du package d’extension révisée.

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>Une fois l’autorisation approuvée, votre entreprise peut installer le package d’extension sur vos propriétés.

## Récupérer les données du package d’extension pour une autorisation d’utilisation de package d’extension {#retrieve-data}

Vous pouvez récupérer les données du package d’extension pour une autorisation d’utilisation de package d’extension en effectuant une demande de GET.

**Format d’API**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| Paramètre | Description |
| --- | --- |
| `ID` | `ID` de l’autorisation d’utilisation du package d’extension que vous souhaitez récupérer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie des données pour le package d’extension pour une autorisation de package d’extension.

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
