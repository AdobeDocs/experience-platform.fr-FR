---
title: Point d’entrée Propriétés
description: Découvrez comment effectuer des appels vers le point d’entrée /Propriétés dans l’API Reactor.
exl-id: 7830c519-312f-4f73-b3f5-64ab0420d902
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 98%

---

# Point d’entrée Propriétés

Une propriété est un concept de conteneur qui assure le disponibilité de la plupart des autres ressources dans l’API Reactor. Vous gérez les propriétés par programmation à l’aide du point d’entrée `/properties`.

Dans la hiérarchie Ressource, une propriété est considérée propriétaire des éléments suivants :

* [Versions](./builds.md)
* [Rappels](./callbacks.md)
* [Éléments de données](./data-elements.md)
* [Environnements](./environments.md)
* [Extensions](./extensions.md)
* [Hôtes](./properties.md)
* [Bibliothèques](./libraries.md)
* [Composants de règle](./rule-components.md)
* [Règles](./rules.md)

Une propriété appartient à une seule [société](./companies.md). Une société peut contenir plusieurs propriétés.

Pour plus d’informations sur les propriétés et leur rôle dans la gestion des balises, reportez-vous à la présentation des [entreprises et propriétés](../../ui/administration/companies-and-properties.md).

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, veuillez consulter le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

## Récupération dʼune liste de propriétés {#list}

Vous pouvez récupérer une liste de propriétés appartenant à la société en incluant l’identifiant de l’entreprise dans le chemin d&#39;accès d’une requête GET.

**Format d’API**

```http
GET /companies/{COMPANY_ID}/properties
```

| Paramètre | Description |
| --- | --- |
| `COMPANY_ID` | Champ `id` de la société qui détient les propriétés que vous souhaitez répertorier. |

{style="table-layout:auto"}

>[!NOTE]
>
>À l’aide des paramètres de requête, les propriétés répertoriées peuvent être filtrées en fonction des attributs suivants :<ul><li>`copying`</li><li>`created_at`</li><li>`enabled`</li><li>`name`</li><li>`platform`</li><li>`token`</li><li>`updated_at`</li></ul>Pour plus d’informations, consultez le guide sur le [filtrage des réponses](../guides/filtering.md).

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de propriétés pour la société spécifiée.

```json
{
  "data": [
    {
      "id": "PR29e066628dcf4ba0a16780b2e339821c",
      "type": "properties",
      "attributes": {
        "created_at": "2020-12-14T17:51:28.215Z",
        "enabled": true,
        "name": "Kessel Example Property",
        "updated_at": "2020-12-14T17:51:28.215Z",
        "platform": "web",
        "development": false,
        "token": "30a138ca7f5b",
        "domains": [
          "example.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments",
        "extensions": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions",
        "rules": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules",
        "self": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c"
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
    },
    {
      "id": "PR0c559a62480142a7b9be4a118d1a0448",
      "type": "properties",
      "attributes": {
        "created_at": "2020-08-14T15:29:34.241Z",
        "enabled": true,
        "name": "new prop",
        "updated_at": "2020-08-14T15:29:34.241Z",
        "platform": "web",
        "development": true,
        "token": "b6cee01dedb7",
        "domains": [
          "google.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments",
        "extensions": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions",
        "rules": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules",
        "self": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448"
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

## Recherche d’une propriété {#lookup}

Vous pouvez rechercher une propriété en fournissant son identifiant dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /properties/{PROPERTY_ID}
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | Champ `id` de la propriété que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails au sujet de la propriété.

```json
{
  "data": {
    "id": "PR48ade10e6acf4385ba96214e9f5d31e1",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:18.725Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:18.725Z",
      "platform": "web",
      "development": false,
      "token": "c54ba5e843e6",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments",
      "extensions": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions",
      "rules": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules",
      "self": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1"
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

## Création d’une propriété {#create}

Vous pouvez créer une propriété en effectuant une requête POST.

**Format d’API**

```http
POST /company/{COMPANY_ID}/properties
```

| Paramètre | Description |
| --- | --- |
| `COMPANY_ID` | Champ `id` de la société sous laquelle vous définissez la propriété. |

{style="table-layout:auto"}

**Requête**

La requête suivante crée une propriété pour la propriété spécifiée. L’appel associe également la propriété à une extension existante par le biais de la propriété `relationships`. Pour plus d’informations, consultez le guide sur les [relations](../guides/relationships.md).

```shell
curl -X POST \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Example Property",
            "platform": "web"
            "domains": [
              "example.com"
            ],
            "privacy": "gdpr",
            "rule_component_sequencing_enabled": false,
            "ssl_enabled": false,
            "undefined_vars_return_empty": true
          },
          "type": "properties"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes.name` | **(Obligatoire)** Nom lisible par l&#39;utilisateur de la propriété. |
| `attributes.platform` | **(Obligatoire)** Plateforme de la propriété. Peut être `web` pour les propriétés web ou `mobile` ou encore `edge` pour les propriétés mobiles. |
| `attributes.domains` | **(Obligatoire pour les propriétés web)** Tableau de domaines d’URL pour la propriété. |
| `attributes.development` | Valeur booléenne qui indique s’il s’agit d’une propriété de développement. |
| `attributes.privacy` | Chaîne pouvant être utilisée pour faire référence à des considérations liées à la confidentialité pour la propriété. |
| `attributes.rule_component_sequencing_enabled` | Valeur booléenne indiquant si le séquencement des composants de règle doit être activé pour cette propriété. |
| `attributes.ssl_enabled` | Valeur booléenne indiquant si le protocole SSL (Secure Sockets Layer) doit être activé pour cette propriété. |
| `attributes.undefined_vars_return_empty` | Valeur booléenne indiquant si les variables non définies doivent être renvoyées comme étant vides pour cette propriété. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `properties`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la propriété nouvellement créée.

```json
{
  "data": {
    "id": "PR505e39de0d0042d1b22321e7767edb4d",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:31:31.579Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:31:31.579Z",
      "platform": "web",
      "development": false,
      "token": "a969ffc6f872",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments",
      "extensions": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions",
      "rules": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules",
      "self": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d"
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

## Mettre à jour une propriété {#update}

Vous pouvez mettre à jour une propriété en incluant son identifiant dans le chemin d’accès d’une requête PATCH.

**Format d’API**

```http
PATCH /properties/{PROPERTY_ID}
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | Champ `id` de la propriété que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

La requête suivante met à jour `name` et `domains` pour une propriété existante.

```shell
curl -X PATCH \
  https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Property B",
            "domains": [
              "example.com"
            ]
          },
          "id": "PR541dbb24bad54dceb04710d7a9e7a740",
          "type": "properties"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `attributes` | Objet dont les propriétés représentent les attributs à mettre à jour pour la propriété. Pour une propriété donnée, les attributs suivants peuvent être mis à jour : <ul><li>`development`</li><li>`domains`</li><li>`name`</li><li>`platform`</li><li>`privacy`</li><li>`rule_component_sequencing_enabled`</li><li>`ssl_enabled`</li><li>`undefined_vars_return_empty`</li></ul> |
| `id` | Le `id` de la propriété que vous souhaitez mettre à jour. Cela doit correspondre à la valeur `{PROPERTY_ID}` fournie dans le chemin d’accès de la requête. |
| `type` | Le type de ressource en cours de mise à jour. Pour ce point d’entrée, la valeur doit être `properties`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la propriété mise à jour.

```json
{
  "data": {
    "id": "PR541dbb24bad54dceb04710d7a9e7a740",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:37.386Z",
      "enabled": true,
      "name": "Kessel Property B",
      "updated_at": "2020-12-14T17:51:43.062Z",
      "platform": "web",
      "development": false,
      "token": "3f2d8630a8d3",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments",
      "extensions": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions",
      "rules": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules",
      "self": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740"
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

## Suppression d’une propriété

Vous pouvez supprimer une propriété en incluant son identifiant dans le chemin dʼaccès dʼune requête DELETE.

**Format d’API**

```http
DELETE /properties/{PROPERTY_ID}
```

| Paramètre | Description |
| --- | --- |
| `PROPERTY_ID` | `id` de la propriété que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X DELETE \
  https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content) sans corps de réponse, indiquant que la propriété a été supprimée.

## Gestion des notes d’une propriété {#notes}

Les propriétés sont des ressources « remarquables », ce qui signifie que vous pouvez créer et récupérer des notes textuelles sur chaque ressource. Pour plus d’informations sur la façon de gérer des notes pour les propriétés et d’autres ressources compatibles, consultez le [guide des points d’entrée de notes](./notes.md).

## Récupération des ressources associées à une propriété {#related}

Les appels suivants montrent comment récupérer les ressources associés à une propriété. Lorsque [recherche une propriété](#lookup), ces relations sont répertoriées sous la propriété `relationships`.

Pour plus d’informations sur les relations dans l’API Reactor, consultez le [guide des relations](../guides/relationships.md).

### Liste des rappels associés à une propriété {#callbacks}

Vous pouvez répertorier les [rappels](./callbacks.md) enregistrés sur une propriété en ajoutant `/callbacks` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez répertorier les rappels. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de rappels détenus par la propriété spécifiée.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
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

### Liste des éléments de données associés à une propriété {#data-elements}

Vous pouvez répertorier les [éléments de données](./data-elements.md) qui sont détenus par une propriété en ajoutant `/data_elements` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /properties/{PROPERTY_ID}/data_elements
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez répertorier les éléments de données. |

{style="table-layout:auto"}

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

Une réponse réussie renvoie une liste d’éléments de données détenus par la propriété spécifiée.

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

### Liste des environnements associés à une propriété {#environments}

Vous pouvez répertorier les [environnements](./environments.md) qui sont détenus par une propriété en ajoutant `/environments` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /properties/{PROPERTY_ID}/environments
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez répertorier les environnements. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste d’environnements détenus par la propriété spécifiée.

```json
{
  "data": [
    {
      "id": "ENbe322acb4fc64dfdb603254ffe98b5d3",
      "type": "environments",
      "attributes": {
        "archive": false,
        "created_at": "2020-12-14T17:38:51.047Z",
        "library_path": "f9fd106ab399/cb29d726b35e",
        "library_name": "launch-c0331746ae03-development.min.js",
        "library_entry_points": [
          {
            "library_name": "launch-c0331746ae03-development.min.js",
            "minified": true,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.min.js"
            ],
            "license_path": "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
          },
          {
            "library_name": "launch-c0331746ae03-development.js",
            "minified": false,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
            ]
          }
        ],
        "name": "Development Environment A",
        "path": "https://assets.adobedtm.com/staging",
        "stage": "development",
        "updated_at": "2020-12-14T17:38:51.047Z",
        "status": "succeeded",
        "token": "c0331746ae03"
      },
      "relationships": {
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/library"
          },
          "data": null
        },
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/builds"
          }
        },
        "host": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/host",
            "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/relationships/host"
          },
          "data": {
            "id": "HTc5cae9ce1e3943aab185bdba939f98bd",
            "type": "hosts"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/property"
          },
          "data": {
            "id": "PR06c9196bc57048dd8ff169c27baeeca8",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8",
        "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3"
      },
      "meta": {
        "archive_encrypted": false
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

### Liste des extensions associées à une propriété {#extensions}

Vous pouvez répertorier les [extensions](./extensions.md) qui sont détenues par une propriété en ajoutant `/extensions` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /properties/{PROPERTY_ID}/extensions
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez répertorier les extensions. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste d’extensions détenues par la propriété spécifiée.

```json
{
  "data": [
    {
      "id": "EXd9d80c87afb6432ba823a58d3e78299b",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:40:21.000Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:40:21.000Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/property"
          },
          "data": {
            "id": "PRee071cb5b7794f42b74c913e1ad2e325",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/origin"
          },
          "data": {
            "id": "EXd9d80c87afb6432ba823a58d3e78299b",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325",
        "origin": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "self": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
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

### Liste des hôtes associés à une propriété {#hosts}

Vous pouvez répertorier les [hôtes](./hosts.md) utilisés par une propriété en ajoutant `/hosts` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /properties/{PROPERTY_ID}/hosts
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez répertorier les hôtes. |

{style="table-layout:auto"}

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

Une réponse réussie renvoie une liste d’hôtes utilisés par une propriété spécifiée.

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

### Liste des règles associées à une propriété {#rules}

Vous pouvez répertorier les [règles](./rules.md) utilisées par une propriété en ajoutant `/rules` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET  /properties/{PROPERTY_ID}/rules
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez répertorier les règles. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste de règles utilisées par une propriété spécifiée.

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

### Recherche de la société associée à une propriété {#company}

Vous pouvez rechercher la société qui détient une propriété en ajoutant `/company` au chemin d’accès d’une requête de recherche.

**Format d’API**

```http
GET /properties/{PROPERTY_ID}/company
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | `id` de la propriété dont vous souhaitez rechercher la société détentrice. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/HT5d90148e72224224aac9bc0b01498b84/company \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de la société de la propriété spécifiée.

```json
{
  "data": {
    "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.711Z",
      "name": "Reactor QE",
      "org_id": "08364A825824E04F0A494115@AdobeOrg",
      "updated_at": "2020-08-13T17:13:30.711Z",
      "token": "f9fd106ab399",
      "cjm_enabled": true,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "properties": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties",
        "manage_app_configurations"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ]
      }
    }
  }
}
```
