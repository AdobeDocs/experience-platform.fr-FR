---
title: Point de terminaison des secrets
description: Découvrez comment effectuer des appels au point de terminaison /secrets dans l’API Reactor.
source-git-commit: 103ba74646a42fd62007f47df4d1a46caf25e3e6
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 16%

---

# Point de terminaison des secrets

Un secret est une ressource qui n&#39;existe que dans les propriétés de transfert d&#39;événements (propriétés avec un `platform` attribut défini sur `edge`). Ils permettent au transfert d&#39;événements de s&#39;authentifier sur un autre système pour un échange sécurisé de données.

Ce guide vous explique comment appeler le `/secrets` point de terminaison dans l’API Reactor. Pour une explication détaillée des différents types de secrets et comment les utiliser, veuillez vous référer à la présentation de haut niveau sur [secrets](../guides/secrets.md) avant de revenir à ce guide.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la procédure à suivre pour s’authentifier auprès de l’API.

## Récupérer une liste de secrets pour une propriété {#list-property}

Vous pouvez lister les secrets qui appartiennent à une propriété en faisant une demande de GET.

**Format d’API**

```http
GET /properties/{PROPERTY_ID}/secrets
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | ID de la propriété dont vous souhaitez répertorier les secrets. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRe005d921bb724bc88c3ff28e3e916f04/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Réponse**

Une réponse réussie renvoie une liste de secrets appartenant à la propriété.

```json
{
  "data": [
    {
      "id": "SE8bd20bd5d16b49ee9d925929e292526c",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:29.777Z",
        "updated_at": "2021-07-16T22:29:29.777Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
          },
          "data": {
            "id": "PRe005d921bb724bc88c3ff28e3e916f04",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/environment"
          },
          "data": {
            "id": "EN80ad9efbf4ff4f15bebd770613378a75",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c",
        "property": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
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

## Récupérer une liste de secrets pour un environnement {#list-environment}

Vous pouvez répertorier les secrets qui appartiennent à un environnement en effectuant une demande de GET.

**Format d’API**

```http
GET /environments/{ENVIRONMENT_ID}/secrets
```

| Paramètre | Description |
| --- | --- |
| `{ENVIRONMENT_ID}` | ID de l&#39;environnement dont vous souhaitez répertorier les secrets. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/EN0a1b00749daf4ff48a34d2ec37286aa7/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Réponse**

Une réponse réussie renvoie une liste de secrets appartenant à l&#39;environnement.

```json
{
  "data": [
    {
      "id": "SE57b5ea69acde4595825b85befd1675b3",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:35.447Z",
        "updated_at": "2021-07-16T22:29:35.447Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
          },
          "data": {
            "id": "PRb302ca3557334c13b130da719222ec97",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/environment"
          },
          "data": {
            "id": "EN0a1b00749daf4ff48a34d2ec37286aa7",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3",
        "property": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
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

## Rechercher un secret {#lookup}

Vous pouvez rechercher un secret en incluant son ID dans le chemin d’une demande de GET.

**Format d’API**

```http
GET /secrets/{SECRET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SECRET_ID}` | L&#39;ID du secret que vous voulez rechercher. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Réponse**

Une réponse réussie renvoie les détails du secret.

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## Création d’un secret {#create}

Vous pouvez créer un secret en effectuant une demande de POST.

>[!NOTE]
>
>Lorsque vous créez un nouveau secret, l’API renvoie une réponse immédiate contenant des informations pour cette ressource. Dans le même temps, une tâche d&#39;échange secret est déclenchée pour vérifier que l&#39;échange d&#39;informations d&#39;identification est fonctionnel. Cette tâche est traitée de manière asynchrone et met à jour l’attribut d’état du secret vers `succeeded` ou `failed` selon le résultat.

**Format d’API**

```http
POST /properties/{PROPERTY_ID}/secrets
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | ID de la propriété sous laquelle vous souhaitez définir le secret. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR9eff664dc6014217b76939bb78b83976/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Secret",
            "type_of": "simple-http",
            "credentials": {
              "username": "example_username",
              "password": "pass12345"
            }
          },
          "relationships": {
            "environment": {
              "data": {
                "id": "EN04cdddbdb6574170bcac9f470f3b8087",
                "type": "environments"
              }
            }
          },
          "type": "secrets"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom descriptif unique du secret. |
| `type_of` | Type d&#39;informations d&#39;identification d&#39;authentification que représente le secret. Contient trois valeurs acceptées :<ul><li>`token`: Chaîne de jeton.</li><li>`simple-http`: Nom d’utilisateur et mot de passe.</li><li>`oauth2`: Informations d’identification conformes à la norme OAuth.</li></ul> |
| `credentials` | Objet contenant les valeurs d&#39;identification du secret. Selon le paramètre `type_of` , différentes propriétés doivent être fournies. Consultez la section sur [informations](../guides/secrets.md#credentials) dans le guide des secrets pour plus de détails sur les exigences de chaque type. |
| `relationships.environment` | Chaque secret doit être associé à un environnement lors de sa création. Le `data` l&#39;objet dans cette propriété doit contenir `id` de l&#39;environnement, le secret qui lui est assigné, ainsi qu&#39;un `type` valeur de `environments`. |
| `type` | Le type de ressource en cours de création. Pour cet appel, la valeur doit être `secrets`. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails du secret. Notez que, selon le type de secret, certaines propriétés sous `credentials` peut être masqué.

```json
{
  "data": { 
    "id": "SE39fdf431f8ad4600bbc24ea73fcb1154", 
    "type": "secrets", 
    "attributes": { 
    "created_at": "2021-07-14T19:33:25.628Z", 
    "updated_at": "2021-07-14T19:33:25.628Z", 
    "name": "Example Secret", 
    "type_of": "simple-http", 
    "activated_at": null, 
    "expires_at": null, 
    "refresh_at": null, 
    "status": "pending", 
    "credentials": { 
      "username": "example_username" 
      } 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    } 
  } 
}
```

## Tester `oauth2` secret {#test}

>[!NOTE]
>
>Cette opération ne peut être effectuée que sur des secrets avec un `type_of` valeur de `oauth2`.

Vous pouvez tester `oauth2` en incluant son ID dans le chemin d’une demande de PATCH. L&#39;opération de test effectue un échange et inclut la réponse du service d&#39;autorisation dans la `test_exchange` dans le `meta` objet. Cette opération ne met pas à jour le secret lui-même.

**Format d’API**

```http
PATCH /secrets/{SECRET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SECRET_ID}` | L’ID du fichier `oauth2` secret que vous voulez tester. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SE6c15a7a64f9041b5985558ed3e19a449 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "oauth2"
          },
          "meta": {
            "action": "test"
          },
          "id": "SE6c15a7a64f9041b5985558ed3e19a449",
          "type": "secrets"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes` | Doit contenir un `type_of` avec une valeur de `oauth2`. |
| `meta` | Doit contenir un `action` avec une valeur de `test`. |
| `id` | L&#39;ID du secret que vous testez. Cette valeur doit correspondre à l’ID fourni dans le chemin d’accès de la demande. |
| `type` | Type de ressource utilisée. Cette propriété doit être définie sur `secrets`. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails du secret, avec la réponse du service d&#39;autorisation contenue dans la `meta.test_exchange`.

```json
{ 
  "data": { 
    "id": "SE6c15a7a64f9041b5985558ed3e19a449", 
    "type": "secrets", 
    "attributes": { 
      "activated_at": null, 
      "created_at": "2021-07-14T19:33:25.628Z", 
      "credentials": { 
        "authorization_url": "https://athorization_url.test/token/authorize?required_param=value",
        "client_id": "test_client_id", 
        "client_secret": "test_client_secret", 
        "refresh_offset": 14400, 
      },
      "expires_at": null, 
      "name": "Example Secret", 
      "refresh_at": null, 
      "status": "pending", 
      "type_of": "oauth2", 
      "updated_at": "2021-07-14T19:33:25.628Z", 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    }, 
    "meta": { 
      "test_exchange": { 
        "access_token": "FpIkBn3zxW0fH6EBC4MB", 
        "expires_in": 36000, 
        "token_type": "Bearer", 
      } 
    } 
  } 
}
```

## Réessayer un secret {#retry}

Une nouvelle tentative de secret consiste à déclencher manuellement l&#39;échange secret. Vous pouvez réessayer un secret en incluant son ID dans le chemin d’une demande de PATCH.

**Format d’API**

```http
PATCH /secrets/{SECRET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SECRET_ID}` | ID du secret que vous souhaitez réessayer. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "token"
          },
          "meta": {
            "action": "retry"
          },
          "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
          "type": "secrets"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes` | Doit contenir un `type_of` propriété correspondant à celle du secret en cours de mise à jour (`token`, `simple-http`, ou `oauth2`). |
| `meta` | Doit contenir un `action` avec une valeur de `retry`. |
| `id` | L&#39;ID du secret que vous tentez de nouveau. Cette valeur doit correspondre à l’ID fourni dans le chemin d’accès de la demande. |
| `type` | Type de ressource utilisée. Cette propriété doit être définie sur `secrets`. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails du secret, avec son état réinitialisé sur `pending`. Une fois l&#39;échange terminé, le statut du secret sera mis à jour en `succeeded` ou `failed` selon le résultat.

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## Suppression d’un secret {#delete}

Vous pouvez supprimer un secret en incluant son ID dans le chemin d’une demande de DELETE. Il s’agit d’une suppression définitive avec effet immédiat et ne nécessite pas de republication de bibliothèque.

Cette opération supprime le secret de l&#39;environnement auquel il est associé et la ressource sous-jacente est supprimée.

>[!WARNING]
>
>Si vous avez des règles déployées qui font référence à un secret supprimé, ces règles cesseront immédiatement de fonctionner. Tout élément de données faisant référence à ce secret doit être mis à jour ou supprimé par la suite.

**Format d’API**

```http
DELETE /secrets/{SECRET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SECRET_ID}` | ID du secret que vous souhaitez supprimer. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X DELETE \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 204 (Aucun contenu) et un corps de réponse vide, indiquant que le secret a été supprimé du système.

## Liste des notes pour un secret {#notes}

L’API Reactor vous permet d’ajouter des notes à certaines ressources, y compris des secrets. Les notes sont des annotations textuelles qui n’ont aucune incidence sur le comportement des ressources et peuvent être utilisées pour divers cas d’utilisation.

>[!NOTE]
>
>Voir la section [guide de point de terminaison notes](./notes.md) pour plus d’informations sur la création et la modification de notes pour les ressources d’API de réacteur.

Vous pouvez récupérer toutes les notes associées à un secret en effectuant une demande de GET.

**Format d’API**

```http
GET /secrets/{SECRET_ID}/notes
```

| Paramètre | Description |
| --- | --- |
| `{SECRET_ID}` | L&#39;ID du secret dont vous souhaitez répertorier les notes. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Réponse**

Une réponse réussie renvoie une liste de notes appartenant au secret.

```json
{
  "data": [
    {
      "id": "NTe666dbcc2f204218b6fde2fe60ab7043",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Doe",
        "author_email": "jdoe@example.com",
        "created_at": "2021-07-16T22:29:58.259Z",
        "text": "This is a secret note."
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1"
          },
          "data": {
            "id": "SE591d3b86910f4e6883f0e1c36e54bff1",
            "type": "secrets"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1",
        "self": "https://reactor.adobe.io/notes/NTe666dbcc2f204218b6fde2fe60ab7043"
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

## Récupérer les ressources associées pour un secret {#related}

Les appels suivants montrent comment récupérer les ressources associées pour un secret. Lorsque [rechercher un secret](#lookup), ces relations sont répertoriées sous le noeud `relationships` propriété.

Pour plus d’informations sur les relations dans l’API Reactor, consultez le [guide des relations](../guides/relationships.md).

### Rechercher un secret dans l&#39;environnement associé {#environment}

Vous pouvez rechercher l&#39;environnement qui utilise un secret en ajoutant `/environment` vers le chemin d’une demande de GET.

**Format d’API**

```http
GET /secrets/{SECRET_ID}/environment
```

| Paramètre | Description |
| --- | --- |
| `{SECRET_ID}` | L&#39;ID du secret dont vous souhaitez rechercher l&#39;environnement. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Réponse**

Une réponse réussie renvoie les détails de l’environnement.

```json
{
  "data": {
    "id": "EN33e8d63ac647448da1f77ced5c3c8580",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2021-07-16T22:19:13.438Z",
      "library_path": "bc12f2b85d11/b9a3067414ff",
      "library_name": "launch-3b6c4eea15ae-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-3b6c4eea15ae-development.min.js",
          "minified": true,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.min.js"
          ],
          "license_path": "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
        },
        {
          "library_name": "launch-3b6c4eea15ae-development.js",
          "minified": false,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": null,
      "stage": "development",
      "updated_at": "2021-07-16T22:19:13.438Z",
      "status": "succeeded",
      "token": "3b6c4eea15ae"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/host",
          "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/relationships/host"
        },
        "data": {
          "id": "HT7d5cf665463e46a1968ada1ceb1b5ca7",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/property"
        },
        "data": {
          "id": "PRba81d3027db846b084212391aa5d2f1f",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRba81d3027db846b084212391aa5d2f1f",
      "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### Rechercher un secret dans la propriété associée {#property}

Vous pouvez rechercher la propriété qui possède un secret en ajoutant `/property` vers le chemin d’une demande de GET.

**Format d’API**

```http
GET /secrets/{SECRET_ID}/property
```

| Paramètre | Description |
| --- | --- |
| `{SECRET_ID}` | L&#39;ID du secret dont vous souhaitez rechercher la propriété. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Réponse**

Une réponse réussie renvoie les détails au sujet de la propriété.

```json
{
  "data": {
    "id": "PR2d191feafef54c5da4ddb5ef647d4867",
    "type": "properties",
    "attributes": {
      "created_at": "2021-07-16T22:26:25.320Z",
      "enabled": true,
      "name": "Kessel Edge Example Property",
      "updated_at": "2021-07-16T22:26:25.320Z",
      "platform": "edge",
      "development": false,
      "token": "8efbe7023155"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/company"
        },
        "data": {
          "id": "COc26fb19f87d24cbe827a70ad2a672093",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/COc26fb19f87d24cbe827a70ad2a672093",
      "data_elements": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments",
      "extensions": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions",
      "rules": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules",
      "self": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "edit_property",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
