---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Configuration des spécifications de source pour les sources en libre-service (SDK par lots)
description: Ce document présente les configurations que vous devez préparer pour utiliser les sources en libre-service (SDK par lots).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 50%

---

# Configuration de la spécification source pour les sources en libre-service (SDK par lots)

Les spécifications de source contiennent des informations spécifiques à une source, notamment des attributs relatifs à la catégorie d’une source, au statut bêta et à l’icône de catalogue. Elles contiennent également des informations utiles telles que les paramètres d’URL, le contenu, l’en-tête et le planning. Les spécifications de source décrivent également le schéma des paramètres requis pour créer une connexion source à partir d’une connexion de base. Le schéma est nécessaire pour créer une connexion source.

Voir [annexe](#source-spec) pour un exemple de spécification de source entièrement rempli.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "host",
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| Propriété | Description | Exemple |
| --- | --- | --- |
| `sourceSpec.attributes` | Contient des informations sur la source spécifique à l’interface utilisateur ou à l’API. |
| `sourceSpec.attributes.uiAttributes` | Affiche des informations sur la source spécifique à l’interface utilisateur. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Attribut booléen qui indique si la source nécessite davantage de commentaires de la part des clients à ajouter à sa fonctionnalité. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Définit la catégorie de la source. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Définit l’icône utilisée pour le rendu de la source dans l’interface utilisateur de Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Affiche une brève description de la source. |
| `sourceSpec.attributes.uiAttributes.label` | Affiche le libellé à utiliser pour le rendu de la source dans l’interface utilisateur de Platform. |
| `sourceSpec.attributes.spec.properties.urlParams` | Contient des informations sur le chemin d’accès à la ressource URL, la méthode et les paramètres de requête pris en charge. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Définit le chemin d’accès à la ressource à partir duquel récupérer les données. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Définit la méthode HTTP à utiliser pour que la requête à la ressource récupère les données. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Définit les paramètres de requête pris en charge qui peuvent être utilisés pour ajouter l’URL source lors d’une requête de récupération de données. **Remarque** : toute valeur de paramètre fournie par l’utilisateur doit être formatée en tant qu’espace réservé. Par exemple : `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` sera ajouté à l’URL source en tant que : `/?key=value&key1=value1`. |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Définit les en-têtes qui doivent être fournis dans la requête HTTP à l’URL source lors de la récupération des données. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Cet attribut peut être configuré pour envoyer un corps HTTP par le biais d’une requête de POST. |
| `sourceSpec.attributes.spec.properties.contentPath` | Définit le nœud qui contient la liste des éléments requis à ingérer dans Platform. Cet attribut doit respecter une syntaxe de chemin d’accès JSON valide et doit pointer vers un tableau particulier. | Afficher la variable [section ressources supplémentaires](#content-path) pour un exemple de la ressource contenue dans un chemin d’accès au contenu. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Chemin d’accès qui pointe vers les enregistrements de collection à ingérer dans Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Cette propriété vous permet d’identifier des éléments spécifiques de la ressource identifiée dans le chemin d’accès du contenu qui doivent être exclus de l’ingestion. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Cette propriété vous permet de spécifier explicitement les attributs individuels que vous souhaitez conserver. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Cette propriété vous permet de remplacer la valeur du nom d’attribut que vous avez spécifiée dans `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Cette propriété vous permet d’aplatir deux tableaux et de transformer les données de ressource en ressource Platform. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Le chemin d’accès qui pointe vers les enregistrements de collection que vous souhaitez aplatir. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Cette propriété vous permet d’identifier des éléments spécifiques de la ressource identifiée dans le chemin d’accès de l’entité qui doivent être exclus de l’ingestion. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Cette propriété vous permet de spécifier explicitement les attributs individuels que vous souhaitez conserver. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Cette propriété vous permet de remplacer la valeur du nom d’attribut que vous avez spécifiée dans `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Définit les paramètres ou les champs qui doivent être fournis pour obtenir un lien vers la page suivante à partir de la réponse de page active de l’utilisateur ou lors de la création d’une URL de page suivante. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Affiche le type de pagination pris en charge pour votre source. | <ul><li>`OFFSET` : ce type de pagination vous permet d’analyser les résultats en spécifiant un index à partir duquel démarrer le tableau associé, ainsi qu’une limite du nombre de résultats renvoyés.</li><li>`POINTER` : ce type de pagination permet d’utiliser une variable `pointer` pour pointer vers un élément particulier qui doit être envoyé avec une requête. La pagination du type de pointeur nécessite un chemin d’accès dans la payload qui pointe vers la page suivante..</li><li>`CONTINUATION_TOKEN`: Ce type de pagination vous permet d’ajouter vos paramètres de requête ou d’en-tête avec un jeton de continuation pour récupérer les données renvoyées restantes de votre source, qui n’ont pas été renvoyées initialement en raison d’un maximum prédéterminé.</li><li>`PAGE`: Ce type de pagination vous permet d’ajouter votre paramètre de requête avec un paramètre de pagination pour parcourir les données renvoyées par pages, à partir de la page zéro.</li><li>`NONE`: Ce type de pagination peut être utilisé pour les sources qui ne prennent en charge aucun des types de pagination disponibles. Type de pagination `NONE` renvoie l’intégralité des données de réponse après une requête.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Nom de la limite avec laquelle l’API peut spécifier le nombre d’enregistrements à récupérer dans une page. | `limit` ou `count`. |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Nombre d’enregistrements à récupérer dans une page. | `limit=10` ou `count=10`. |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Nom de l’attribut offset. Obligatoire si le type de pagination est défini sur `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Nom de l’attribut du pointeur. Exige un chemin d’accès json vers l’attribut qui pointe vers la page suivante. Obligatoire si le type de pagination est défini sur `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contient des paramètres qui définissent les formats de planification pris en charge pour votre source. Les paramètres de planification incluent `startTime` et `endTime`, qui vous permettent de définir des intervalles de temps spécifiques pour des exécutions par lots, ce qui garantit que les enregistrements récupérés lors d’une exécution par lots précédente ne soient pas récupérés à nouveau. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Définit le nom du paramètre d’heure de début. | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Définit le nom du paramètre d’heure de fin. | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Définit le format pris en charge pour la variable `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Définit le format pris en charge pour la variable `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Définit les paramètres fournis par l’utilisateur pour récupérer les valeurs de ressource. | Voir [ressources supplémentaires](#user-input) pour un exemple de paramètres entrés par l’utilisateur pour `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Ressources supplémentaires {#appendix}

Les sections suivantes apportent des informations sur les configurations supplémentaires que vous pouvez effectuer dans votre `sourceSpec`, notamment la planification avancée et les schémas personnalisés.

### Exemple de chemin de contenu {#content-path}

Voici un exemple de contenu de la propriété `contentPath` dans une spécification de connexion [!DNL MailChimp Members].

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### Exemple d’entrée utilisateur `spec.properties` {#user-input}

Voici un exemple de variable `spec.properties` fournie par l’utilisateur à l’aide d’une spécification de connexion [!DNL MailChimp Members].

Dans cet exemple, `listId` est fourni comme faisant partie de `urlParams.path`. Si vous devez récupérer le `listId` d’un client, vous devez également le définir comme faisant partie de `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Exemple de spécification de source {#source-spec}

Voici une spécification de source complétée à l’aide de [!DNL MailChimp Members] :

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "host": "https://{domain}.api.mailchimp.com",
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### Configuration de différents types de pagination pour votre source {#pagination}

Vous trouverez ci-dessous des exemples d’autres types de pagination pris en charge par les sources en libre-service (SDK par lots) :

#### `CONTINUATION_TOKEN`

Un type de pagination de jeton de continuation renvoie un jeton de chaîne qui signifie qu’il existe d’autres éléments qui n’ont pas pu être renvoyés, en raison d’un nombre maximal d’éléments prédéterminé qui peuvent être renvoyés dans une seule réponse.

Une source qui prend en charge le type de pagination des jetons de continuation peut avoir un paramètre de pagination similaire à :

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| Propriété | Description |
| --- | --- |
| `type` | Type de pagination utilisé pour renvoyer des données. |
| `continuationTokenPath` | La valeur qui doit être ajoutée aux paramètres de requête afin de passer à la page suivante des résultats renvoyés. |
| `parameterType` | Le `parameterType` définit l’emplacement où la propriété `parameterName` doit être ajouté. Le `QUERYPARAM` vous permet d’ajouter votre requête à l’aide de la propriété `parameterName`. Le `HEADERPARAM` vous permet d’ajouter `parameterName` à votre requête d’en-tête. |
| `parameterName` | Nom du paramètre utilisé pour incorporer le jeton de continuation. Le format est le suivant : `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | Le `delayRequestMillis` dans la pagination, vous permet de contrôler le taux de requêtes envoyées à votre source. Certaines sources peuvent avoir une limite au nombre de requêtes que vous pouvez effectuer par minute. Par exemple : [!DNL Zendesk] est limitée à 100 requêtes par minute et définit  `delayRequestMillis` to `850` vous permet de configurer la source pour effectuer des appels à environ 80 demandes par minute, bien en dessous du seuil de 100 demandes par minute. |

Voici un exemple de réponse renvoyée à l’aide du type de pagination du jeton de continuation :

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

#### `PAGE`

Le `PAGE` type de pagination permet de parcourir les données renvoyées par nombre de pages commençant par zéro. Lors de l’utilisation de `PAGE` type pagination, vous devez indiquer le nombre d&#39;enregistrements sur une seule page.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| Propriété | Description |
| --- | --- |
| `type` | Type de pagination utilisé pour renvoyer des données. |
| `limitName` | Nom de la limite avec laquelle l’API peut spécifier le nombre d’enregistrements à récupérer dans une page. |
| `limitValue` | Nombre d’enregistrements à récupérer dans une page. |
| `pageParamName` | Nom du paramètre que vous devez ajouter aux paramètres de requête pour parcourir les différentes pages des données renvoyées. Par exemple : `https://abc.com?pageIndex=1` renvoie la deuxième page de la charge utile renvoyée par une API. |
| `maximumRequest` | Nombre maximal de requêtes qu’une source peut effectuer pour une exécution incrémentielle donnée. La limite par défaut actuelle est de 10 000. |

#### `NONE`

Le `NONE` Le type de pagination peut être utilisé pour les sources qui ne prennent en charge aucun des types de pagination disponibles. Sources qui utilisent le type de pagination de `NONE` renvoyez simplement tous les enregistrements récupérables lorsqu’une demande de GET est effectuée.

```json
"paginationParams": {
  "type": "NONE"
}
```

### Planification avancée pour les sources en libre-service (SDK par lots)

Configurez le planning incrémentiel et de renvoi de votre source à l’aide d’une planification avancée. Le `incremental` vous permet de configurer un planning dans lequel votre source n’ingèrera que des enregistrements nouveaux ou modifiés, tandis que la propriété `backfill` vous permet de créer un planning pour l’ingestion de données historiques.

Avec la planification avancée, vous pouvez utiliser des expressions et des fonctions spécifiques à votre source pour configurer les plannings incrémentiels et de renvoi. Dans l’exemple ci-dessous, la variable [!DNL Zendesk] La source nécessite que le planning incrémentiel soit formaté comme `type:user updated > {START_TIME} updated < {END_TIME}` et renvoyer en tant que `type:user updated < {END_TIME}`.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| Propriété | Description |
| --- | --- |
| `scheduleParams.type` | Le type de planification que votre source utilisera. Définissez cette valeur sur `ADVANCE` pour utiliser le type de planification avancé. |
| `scheduleParams.paramFormat` | Le format défini de votre paramètre de planification. Cette valeur peut être identique à celle de la source `scheduleStartParamFormat` et `scheduleEndParamFormat` valeurs. |
| `scheduleParams.incremental` | Requête incrémentale de votre source. Incrémentiel fait référence à une méthode d’ingestion dans laquelle seules les données nouvelles ou modifiées sont ingérées. |
| `scheduleParams.backfill` | Requête de renvoi de la source. Le renvoi désigne une méthode d’ingestion dans laquelle des données historiques sont ingérées. |

Une fois que vous avez configuré la planification avancée, vous devez alors vous référer à la section `scheduleParams` dans la section des paramètres d’URL, de corps ou d’en-tête, selon ce que votre source particulière prend en charge. Dans l’exemple ci-dessous, `{SCHEDULE_QUERY}` est un espace réservé utilisé pour spécifier où les expressions de planification incrémentielle et de renvoi seront utilisées. Dans le cas d’un [!DNL Zendesk] source, `query` est utilisé dans la variable `queryParams` pour spécifier une planification avancée.

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### Ajout d’un schéma personnalisé pour définir les attributs dynamiques de la source

Vous pouvez inclure un schéma personnalisé à votre `sourceSpec` pour définir tous les attributs requis pour votre source, y compris les attributs dynamiques dont vous pourriez avoir besoin. Vous pouvez mettre à jour la spécification de connexion correspondante de votre source en adressant une requête de PUT à la fonction `/connectionSpecs` point d’entrée du [!DNL Flow Service] lors de la fourniture de votre schéma personnalisé dans la variable `sourceSpec` de votre spécification de connexion.

Voici un exemple de schéma personnalisé que vous pouvez ajouter à la spécification de connexion de votre source :

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## Étapes suivantes

Une fois vos spécifications de source renseignées, vous pouvez procéder à la configuration des spécifications d’exploration pour la source que vous souhaitez intégrer à Platform. Voir le document sur la [configuration des spécifications d’exploration](./explorespec.md) pour plus d’informations.
