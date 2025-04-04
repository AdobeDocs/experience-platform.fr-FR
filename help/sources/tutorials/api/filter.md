---
title: Filtrer les données au niveau des lignes pour un Source à l’aide de l’API Flow Service
description: Ce tutoriel décrit les étapes à suivre pour filtrer les données au niveau source à l’aide de l’API Flow Service
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1823'
ht-degree: 15%

---

# Filtrer les données au niveau des lignes pour une source à l’aide de l’API [!DNL Flow Service]

>[!AVAILABILITY]
>
>Actuellement, la prise en charge du filtrage des données au niveau des lignes n’est disponible que pour les sources suivantes :
>
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)
>* [[!DNL Marketo Engage] activités standard](../../connectors/adobe-applications/marketo/marketo.md)

Lisez ce guide pour savoir comment filtrer les données au niveau des lignes pour une source à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../landing/api-guide.md).

## Filtrer les données sources {#filter-source-data}

Les étapes suivantes permettent de filtrer les données au niveau des lignes pour votre source.

### Récupérer les spécifications de connexion {#retrieve-your-connection-specs}

La première étape du filtrage des données au niveau des lignes pour votre source consiste à récupérer les spécifications de connexion de votre source et à déterminer les opérateurs et la langue pris en charge par votre source.

Pour récupérer la spécification de connexion d’une source donnée, envoyez une requête GET au point d’entrée `/connectionSpecs` de l’API [!DNL Flow Service] et indiquez le nom de la propriété de votre source dans vos paramètres de requête.

**Format d’API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pour le filtrage des résultats. Vous pouvez récupérer la spécification de connexion [!DNL Google BigQuery] en appliquant la propriété `name` et en spécifiant `"google-big-query"` dans votre recherche. |

+++Requête

La requête suivante récupère les spécifications de connexion pour [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Réponse

Une réponse réussie renvoie le code d’état 200 et les spécifications de connexion pour [!DNL Google BigQuery], y compris des informations sur son langage de requête pris en charge et ses opérateurs logiques.

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
| `attributes.filterAtSource.enabled` | Détermine si la source interrogée prend en charge le filtrage des données au niveau des lignes. |
| `attributes.filterAtSource.queryLanguage` | Détermine la langue de requête prise en charge par la source interrogée. |
| `attributes.filterAtSource.logicalOperators` | Détermine les opérateurs logiques que vous pouvez utiliser pour filtrer les données au niveau des lignes pour votre source. |
| `attributes.filterAtSource.comparisonOperators` | Détermine les opérateurs de comparaison que vous pouvez utiliser pour filtrer les données au niveau des lignes pour votre source. Pour plus d’informations sur les opérateurs de comparaison, consultez le tableau ci-dessous. |
| `attributes.filterAtSource.columnNameEscapeChar` | Détermine le caractère à utiliser pour les colonnes d&#39;échappement. |
| `attributes.filterAtSource.valueEscapeChar` | Détermine comment les valeurs seront entourées lors de l&#39;écriture d&#39;une requête SQL. |

{style="table-layout:auto"}

+++

#### Opérateurs de comparaison  {#comparison-operators}

| Opérateur | Description |
| --- | --- |
| `==` | Filtre en fonction de si la propriété est égale à la valeur fournie. |
| `!=` | Filtre en fonction de si la propriété n’est pas égale à la valeur fournie. |
| `<` | Filtre en fonction de si la valeur de la propriété est inférieure à la valeur fournie. |
| `>` | Filtre en fonction de si la propriété est supérieure à la valeur fournie. |
| `<=` | Filtre en fonction de si la propriété est inférieure ou égale à la valeur fournie. |
| `>=` | Filtre selon que la propriété est supérieure ou égale à la valeur fournie. |
| `like` | Filtre en étant utilisé dans une clause de `WHERE` pour rechercher un modèle spécifié. |
| `in` | Filtre selon si la propriété se trouve dans une plage spécifiée. |

{style="table-layout:auto"}

### Définition des conditions de filtrage pour l’ingestion {#specify-filtering-conditions-for-ingestion}

Une fois que vous avez identifié les opérateurs logiques et le langage de requête pris en charge par votre source, vous pouvez utiliser Profile Query Language (PQL) pour spécifier les conditions de filtrage à appliquer à vos données source.

Dans l’exemple ci-dessous, les conditions sont appliquées pour sélectionner uniquement les données égales aux valeurs fournies pour les types de nœuds répertoriés en tant que paramètres.

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

### Prévisualiser vos données {#preview-your-data}

Vous pouvez prévisualiser vos données en adressant une requête GET au point d’entrée `/explore` de l’API [!DNL Flow Service], tout en fournissant des `filters` dans le cadre de vos paramètres de requête et en spécifiant vos conditions d’entrée PQL dans [!DNL Base64].

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base de votre source. |
| `{TABLE_PATH}` | Propriété de chemin d&#39;accès de la table à inspecter. |
| `{FILTERS}` | Vos conditions de filtrage PQL codées en [!DNL Base64]. |

+++Requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Réponse

Une réponse réussie renvoie le contenu et la structure de vos données.

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

+++

### Créer une connexion source pour les données filtrées

Pour créer une connexion source et ingérer des données filtrées, envoyez une requête POST au point d’entrée `/sourceConnections` et indiquez vos conditions de filtrage dans les paramètres du corps de la requête.

**Format d’API**

```http
POST /sourceConnections
```

+++Requête

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

+++

+++Réponse

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source qui vient d’être créée.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## Filtrage des entités d’activité pour les [!DNL Marketo Engage] {#filter-for-marketo}

Vous pouvez utiliser le filtrage au niveau des lignes pour filtrer les entités d’activité lors de l’utilisation du [[!DNL Marketo Engage]  connecteur source ](../../connectors/adobe-applications/marketo/marketo.md). Actuellement, vous ne pouvez filtrer que les entités d’activité et les types d’activité standard. Les activités personnalisées restent régies sous [[!DNL Marketo] mappages de champs](../../connectors/adobe-applications/mapping/marketo.md).

### [!DNL Marketo] types d’activité standard {#marketo-standard-activity-types}

Le tableau suivant décrit les types d’activités standard pour [!DNL Marketo]. Utilisez ce tableau comme référence pour vos critères de filtrage.

| Identifiant du type d’activité | Nom du type d’activité |
| --- | --- |
| 1 | Page web de la visite |
| 2 | Remplir le formulaire |
| 3 | Clic sur le lien |
| 6 | Envoyer un courrier électronique |
| 7 | E-mail remis |
| 8 | E-mail non remis |
| 9 | E-mail de désabonnement |
| 10 | Ouvrir l’e-mail |
| 11 | Cliquez sur E-mail |
| 12 | Nouveau prospect |
| 21 | Convertir le prospect |
| 22 | Modifier le score |
| 24 | Ajouter à la liste |
| 25 | Supprimer de la liste |
| 27 | Non-remise temporaire de l’e-mail |
| 32 | Fusionner les prospects |
| 34 | Ajouter à l’opportunité |
| 35 | Supprimer de l’opportunité |
| 36 | Mettre à jour l’opportunité |
| 46 | Moment intéressant |
| 101 | Modifier l’étape Revenu |
| 104 | Modifier le statut en cours |
| 110 | Appeler le Webhook |
| 113 | Ajouter à la suite |
| 114 | Modifier le suivi de maturation |
| 115 | Modifier le rythme de maturation |

{style="table-layout:auto"}

Suivez les étapes ci-dessous pour filtrer vos entités d’activité standard lors de l’utilisation du connecteur source [!DNL Marketo].

### Créer un brouillon de flux de données

Créez tout d’abord un [[!DNL Marketo] flux de données](../ui/create/adobe-applications/marketo.md) et enregistrez-le en tant que brouillon. Consultez la documentation suivante pour obtenir des instructions détaillées sur la création d’un brouillon de flux de données :

* [Enregistrer un flux de données en tant que brouillon dans l’interface utilisateur](../ui/draft.md)
* [Enregistrer un flux de données en tant que brouillon à l’aide de l’API](../api/draft.md)

### Récupérer l’identifiant du flux de données

Une fois que vous disposez d’un brouillon de flux de données, vous devez récupérer son identifiant correspondant.

Dans l’interface utilisateur d’, accédez au catalogue de sources, puis sélectionnez **[!UICONTROL Flux de données]** dans l’en-tête supérieur. Utilisez la colonne Statut pour identifier tous les flux de données enregistrés en mode brouillon, puis sélectionnez le nom de votre flux de données. Ensuite, utilisez le panneau **[!UICONTROL Propriétés]** sur la droite pour localiser votre identifiant de flux de données.

### Récupérer les détails de votre flux de données

Ensuite, vous devez récupérer les détails de votre flux de données, en particulier l’identifiant de connexion source associé à votre flux de données. Pour récupérer les détails de votre flux de données, envoyez une requête GET au point d’entrée `/flows` et indiquez votre identifiant de flux de données comme paramètre de chemin d’accès.

**Format d’API**

```http
GET /flows/{FLOW_ID}
```

| Paramètre | Description |
| --- | --- |
| `{FLOW_ID}` | Identifiant du flux de données à récupérer. |

+++Requête

La requête suivante récupère des informations sur l’ID de flux de données : `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Réponse

Une réponse réussie renvoie les détails de votre flux de données, y compris les informations sur les connexions source et cible correspondantes. Vous devez prendre note de vos identifiants de connexion source et cible, car ces valeurs sont requises ultérieurement, afin de publier votre flux de données.

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### Récupérer les détails de votre connexion source

Ensuite, utilisez votre identifiant de connexion source et envoyez une requête GET au point d’entrée `/sourceConnections` pour récupérer les détails de votre connexion source.

**Format d’API**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | L’identifiant de la connexion source que vous souhaitez récupérer. |

+++Requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Réponse

Une réponse réussie renvoie les détails de votre connexion source. Prenez note de la version, car vous aurez besoin de cette valeur à l’étape suivante pour mettre à jour votre connexion source.

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### Mettre à jour votre connexion source avec des conditions de filtrage

Maintenant que vous disposez de votre identifiant de connexion source et de sa version correspondante, vous pouvez effectuer une requête PATCH avec les conditions de filtrage qui spécifient vos types d’activité standard.

Pour mettre à jour votre connexion source, envoyez une requête PATCH au point d’entrée `/sourceConnections` et indiquez votre identifiant de connexion source comme paramètre de requête. En outre, vous devez fournir un paramètre d’en-tête `If-Match`, avec la version correspondante de votre connexion source.

>[!TIP]
>
>L’en-tête `If-Match` est requis lors de l’exécution d’une requête PATCH. La valeur de cet en-tête est la version/etag unique du flux de données que vous souhaitez mettre à jour. La valeur de version/etag est mise à jour avec chaque mise à jour réussie d’un flux de données.

**Format d’API**

```http
PATCH /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | Identifiant de la connexion source à mettre à jour |

+++Requête

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++Réponse

Une réponse réussie renvoie votre identifiant de connexion source et votre etag (version).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### Publier votre connexion source

Maintenant que votre connexion source a été mise à jour avec vos conditions de filtrage, vous pouvez passer de l’état de brouillon à celui de publication de votre connexion source. Pour ce faire, envoyez une requête POST au point d’entrée `/sourceConnections` et indiquez l’identifiant de votre brouillon de connexion source ainsi qu’une opération d’action pour la publication.

**Format d’API**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | L’identifiant de la connexion source que vous souhaitez publier. |
| `op` | Opération d’action qui met à jour le statut de la connexion source interrogée. Pour publier un brouillon de connexion source, définissez `op` sur `publish`. |

+++Requête

La requête suivante publie un brouillon de connexion source.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Réponse

Une réponse réussie renvoie votre identifiant de connexion source et votre etag (version).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### Publier votre connexion cible

Comme à l’étape précédente, vous devez également publier votre connexion cible pour pouvoir continuer et publier votre brouillon de flux de données. Envoyez une requête POST au point d’entrée `/targetConnections` et indiquez l’identifiant du brouillon de connexion cible que vous souhaitez publier, ainsi qu’une opération d’action pour la publication.

**Format d’API**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | Identifiant de la connexion cible que vous souhaitez publier. |
| `op` | Opération d’action qui met à jour le statut de la connexion cible interrogée. Pour publier un brouillon de connexion cible, définissez `op` sur `publish`. |

+++Requête

La requête suivante publie la connexion cible avec l’ID : `7e53e6e8-b432-4134-bb29-21fc6e8532e5`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Réponse

Une réponse réussie renvoie l’identifiant et l’etag correspondant à votre connexion cible publiée.

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### Publier votre flux de données

Une fois vos connexions source et cible publiées, vous pouvez passer à l’étape finale et publier votre flux de données. Pour publier votre flux de données, envoyez une requête POST au point d’entrée `/flows` et indiquez votre identifiant de flux de données et une opération d’action pour la publication.

**Format d’API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `{FLOW_ID}` | L’identifiant du flux de données que vous souhaitez publier. |
| `op` | Opération d’action qui met à jour le statut du flux de données interrogé. Pour publier un brouillon de flux de données, définissez `op` sur `publish`. |

+++Requête

La requête suivante permet de publier le brouillon de flux de données.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Réponse

Une réponse réussie renvoie l’identifiant et l’`etag` correspondant du flux de données.

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

Vous pouvez utiliser l’interface utilisateur d’Experience Platform pour vérifier que votre brouillon de flux de données a été publié. Accédez à la page Flux de données dans le catalogue de sources et référencez le **[!UICONTROL Statut]** de votre flux de données. En cas de réussite, le statut doit maintenant être défini sur **Activé**.

>[!TIP]
>
>* Un flux de données avec le filtrage activé ne sera renvoyé qu’une seule fois. Toute modification apportée aux critères de filtrage (qu’il s’agisse d’un ajout ou d’une suppression) ne peut prendre effet que pour les données incrémentielles.
>* Si vous devez ingérer des données historiques pour un ou plusieurs nouveaux types d’activité, il est recommandé de créer un nouveau flux de données et de définir les critères de filtrage avec les types d’activité appropriés dans la condition de filtrage.
>* Vous ne pouvez pas filtrer les types d’activité personnalisés.
>* Vous ne pouvez pas prévisualiser les données filtrées.

## Annexe

Cette section fournit d’autres exemples de payloads différents pour le filtrage.

### Conditions singulières

Vous pouvez omettre la `fnApply` initiale pour les scénarios qui ne nécessitent qu’une seule condition.

+++Sélectionner pour afficher l’exemple

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

+++

### Utilisation de l’opérateur `in`

Consultez l’exemple de payload ci-dessous pour obtenir un exemple du `in` de l’opérateur.

+++Sélectionner pour afficher l’exemple

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

+++

### Utilisation de l’opérateur `isNull`

+++Sélectionner pour afficher l’exemple

Consultez l’exemple de payload ci-dessous pour obtenir un exemple du `isNull` de l’opérateur.

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

+++

### Utilisation de l’opérateur `NOT`

Consultez l’exemple de payload ci-dessous pour obtenir un exemple du `NOT` de l’opérateur.


+++Sélectionner pour afficher l’exemple

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

+++

### Exemple avec des conditions imbriquées

Consultez l’exemple de payload ci-dessous pour obtenir un exemple de conditions imbriquées complexes.

+++Sélectionner pour afficher l’exemple

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

+++