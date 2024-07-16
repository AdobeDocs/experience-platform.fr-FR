---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux;API de service de flux;sources;sources
title: Filtrage Des Données Au Niveau De La Ligne Pour Un Source À L’Aide De L’API Flow Service
description: Ce tutoriel décrit les étapes de filtrage des données au niveau de la source à l’aide de l’API Flow Service
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: b0e2fc4767fb6fbc90bcdd3350b3add965988f8f
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 14%

---

# Filtrage des données au niveau des lignes pour une source à l’aide de l’API [!DNL Flow Service]

>[!IMPORTANT]
>
>La prise en charge du filtrage des données au niveau des lignes n’est actuellement disponible que pour les sources suivantes :
>
>* [Google BigQuery](../../connectors/databases/bigquery.md)
>* [Microsoft Dynamics](../../connectors/crm/ms-dynamics.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Snowflake](../../connectors/databases/snowflake.md)

Ce tutoriel décrit les étapes à suivre pour filtrer les données au niveau des lignes pour une source à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Filtrage des données source

Les étapes suivantes décrivent les étapes à suivre pour filtrer les données au niveau de la ligne pour votre source.

### Recherche des spécifications de connexion

Avant de pouvoir utiliser l’API pour filtrer les données au niveau des lignes d’une source, vous devez d’abord récupérer les détails de spécification de connexion de votre source afin de déterminer les opérateurs et la langue pris en charge par une source spécifique.

Pour récupérer la spécification de connexion d’une source donnée, envoyez une requête GET au point de terminaison `/connectionSpecs` de l’API [!DNL Flow Service] tout en fournissant le nom de propriété de votre source dans le cadre de vos paramètres de requête.

**Format d’API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs selon lesquels filtrer les résultats. Vous pouvez récupérer la spécification de connexion [!DNL Google BigQuery] en appliquant la propriété `name` et en spécifiant `"google-big-query"` dans votre recherche. |

**Requête**

La requête suivante récupère les spécifications de connexion pour [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les spécifications de connexion pour [!DNL Google BigQuery], y compris des informations sur le langage de requête et les opérateurs logiques pris en charge.

>[!NOTE]
>
>La réponse de l’API ci-dessous est tronquée pour des raisons de concision.

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| Propriété | Description |
| --- | --- |
| `attributes.filterAtSource.enabled` | Détermine si la source interrogée prend en charge le filtrage des données au niveau de la ligne. |
| `attributes.filterAtSource.queryLanguage` | Détermine le langage de requête pris en charge par la source interrogée. |
| `attributes.filterAtSource.logicalOperators` | Détermine les opérateurs logiques que vous pouvez utiliser pour filtrer les données au niveau de la ligne pour votre source. |
| `attributes.filterAtSource.comparisonOperators` | Détermine les opérateurs de comparaison que vous pouvez utiliser pour filtrer les données au niveau de la ligne pour votre source. Pour plus d’informations sur les opérateurs de comparaison, reportez-vous au tableau ci-dessous. |
| `attributes.filterAtSource.columnNameEscapeChar` | Détermine le caractère à utiliser pour échapper les colonnes. |
| `attributes.filterAtSource.valueEscapeChar` | Détermine la manière dont les valeurs seront entourées lors de l’écriture d’une requête SQL. |

{style="table-layout:auto"}

#### Opérateurs de comparaison 

| Opérateur | Description |
| --- | --- |
| `==` | Filtre selon si la propriété est égale à la valeur fournie. |
| `!=` | Filtre selon si la propriété n’est pas égale à la valeur fournie. |
| `<` | Filtre selon si la propriété est inférieure à la valeur fournie. |
| `>` | Filtre selon si la propriété est supérieure ou non à la valeur fournie. |
| `<=` | Filtre selon si la propriété est inférieure ou égale à la valeur fournie. |
| `>=` | Filtre selon si la propriété est supérieure ou égale à la valeur fournie. |
| `like` | Filtre en utilisant une clause `WHERE` pour rechercher un modèle spécifié. |
| `in` | Filtre selon si la propriété se trouve dans une plage spécifiée. |

{style="table-layout:auto"}

### Définition des conditions de filtrage pour l’ingestion

Une fois que vous avez identifié les opérateurs logiques et le langage de requête pris en charge par votre source, vous pouvez utiliser Profile Query Language (PQL) pour spécifier les conditions de filtrage à appliquer à vos données source.

Dans l’exemple ci-dessous, les conditions sont appliquées uniquement à la sélection des données qui correspondent aux valeurs fournies pour les types de noeuds répertoriés en tant que paramètres.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### Prévisualiser vos données

Vous pouvez prévisualiser vos données en envoyant une requête de GET au point de terminaison `/explore` de l’API [!DNL Flow Service] tout en fournissant `filters` dans le cadre de vos paramètres de requête et en spécifiant vos conditions d’entrée PQL dans [!DNL Base64].

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | L’identifiant de connexion de base de votre source. |
| `{TABLE_PATH}` | La propriété path de la table que vous souhaitez inspecter. |
| `{FILTERS}` | Vos conditions de filtrage PQL codées dans [!DNL Base64]. |

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une requête réussie renvoie la réponse suivante.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### Créer une connexion source pour les données filtrées

Pour créer une connexion source et ingérer des données filtrées, envoyez une requête de POST au point de terminaison `/sourceConnections` tout en fournissant vos conditions de filtrage dans le cadre de vos paramètres de corps.

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

La requête suivante crée une connexion source pour ingérer des données à partir de `test1.fasTestTable` où `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source nouvellement créée.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Annexe

Cette section fournit d’autres exemples de payloads différents pour le filtrage.

### Conditions uniques

Vous pouvez omettre le `fnApply` initial pour les scénarios qui ne nécessitent qu’une seule condition.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### Utilisation de l’opérateur `in`

Consultez l’exemple de payload ci-dessous pour obtenir un exemple de l’opérateur `in`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### Utilisation de l’opérateur `isNull`

Consultez l’exemple de payload ci-dessous pour obtenir un exemple de l’opérateur `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### Utilisation de l’opérateur `NOT`

Consultez l’exemple de payload ci-dessous pour obtenir un exemple de l’opérateur `NOT`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### Exemple avec conditions imbriquées

Consultez l’exemple de payload ci-dessous pour obtenir un exemple de conditions imbriquées complexes.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
