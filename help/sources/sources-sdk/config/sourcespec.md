---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Configuration des spécifications d’authentification pour le SDK Sources
topic-legacy: overview
description: Ce document présente les configurations que vous devez préparer pour utiliser le SDK Sources.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 1%

---


# Configuration de la spécification source pour le SDK Sources

Les spécifications source contiennent des informations spécifiques à une source, notamment des attributs relatifs à la catégorie d’une source, à l’état bêta et à l’icône de catalogue. Elles contiennent également des informations utiles telles que les paramètres d’URL, le contenu, l’en-tête et la planification. Les spécifications source décrivent également le schéma des paramètres requis pour créer une connexion source à partir d’une connexion de base. Le schéma est nécessaire pour créer une connexion source.

Voir [annexe](#source-spec) pour un exemple de spécification source entièrement renseignée.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "{CATEGORY}"
      },
      "icon": {
        "key": "{ICON}"
      },
      "description": {
        "key": "{DESCRIPTION}"
      },
      "label": {
        "key": "{LABEL}"
      }
    },
    "urlParams": {
      "path": "{RESOURCE_PATH}",
      "method": "{GET_or_POST}",
      "queryParams": "{QUERY_PARAMS}"
    },
    "headerParams": "{HEADER_VALUES}",
    "bodyParams": "{BODY_PARAMS_USED_IF_METHOD_IS_POST}",
    "contentPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "explodeEntityPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "paginationParams": {
      "type": "{OFFSET_OR_POINTER}",
      "limitName": "{NUMBER_OF_RECORDS_ATTRIBUTE_NAME}",
      "limitValue": "{NUMBER_OF_RECORDS_PER_PAGE}",
      "offSetName": "{OFFSET_ATTRIBUTE_NAME_REQUIRED_IN_CASE_OF_OFFSET BASED_PAGINATION}",
      "pointerName": "{POINTER_PATH_REQUIRED_IN__CASE_OF_POINTER BASED_PAGINATION}"
    },
    "scheduleParams": {
      "scheduleStartParamName": "{START_TIME_PARAMETER_NAME}",
      "scheduleEndParamName": "{END_TIME_PARAMETER_NAME}",
      "scheduleStartParamFormat": "{DATE_TIME_FORMAT_FOR_START_TIME}",
      "scheduleEndParamFormat": "{END_TIME_FORMAT_FOR_START_TIME}"
    }
  },
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define user input parameters to fetch resource values.",
    "properties": "{USER_INPUT}"
  }
}
```

| Propriété | Description | Exemple |
| --- | --- | --- |
| `sourceSpec.attributes` | Contient des informations sur la source spécifique à l’interface utilisateur ou à l’API. |
| `sourceSpec.attributes.uiAttributes` | Affiche des informations sur la source spécifique à l’interface utilisateur. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Attribut boolean qui indique si la source nécessite davantage de commentaires de la part des clients pour ajouter à ses fonctionnalités. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Définit la catégorie de la source. | <ul><li>`advertising`</li><li>`cloud storage`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li><li>`streaming`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Définit l’icône utilisée pour le rendu de la source dans l’interface utilisateur de Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Affiche une brève description de la source. |
| `sourceSpec.attributes.uiAttributes.label` | Affiche le libellé à utiliser pour le rendu de la source dans l’interface utilisateur de Platform. |
| `sourceSpec.attributes.urlParams` | Contient des informations sur le chemin, la méthode et les paramètres de requête pris en charge de la ressource URL. |
| `sourceSpec.attributes.urlParams.path` | Définit le chemin d’accès à la ressource d’où récupérer les données. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.urlParams.method` | Définit la méthode HTTP à utiliser pour envoyer la requête à la ressource pour récupérer les données. | `GET`, `POST` |
| `sourceSpec.attributes.urlParams.queryParams` | Définit les paramètres de requête pris en charge qui peuvent être utilisés pour ajouter l’URL source lors d’une requête de récupération de données. Les paramètres de requête doivent être une virgule (`,`) des paires clé-valeur séparées. **Remarque**: Toute valeur de paramètre fournie par l’utilisateur doit être formatée en tant qu’espace réservé. Par exemple : `${USER_PARAMETER}`. | `exclude_fields=emails._links,id=${id}` |
| `sourceSpec.attributes.headerParams` | Définit la virgule (`,`) des en-têtes séparés qui doivent être fournis dans la requête HTTP à l’URL source lors de la récupération des données. | `Content-Type=application/json,foo=bar&userHeader={{USER_HEADER_VALUE}}` |
| `sourceSpec.attributes.bodyParams` | Définit les paramètres de corps requis. Cette propriété n’est utilisée que si `urlParams.method` est défini sur `POST`. |
| `sourceSpec.attributes.contentPath` | Définit le noeud qui contient la liste des éléments à ingérer dans Platform. Cet attribut doit respecter une syntaxe de chemin JSON valide et doit pointer vers un tableau particulier. | Voir [annexe](#content-path) pour un exemple de la ressource contenue dans un chemin d’accès au contenu. |
| `sourceSpec.attributes.contentPath.path` | Chemin d’accès qui pointe vers les enregistrements de collection à ingérer dans Platform. | `$.emails` |
| `sourceSpec.attributes.contentPath.skipAttributes` | Cette propriété vous permet d’identifier des éléments spécifiques de la ressource identifiée dans le chemin de contenu qui doivent être exclus de l’ingestion. |
| `sourceSpec.attributes.contentPath.overrideWrapperAttribute` | Cette propriété vous permet de remplacer la valeur du nom d’attribut que vous avez spécifiée dans `contentPath`. |
| `sourceSpec.attributes.contentPath.keepAttributes` | Cette propriété vous permet de spécifier explicitement les attributs individuels que vous souhaitez mapper. |
| `sourceSpec.attributes.explodeEntityPath` | Cette propriété vous permet d’aplatir deux tableaux et de transformer les données de ressource en ressource Platform. |
| `sourceSpec.attributes.explodeEntityPath.path` | Le chemin qui pointe vers les enregistrements de collection que vous souhaitez aplatir. | `$.email.activity` |
| `sourceSpec.attributes.explodeEntityPath.skipAttributes` | Cette propriété vous permet d’identifier des éléments spécifiques de la ressource identifiée dans le chemin d’accès de l’entité qui doivent être exclus de l’ingestion. |
| `sourceSpec.attributes.explodeEntityPath.overrideWrapperAttribute` | Cette propriété vous permet de remplacer la valeur du nom d’attribut que vous avez spécifiée dans `explodeEntityPath`. |
| `sourceSpec.attributes.explodeEntityPath.keepAttributes` | Cette propriété vous permet de spécifier explicitement les attributs individuels que vous souhaitez mapper. |
| `sourceSpec.attributes.paginationParams` | Définit les paramètres ou les champs qui doivent être fournis pour obtenir un lien vers la page suivante à partir de la réponse de page active de l’utilisateur ou lors de la création d’une URL de page suivante. |
| `sourceSpec.attributes.paginationParams.type` | Affiche le type de pagination pris en charge pour votre source. | <ul><li>`offset`: Ce type de pagination vous permet d’analyser les résultats en spécifiant un index à partir duquel démarrer le tableau résultant, ainsi qu’une limite sur le nombre de résultats renvoyés.</li><li>`pointer`: Ce type de pagination permet d’utiliser une `pointer` pour pointer vers un élément particulier qui doit être envoyé avec une requête. La pagination du type de pointeur nécessite un chemin dans la payload qui pointe vers la page suivante.</li></ul> |
| `sourceSpec.attributes.paginationParams.limitName` | Nom de la limite par laquelle l’API peut spécifier le nombre d’enregistrements à récupérer dans une page. | `count` |
| `sourceSpec.attributes.paginationParams.limitValue` | Nombre d’enregistrements à récupérer dans une page. | `100` |
| `sourceSpec.attributes.paginationParams.offSetName` | Nom de l’attribut offset. Cela est requis si le type de pagination est défini sur `offset`. | `offset` |
| `sourceSpec.attributes.paginationParams.pointerName` | Nom de l’attribut du pointeur. Cela nécessite un chemin json vers l’attribut qui pointe vers la page suivante. Cela est requis si le type de pagination est défini sur `pointer`. | `pointer` |
| `sourceSpec.attributes.scheduleParams` | Contient des paramètres qui définissent les formats de planification pris en charge pour votre source. Les paramètres de planification incluent `startTime` et `endTime`, qui vous permet de définir des intervalles de temps spécifiques pour les exécutions de lot, ce qui garantit que les enregistrements récupérés lors d’une exécution de lot précédente ne sont pas récupérés à nouveau. |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamName` | Définit le nom du paramètre d’heure de début | `since_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamName` | Définit le nom du paramètre d’heure de fin | `before_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamFormat` | Définit le format pris en charge pour la variable `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamFormat` | Définit le format pris en charge pour la variable `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Définit les paramètres fournis par l’utilisateur pour récupérer les valeurs de ressource. | Voir [annexe](#user-input) pour un exemple de paramètres entrés par l’utilisateur pour `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Annexe {#appendix}

### Exemple de chemin de contenu {#content-path}

Voici un exemple du contenu de la variable `contentPath` dans une propriété [!DNL MailChimp Campaigns] spécification de connexion.

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

### `spec.properties` exemple d’entrée utilisateur {#user-input}

Voici un exemple d’utilisation fournie par l’utilisateur. `spec.properties` à l’aide d’une [!DNL MailChimp Members] spécification de connexion.

Dans cet exemple, `listId` est fourni dans `urlParams.path`. Si vous devez récupérer `listId` d’un client, vous devez également le définir comme faisant partie de `spec.properties`.


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

Voici une spécification source complétée à l’aide de [!DNL MailChimp Members]:

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

Une fois vos spécifications source renseignées, vous pouvez procéder à la configuration des spécifications d’exploration pour la source que vous souhaitez intégrer à Platform. Voir le document sur [configuration des spécifications d’exploration](./explorespec.md) pour plus d’informations.