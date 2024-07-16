---
title: Point d’entrée des configurations d’application
description: Découvrez comment effectuer des appels vers le point d’entrée /app_configurations dans l’API Reactor.
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 36320addc790e844a1102314890e8692841dc5d0
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 96%

---

# Point d’entrée des configurations d’application

>[!WARNING]
>
>L’implémentation du point d’entrée `/app_configurations` se fait en flux continu à mesure que des fonctionnalités sont ajoutées, supprimées et retravaillées.

Les configurations dʼapplication permettent de stocker et de récupérer les informations dʼidentification en vue dʼune utilisation ultérieure. Le point d’entrée `/app_configurations` de l’API Reactor vous permet de gérer par programmation les configurations d’application au sein de votre application d’expérience.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, veuillez consulter le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

## Récupération d’une liste de configurations d’application {#list}

**Format d’API**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Paramètre | Description |
| --- | --- |
| `COMPANY_ID` | `id` de la [société](./companies.md) propriétaire des configurations de l’application. |

{style="table-layout:auto"}

>[!NOTE]
>
>À l’aide des paramètres de requête, les configurations d’application répertoriées peuvent être filtrées en fonction des attributs suivants :<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Pour plus d’informations, consultez le guide sur le [filtrage des réponses](../guides/filtering.md).

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de configurations d’application.

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
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

## Recherche d’une configuration d’application {#lookup}

Vous pouvez rechercher une configuration d’application en fournissant son identifiant dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `APP_CONFIGURATION_ID` | Le `id` de la configuration d’application que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de la configuration d’application.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Création d’une configuration d’application {#create}

Vous pouvez créer une configuration d’application en effectuant une requête POST.

**Format d’API**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Paramètre | Description |
| --- | --- |
| `COMPANY_ID` | Champ `id` de la [société](./companies.md) dans laquelle vous définissez la configuration d’application. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `platform` | Plateforme sur laquelle l’application s’exécute (web ou mobile). Cela détermine les services de messagerie disponibles. |
| `messaging_service` | Service de messagerie associé à l’application, tel que [Apple Push Notification Service (APNs)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) et [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Cela détermine les types de clés qui peuvent être utilisés. |
| `key_type` | Représente le protocole pris en charge par un fournisseur de service Push et détermine le format de l’objet `push_credential`. À mesure que les protocoles évoluent pour les services de messagerie, de nouvelles valeurs `key_type` sont créées pour prendre en charge les protocoles mis à jour. |
| `push_credential` | La valeur d’identification réelle, qui est chiffrée au repos. Ce champ n’est normalement pas déchiffré ou inclus dans les réponses de l’API. Seuls certains services Adobe peuvent obtenir une réponse contenant des informations d’identification push déchiffrées. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la configuration d’application que vous venez de créer.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Mise à jour d’une configuration d’application

Vous pouvez mettre à jour une configuration d’application en incluant son identifiant dans le chemin d’accès d’une requête de PATCH.

**Format d’API**

```http
PATCH /app_configurations/{APP_CONFIGURATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `APP_CONFIGURATION_ID` | Champ `id` de la configuration d’application que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

La requête suivante met à jour le `app_id` pour une configuration d’application existante.

```shell
curl -X PATCH \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes` | Objet dont les propriétés représentent les attributs à mettre à jour pour la configuration d’application. Chaque clé représente l’attribut de configuration d’application particulier à mettre à jour, ainsi que la valeur correspondante vers laquelle elle doit être mise à jour.<br><br>Les attributs suivants peuvent être mis à jour pour les configurations d’application :<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | Champ `id` de la configuration d’application à mettre à jour. Cela doit correspondre à la valeur `{APP_CONFIGURATION_ID}` fournie dans le chemin d’accès de la requête. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `app_configurations`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la configuration d’application mise à jour.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Suppression d’une configuration d’application

Vous pouvez supprimer une configuration d’application en incluant son identifiant dans le chemin dʼaccès dʼune requête DELETE.

**Format d’API**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `APP_CONFIGURATION_ID` | Champ `id` de la configuration d’application que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 204 (No Content) sans corps de réponse, indiquant que la configuration d’application a été supprimée.
