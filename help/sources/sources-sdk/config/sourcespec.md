---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Configuration des spécifications de source pour les sources en libre-service (SDK par lots)
description: Ce document présente les configurations que vous devez préparer pour utiliser les sources en libre-service (SDK par lots).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 1fdce7c798d8aff49ab4953298ad7aa8dddb16bd
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 43%

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
| `sourceSpec.attributes.spec.properties.contentPath` | Définit le nœud qui contient la liste des éléments requis à ingérer dans Platform. Cet attribut doit respecter une syntaxe de chemin d’accès JSON valide et doit pointer vers un tableau particulier. | Affichez la [section ressources supplémentaires](#content-path) pour obtenir un exemple de la ressource contenue dans un chemin d’accès au contenu. |
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
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Affiche le type de pagination pris en charge pour votre source. | <ul><li>`OFFSET` : ce type de pagination vous permet d’analyser les résultats en spécifiant un index à partir duquel démarrer le tableau associé, ainsi qu’une limite du nombre de résultats renvoyés.</li><li>`POINTER` : ce type de pagination permet d’utiliser une variable `pointer` pour pointer vers un élément particulier qui doit être envoyé avec une requête. La pagination du type de pointeur nécessite un chemin dans la payload qui pointe vers la page suivante.</li><li>`CONTINUATION_TOKEN` : Ce type de pagination vous permet d’ajouter vos paramètres de requête ou d’en-tête avec un jeton de continuation pour récupérer les données renvoyées restantes de votre source, qui n’ont pas été renvoyées initialement en raison d’un maximum prédéterminé.</li><li>`PAGE` : Ce type de pagination vous permet d’ajouter votre paramètre de requête avec un paramètre de pagination à parcourir par les données renvoyées par les pages, à partir de la page zéro.</li><li>`NONE` : Ce type de pagination peut être utilisé pour les sources qui ne prennent en charge aucun des types de pagination disponibles. Le type de pagination `NONE` renvoie l’intégralité des données de réponse après une requête.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Nom de la limite avec laquelle l’API peut spécifier le nombre d’enregistrements à récupérer dans une page. | `limit` ou `count`. |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Nombre d’enregistrements à récupérer dans une page. | `limit=10` ou `count=10`. |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Nom de l’attribut offset. Obligatoire si le type de pagination est défini sur `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Nom de l’attribut du pointeur. Exige un chemin d’accès json vers l’attribut qui pointe vers la page suivante. Obligatoire si le type de pagination est défini sur `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contient des paramètres qui définissent les formats de planification pris en charge pour votre source. Les paramètres de planification incluent `startTime` et `endTime`, qui vous permettent de définir des intervalles de temps spécifiques pour des exécutions par lots, ce qui garantit que les enregistrements récupérés lors d’une exécution par lots précédente ne soient pas récupérés à nouveau. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Définit le nom du paramètre d’heure de début. | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Définit le nom du paramètre d’heure de fin. | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Définit le format pris en charge pour la variable `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Définit le format pris en charge pour la variable `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Définit les paramètres fournis par l’utilisateur pour récupérer les valeurs de ressource. | Voir les [ressources supplémentaires](#user-input) pour obtenir un exemple de paramètres entrés par l’utilisateur pour `spec.properties`. |

{style="table-layout:auto"}

## Ressources supplémentaires {#appendix}

Les sections suivantes fournissent des informations sur les configurations supplémentaires que vous pouvez effectuer sur votre `sourceSpec`, y compris la planification avancée et les schémas personnalisés.

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

>[!BEGINTABS]

>[!TAB Décalage]

Ce type de pagination vous permet d’analyser les résultats en spécifiant un index à partir duquel démarrer le tableau résultant, ainsi qu’une limite sur le nombre de résultats renvoyés. Par exemple :

```json
"paginationParams": {
        "type": "OFFSET",
        "limitName": "limit",
        "limitValue": "4",
        "offSetName": "offset",
        "endConditionName": "$.hasMore",
        "endConditionValue": "Const:false"
}
```

| Propriété | Description |
| --- | --- |
| `type` | Type de pagination utilisé pour renvoyer des données. |
| `limitName` | Nom de la limite avec laquelle l’API peut spécifier le nombre d’enregistrements à récupérer dans une page. |
| `limitValue` | Nombre d’enregistrements à récupérer dans une page. |
| `offSetName` | Nom de l’attribut offset. Obligatoire si le type de pagination est défini sur `offset`. |
| `endConditionName` | Une valeur définie par l’utilisateur qui indique la condition qui mettra fin à la boucle de pagination dans la requête HTTP suivante. Vous devez indiquer le nom de l’attribut sur lequel vous souhaitez mettre la condition de fin. |
| `endConditionValue` | La valeur d’attribut sur laquelle vous souhaitez mettre la condition de fin. |

>[!TAB Pointer]

Ce type de pagination permet d’utiliser une variable `pointer` pour pointer vers un élément particulier qui doit être envoyé avec une requête. La pagination du type de pointeur nécessite un chemin dans la payload qui pointe vers la page suivante. Par exemple :

```json
{
 "type": "POINTER",
 "limitName": "limit",
 "limitValue": 1,
 "pointerPath": "paging.next"
}
```

| Propriété | Description |
| --- | --- |
| `type` | Type de pagination utilisé pour renvoyer des données. |
| `limitName` | Nom de la limite avec laquelle l’API peut spécifier le nombre d’enregistrements à récupérer dans une page. |
| `limitValue` | Nombre d’enregistrements à récupérer dans une page. |
| `pointerPath` | Nom de l’attribut du pointeur. Cela nécessite un chemin json vers l’attribut qui pointe vers la page suivante. |

>[!TAB Jeton de maintien]

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
| `parameterType` | La propriété `parameterType` définit l’emplacement où `parameterName` doit être ajouté. Le type `QUERYPARAM` vous permet d’ajouter votre requête avec le `parameterName`. `HEADERPARAM` vous permet d’ajouter votre `parameterName` à votre requête d’en-tête. |
| `parameterName` | Nom du paramètre utilisé pour incorporer le jeton de continuation. Le format est le suivant : `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | La propriété `delayRequestMillis` de la pagination vous permet de contrôler le taux de requêtes effectuées à votre source. Certaines sources peuvent avoir une limite au nombre de requêtes que vous pouvez effectuer par minute. Par exemple, [!DNL Zendesk] a une limite de 100 requêtes par minute et la définition de `delayRequestMillis` sur `850` vous permet de configurer la source pour effectuer des appels à seulement 80 requêtes par minute, bien en dessous du seuil de 100 requêtes par minute. |

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

>[!TAB Page]

Le type de pagination `PAGE` vous permet de parcourir les données renvoyées par nombre de pages commençant à zéro. Lors de l&#39;utilisation de la pagination de type `PAGE`, vous devez indiquer le nombre d&#39;enregistrements donnés dans une seule page.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "pageSize",
  "limitValue": 100,
  "initialPageIndex": 1,
  "endPageIndex": "headers.x-pagecount",
  "pageParamName": "pageNumber",
  "maximumRequest": 10000
}
```

| Propriété | Description |
| --- | --- |
| `type` | Type de pagination utilisé pour renvoyer des données. |
| `limitName` | Nom de la limite avec laquelle l’API peut spécifier le nombre d’enregistrements à récupérer dans une page. |
| `limitValue` | Nombre d’enregistrements à récupérer dans une page. |
| `initialPageIndex` | (Facultatif) L’index de page initial définit le numéro de page à partir duquel la pagination commencera. Ce champ peut être utilisé pour les sources où la pagination ne commence pas par 0. Si elle n’est pas fournie, l’index de page initial est défini par défaut sur 0. Ce champ exige un entier. |
| `endPageIndex` | (Facultatif) L’index de page de fin vous permet d’établir une condition de fin et d’arrêter la pagination. Ce champ peut être utilisé lorsque les conditions de fin par défaut pour arrêter la pagination ne sont pas disponibles. Ce champ peut également être utilisé si le nombre de pages à ingérer ou le dernier numéro de page est fourni par le biais de l’en-tête de réponse, ce qui est courant lors de l’utilisation de la pagination de type `PAGE`. La valeur de l’index de page de fin peut être le dernier numéro de page ou une valeur d’expression de type chaîne de l’en-tête de réponse. Par exemple, vous pouvez utiliser `headers.x-pagecount` pour affecter l’index de page de fin à la valeur `x-pagecount` des en-têtes de réponse. **Remarque** : `x-pagecount` est un en-tête de réponse obligatoire pour certaines sources et contient le nombre de pages à ingérer. |
| `pageParamName` | Nom du paramètre que vous devez ajouter aux paramètres de requête pour parcourir les différentes pages des données renvoyées. Par exemple, `https://abc.com?pageIndex=1` renvoie la deuxième page de la payload renvoyée par une API. |
| `maximumRequest` | Nombre maximal de requêtes qu’une source peut effectuer pour une exécution incrémentielle donnée. La limite par défaut actuelle est de 10 000. |

{style="table-layout:auto"}


>[!TAB None]

Le type de pagination `NONE` peut être utilisé pour les sources qui ne prennent en charge aucun des types de pagination disponibles. Les sources qui utilisent le type de pagination `NONE` renvoient simplement tous les enregistrements récupérables lorsqu’une demande de GET est effectuée.

```json
"paginationParams": {
  "type": "NONE"
}
```

>[!ENDTABS]

### Planification avancée pour les sources en libre-service (SDK par lots)

Configurez le planning incrémentiel et de renvoi de votre source à l’aide d’une planification avancée. La propriété `incremental` vous permet de configurer un planning dans lequel votre source n’ingèrera que les enregistrements nouveaux ou modifiés, tandis que la propriété `backfill` vous permet de créer un planning pour ingérer les données historiques.

Avec la planification avancée, vous pouvez utiliser des expressions et des fonctions spécifiques à votre source pour configurer les plannings incrémentiels et de renvoi. Dans l’exemple ci-dessous, la source [!DNL Zendesk] nécessite que le planning incrémentiel soit formaté en tant que `type:user updated > {START_TIME} updated < {END_TIME}` et que le renvoi soit `type:user updated < {END_TIME}`.

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
| `scheduleParams.paramFormat` | Le format défini de votre paramètre de planification. Cette valeur peut être identique aux valeurs `scheduleStartParamFormat` et `scheduleEndParamFormat` de votre source. |
| `scheduleParams.incremental` | Requête incrémentale de votre source. Incrémentiel fait référence à une méthode d’ingestion dans laquelle seules les données nouvelles ou modifiées sont ingérées. |
| `scheduleParams.backfill` | Requête de renvoi de la source. Le renvoi désigne une méthode d’ingestion dans laquelle des données historiques sont ingérées. |

Une fois que vous avez configuré la planification avancée, vous devez vous référer à votre `scheduleParams` dans la section Paramètres d’URL, de corps ou d’en-tête, en fonction de ce que votre source particulière prend en charge. Dans l’exemple ci-dessous, `{SCHEDULE_QUERY}` est un espace réservé utilisé pour spécifier où les expressions de planification incrémentielle et de renvoi seront utilisées. Dans le cas d&#39;une source [!DNL Zendesk], `query` est utilisé dans le `queryParams` pour spécifier une planification avancée.

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

Vous pouvez inclure un schéma personnalisé dans votre `sourceSpec` pour définir tous les attributs requis pour votre source, y compris tous les attributs dynamiques dont vous pourriez avoir besoin. Vous pouvez mettre à jour la spécification de connexion correspondante de votre source en envoyant une requête de PUT au point de terminaison `/connectionSpecs` de l’API [!DNL Flow Service], tout en fournissant votre schéma personnalisé dans la section `sourceSpec` de votre spécification de connexion.

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

Une fois vos spécifications de source renseignées, vous pouvez procéder à la configuration des spécifications d’exploration pour la source que vous souhaitez intégrer à Platform. Pour plus d’informations, consultez le document sur la [configuration des spécifications d’exploration](./explorespec.md) .
