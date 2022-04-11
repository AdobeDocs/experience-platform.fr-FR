---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Configurer les spécifications d’authentification pour le SDK Sources
topic-legacy: overview
description: Ce document présente les configurations que vous devez préparer pour utiliser le SDK Sources.
hide: true
hidefromtoc: true
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 4c4c89ab7db7d3546163d707ac80210561c2fa02
workflow-type: ht
source-wordcount: '861'
ht-degree: 100%

---

# Configurer la spécification de source pour le SDK Sources

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
| `sourceSpec.attributes.spec.properties.contentPath` | Définit le nœud qui contient la liste des éléments requis à ingérer dans Platform. Cet attribut doit respecter une syntaxe de chemin d’accès JSON valide et doit pointer vers un tableau particulier. | Voir [annexe](#content-path) pour un exemple de la ressource contenue dans un chemin d’accès au contenu. |
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
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Affiche le type de pagination pris en charge pour votre source. | <ul><li>`offset` : ce type de pagination vous permet d’analyser les résultats en spécifiant un index à partir duquel démarrer le tableau associé, ainsi qu’une limite du nombre de résultats renvoyés.</li><li>`pointer` : ce type de pagination permet d’utiliser une variable `pointer` pour pointer vers un élément particulier qui doit être envoyé avec une requête. La pagination du type de pointeur nécessite un chemin d’accès dans la payload qui pointe vers la page suivante.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Nom de la limite avec laquelle l’API peut spécifier le nombre d’enregistrements à récupérer dans une page. | `limit` ou `count`. |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Nombre d’enregistrements à récupérer dans une page. | `limit=10` ou `count=10`. |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Nom de l’attribut offset. Obligatoire si le type de pagination est défini sur `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Nom de l’attribut du pointeur. Exige un chemin d’accès json vers l’attribut qui pointe vers la page suivante. Obligatoire si le type de pagination est défini sur `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contient des paramètres qui définissent les formats de planification pris en charge pour votre source. Les paramètres de planification incluent `startTime` et `endTime`, qui vous permettent de définir des intervalles de temps spécifiques pour des exécutions par lots, ce qui garantit que les enregistrements récupérés lors d’une exécution par lots précédente ne soient pas récupérés à nouveau. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Définit le nom du paramètre d’heure de début. | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Définit le nom du paramètre d’heure de fin. | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Définit le format pris en charge pour la variable `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Définit le format pris en charge pour la variable `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Définit les paramètres fournis par l’utilisateur pour récupérer les valeurs de ressource. | Voir [annexe](#user-input) pour un exemple de paramètres entrés par l’utilisateur pour `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Annexe {#appendix}

### Exemple de chemin de contenu {#content-path}

Voici un exemple de contenu de la propriété `contentPath` dans une spécification de connexion [!DNL MailChimp Campaigns].

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

## Étapes suivantes

Une fois vos spécifications de source renseignées, vous pouvez procéder à la configuration des spécifications d’exploration pour la source que vous souhaitez intégrer à Platform. Voir le document sur la [configuration des spécifications d’exploration](./explorespec.md) pour plus d’informations.
