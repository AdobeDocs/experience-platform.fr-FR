---
title: Point d’entrée des hôtes
description: Découvrez comment effectuer des appels au point d’entrée /hôtes dans l’API Reactor.
exl-id: 9d0d2a65-49e9-429c-a665-754b59a11cf1
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 91%

---

# Point d’entrée des hôtes

>[!NOTE]
>
>Ce document explique comment gérer les hôtes dans l’API Reactor. Pour plus d’informations sur les hôtes pour les balises, consultez le guide sur la [présentation des hôtes](../../ui/publishing/hosts/hosts-overview.md) dans la documentation de publication.

Dans l’API Reactor, un hôte définit une destination où une [version](./builds.md) peut être diffusée.

Lorsquʼune version est demandée par un utilisateur de balises dans Adobe Experience Platform, le système vérifie la bibliothèque pour déterminer dans quel [environnement](./environments.md) celle-ci doit être créée. Chaque environnement entretient une relation avec un hôte, indiquant où diffuser la version.

Un hôte appartient à une seule [propriété](./properties.md), tandis qu’une propriété peut avoir de nombreux hôtes. Une propriété doit comporter au moins un hôte avant de pouvoir publier.

Un hôte peut être utilisé par plusieurs environnements au sein d’une propriété. Il est courant de disposer d’un seul hôte sur une propriété et de faire en sorte que tous les environnements de cette propriété utilisent le même hôte.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

## Récupération dʼune liste dʼhôtes {#list}

Vous pouvez récupérer une liste d’hôtes pour une propriété en incluant l’identifiant de la propriété dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | Le `id` de la propriété propriétaire des hôtes. |

{style="table-layout:auto"}

>[!NOTE]
>
>À l’aide des paramètres de requête, les hôtes répertoriés peuvent être filtrés en fonction des attributs suivants :<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>Pour plus d’informations, consultez le guide sur le [filtrage des réponses](../guides/filtering.md).

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste d’hôtes pour la propriété spécifiée.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
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

## Recherche d’un hôte {#lookup}

Vous pouvez rechercher un hôte en fournissant son identifiant dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /hosts/{HOST_ID}
```

| Paramètre | Description |
| --- | --- |
| `HOST_ID` | Le `id` de l’hôte que vous voulez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de l’hôte.

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## Création d’un hôte {#create}

Vous pouvez créer un hôte en effectuant une requête POST.

**Format d’API**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | Le `id` de la [propriété](./properties.md) sous laquelle vous définissez l’hôte. |

{style="table-layout:auto"}

**Requête**

La requête suivante crée un hôte pour la propriété spécifiée. L’appel associe également l’hôte à une extension existante par le biais de la propriété `relationships`. Pour plus d’informations, consultez le guide sur les [relations](../guides/relationships.md).

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "skip_symlinks": true,
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes.name` | **(Obligatoire)** Nom de l’hôte, lisible par l’utilisateur. |
| `attributes.type_of` | **(Obligatoire)** Type d’hôte. Il peut s’agir de l’une des deux options suivantes : <ul><li>`akamai` pour les [hôtes gérés par Adobe](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` pour les [hôtes SFTP](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | Clé privée facultative à utiliser pour l’authentification de l’hôte. |
| `attributes.path` | Chemin d’accès à ajouter à l’URL `server`. |
| `attributes.port` | Nombre entier indiquant le port de serveur spécifique à utiliser. |
| `attributes.server` | URL hôte du serveur. |
| `attributes.skip_symlinks`<br><br>(Pour les hôtes SFTP uniquement) | Par défaut, tous les hôtes SFTP utilisent des liens symboliques (symlinks) pour référencer les versions de bibliothèque enregistrées sur le serveur. Cependant, tous les serveurs ne prennent pas en charge l’utilisation de liens symboliques. Lorsque cet attribut est inclus et défini sur `true`, l’hôte utilise une opération de copie pour mettre à jour les ressources de création directement au lieu d’utiliser des liens symboliques. |
| `attributes.username` | Nom d’utilisateur facultatif pour l’authentification. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `hosts`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de l’hôte nouvellement créé.

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "skip_symlinks": true,
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## Mise à jour d’un hôte {#update}

>[!NOTE]
>
>Seuls les hôtes SFTP peuvent être mis à jour.

Vous pouvez mettre à jour un hôte en incluant son identifiant dans le chemin d’accès d’une requête PATCH.

**Format d’API**

```http
PATCH /hosts/{HOST_ID}
```

| Paramètre | Description |
| --- | --- |
| `HOST_ID` | Le `id` de l’hôte que vous voulez mettre à jour. |

{style="table-layout:auto"}

**Requête**

La requête suivante met à jour le `name` pour un hôte existant.

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes` | Objet dont les propriétés représentent les attributs à mettre à jour pour l’hôte. Les attributs suivants peuvent être mis à jour pour un hôte : <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | Le `id` de l’hôte que vous voulez mettre à jour. Il doit correspondre à la valeur `{HOST_ID}` fournie dans le chemin de requête. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `hosts`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de l&#39;hôte mis à jour.

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "skip_symlinks": true,
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## Suppression d’un hôte

Vous pouvez supprimer un hôte en incluant son identifiant dans le chemin dʼaccès dʼune requête DELETE.

**Format d’API**

```http
DELETE /hosts/{HOST_ID}
```

| Paramètre | Description |
| --- | --- |
| `HOST_ID` | Le `id` de lʼhôte que vous voulez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content) sans corps de réponse, indiquant que l’hôte a été supprimé.

## Récupération des ressources associées à un hôte {#related}

Les appels suivants montrent la marche à suivre pour récupérer les ressources associées à un hôte. Lorsque vous [recherchez un hôte](#lookup), ces relations sont répertoriées sous la propriété `relationships`.

Pour plus d’informations sur les relations dans l’API Reactor, consultez le [guide des relations](../guides/relationships.md).

### Recherche de la propriété associée pour un hôte {#property}

Vous pouvez rechercher la propriété propriétaire d’un hôte en ajoutant `/property` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET /hosts/{HOST_ID}/property
```

| Paramètre | Description |
| --- | --- |
| `{HOST_ID}` | Champ `id` de lʼhôte dont vous souhaitez rechercher la propriété. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de la propriété de l’hôte spécifié.

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
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
