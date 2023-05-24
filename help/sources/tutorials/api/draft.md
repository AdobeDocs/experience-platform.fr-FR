---
title: Création De Brouillons De L’API Entités De Votre Service De Flux
description: Découvrez comment créer des brouillons de votre connexion de base, de votre connexion source, de votre connexion cible et de votre flux de données à l’aide de l’API Flow Service
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: ebd650355a5a4c2a949739384bfd5c8df9577075
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 23%

---

# Créez des brouillons de votre [!DNL Flow Service] entités utilisant l’API

Vous pouvez utiliser la variable `mode=draft` paramètre de requête dans la variable [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) pour définir votre [!DNL Flow Service] entités telles que vos connexions de base, vos connexions source, vos connexions cible et vos flux de données vers un état de brouillon.

Les versions préliminaires peuvent être mises à jour ultérieurement avec de nouvelles informations, puis publiées une fois qu’elles sont prêtes, à l’aide de la variable `op=publish` paramètre de requête.

Ce tutoriel décrit les étapes à suivre pour définir votre [!DNL Flow Service] les entités à un état de brouillon et vous permettent de suspendre et d’enregistrer vos workflows pour qu’ils soient terminés ultérieurement.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

### Vérification de la prise en charge du mode préliminaire

Vous devez également vérifier si l’identifiant de spécification de connexion et l’identifiant de spécification de flux correspondant de la source que vous utilisez sont activés pour le mode préliminaire.

>[!BEGINTABS]

>[!TAB Recherche des détails de spécification de connexion]

+++Request La requête suivante récupère les informations de spécification de connexion pour [!DNL Azure File Storage]:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be5ec48c-5b78-49d5-b8fa-7c89ec4569b8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Réponse

Une réponse réussie renvoie les informations de spécification de connexion pour votre source. Pour vérifier si le mode préliminaire est pris en charge pour votre source, vérifiez que la variable `items[0].attributes.isDraftModeSupported` a une valeur de `true`.

```json {line-numbers="true" start-line="1" highlight="252"}
{
    "items": [
        {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "name": "azure-file-storage",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "basicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specifies the Azure File Storage endpoint."
                            },
                            "userid": {
                                "type": "string",
                                "description": "Specify the user to access the Azure File Storage."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the storage access key",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userid",
                            "password"
                        ]
                    }
                }
            ],
            "sourceSpec": {
                "name": "CloudStorage",
                "type": "CloudStorage",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "type": "string",
                            "description": "input path for copying files, can be a folder path, file path or a wildcard pattern"
                        },
                        "recursive": {
                            "type": "boolean",
                            "description": "indicates recursive copy in case of folder or wild card path, default is false"
                        }
                    },
                    "required": [
                        "path"
                    ]
                },
                "attributes": {
                    "uiAttributes": {
                        "documentationLink": "http://www.adobe.com/go/sources-azure-file-storage-en",
                        "isSource": true,
                        "category": {
                            "key": "cloudStorage"
                        },
                        "icon": {
                            "key": "azureFileStorage"
                        },
                        "description": {
                            "key": "azureFileStorageDescription"
                        },
                        "label": {
                            "key": "azureFileStorageLabel"
                        }
                    }
                }
            },
            "exploreSpec": {
                "name": "FileSystem",
                "type": "FileSystem",
                "requestSpec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines explorable objects",
                    "properties": {
                        "objectType": {
                            "type": "string",
                            "enum": [
                                "file",
                                "folder",
                                "root"
                            ]
                        }
                    },
                    "allOf": [
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "file"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string",
                                        "description": "defines file to get schema or preview of."
                                    },
                                    "fileType": {
                                        "type": "string",
                                        "enum": [
                                            "delimited"
                                        ]
                                    },
                                    "preview": {
                                        "type": "boolean"
                                    }
                                },
                                "required": [
                                    "object",
                                    "fileType"
                                ]
                            }
                        },
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "folder"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "object"
                                ]
                            }
                        }
                    ]
                },
                "responseSpec": {
                    "root": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "description": "lists tables/items under the database/container requested.",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "defines type of an item."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "defines display name of an item."
                                },
                                "path": {
                                    "type": "string",
                                    "description": "defines path of an item."
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether an item is previewable or not."
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether schema can be fetched for an item or not."
                                }
                            }
                        }
                    },
                    "folder": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string"
                                },
                                "name": {
                                    "type": "string"
                                },
                                "path": {
                                    "type": "string"
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false
                                }
                            }
                        }
                    },
                    "file": {
                        "delimited": {
                            "$schema": "http://json-schema.org/draft-07/schema#",
                            "type": "object",
                            "properties": {
                                "format": {
                                    "type": "string"
                                },
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "columns": {
                                            "type": "array",
                                            "items": {
                                                "type": "object",
                                                "properties": {
                                                    "name": {
                                                        "type": "string"
                                                    },
                                                    "type": {
                                                        "type": "string"
                                                    }
                                                }
                                            }
                                        }
                                    }
                                },
                                "data": {
                                    "type": "array",
                                    "items": {
                                        "type": "object"
                                    }
                                }
                            }
                        }
                    }
                }
            },
            "attributes": {
                "category": "Cloud Storage",
                "connectorName": "Azure File Storage",
                "isSource": true,
                "isDraftModeSupported": true,
                "uiAttributes": {
                    "apiFeatures": {
                        "explorePaginationSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

>[!TAB Recherche des détails sur les spécifications de flux]

+++Requête La requête suivante récupère les détails de spécification de flux pour une source de stockage dans le cloud :

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Réponse

Une réponse réussie renvoie les informations de spécification de flux pour votre source. Pour vérifier si le mode préliminaire est pris en charge pour votre source, vérifiez que la variable `items[0].attributes.isDraftModeSupported` a une valeur de `true`.

```json {line-numbers="true" start-line="1" highlight="167"}
{
  "items": [
    {
      "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
      "name": "CloudStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "sourceConnectionSpecIds": [
        "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "ecadc60c-7455-4d87-84dc-2a0e293d997b",
        "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
        "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
        "32e8f412-cdf7-464c-9885-78184cb113fd",
        "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
        "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
        "54e221aa-d342-4707-bcff-7a4bceef0001",
        "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
        "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
      ],
      "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "optionSpec": {
        "name": "OptionSpec",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "errorDiagnosticsEnabled": {
              "title": "Error diagnostics.",
              "description": "Flag to enable detailed and sample error diagnostics summary.",
              "type": "boolean",
              "default": false
            },
            "partialIngestionPercent": {
              "title": "Partial ingestion threshold.",
              "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
              "type": "number",
              "exclusiveMinimum": 0
            }
          }
        }
      },
      "transformationSpecs": [
        {
          "name": "Mapping",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for different mapping from source to target",
            "properties": {
              "mappingId": {
                "type": "string"
              },
              "mappingVersion": {
                "type": "string"
              }
            }
          }
        },
        {
          "name": "Encryption",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for encrypted data ingestion",
            "properties": {
              "publicKeyId": {
                "type": "string",
                "description": "publicKeyId returned in encryptionKey creation API. One must use the publicKeyId corresponding to the same publicKey they used for encrypting the files"
              }
            }
          }
        }
      ],
      "scheduleSpec": {
        "name": "PeriodicSchedule",
        "type": "Periodic",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "startTime": {
              "description": "epoch time",
              "type": "integer"
            },
            "frequency": {
              "type": "string",
              "enum": [
                "once",
                "minute",
                "hour",
                "day",
                "week"
              ]
            },
            "interval": {
              "type": "integer"
            },
            "backfill": {
              "type": "boolean",
              "default": true
            }
          },
          "required": [
            "startTime",
            "frequency"
          ],
          "if": {
            "properties": {
              "frequency": {
                "const": "once"
              }
            }
          },
          "then": {
            "allOf": [
              {
                "not": {
                  "required": [
                    "interval"
                  ]
                }
              },
              {
                "not": {
                  "required": [
                    "backfill"
                  ]
                }
              }
            ]
          },
          "else": {
            "required": [
              "interval"
            ],
            "if": {
              "properties": {
                "frequency": {
                  "const": "minute"
                }
              }
            },
            "then": {
              "properties": {
                "interval": {
                  "minimum": 15
                }
              }
            },
            "else": {
              "properties": {
                "interval": {
                  "minimum": 1
                }
              }
            }
          }
        }
      },
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "isDraftModeSupported": true,
        "frequency": "batch",
        "notification": {
          "category": "sources",
          "flowRun": {
            "enabled": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "read"
            ]
          }
        ]
      }
    }
  ]
}
```

+++

>[!ENDTABS]



## Création d’une connexion de base de brouillon {#create-a-draft-base-connection}

Pour créer une connexion de base de brouillon, envoyez une requête de POST à la fonction `/connections` point d’entrée du [!DNL Flow Service] API et fournir `mode=draft` comme paramètre de requête.

**Format d’API**

```http
POST /connections?mode=draft
```

| Paramètre | Description |
| --- | --- |
| `mode` | Paramètre de requête fourni par l’utilisateur qui décide de l’état de la connexion de base. Pour définir une connexion de base en tant que brouillon, définissez `mode` to `draft`. |

**Requête**

La requête suivante crée une connexion de base de brouillon pour le [!DNL Azure File Storage] source :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "ACME Azure File Storage Base Connection",
        "description": "Azure File Storage base connection for ACME data (DRAFT)",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
      }'
```

**Réponse**

Une réponse réussie renvoie l’identifiant de connexion de base et l’etag correspondant à votre connexion de base de brouillon. Vous pouvez utiliser cet identifiant ultérieurement pour mettre à jour et publier votre connexion de base.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Publier votre connexion de base de brouillon {#publish-your-draft-base-connection}

Une fois que votre brouillon est prêt à être publié, envoyez une requête de POST au `/connections` endpoint et indiquez l’identifiant de la connexion de base de brouillon que vous souhaitez publier, ainsi qu’une opération d’action pour la publication.

**Format d’API**

```http
POST /connections/{BASE_CONNECTION_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `op` | Opération d’action qui met à jour l’état de la connexion de base interrogée. Pour publier un brouillon de connexion de base, définissez `op` to `publish`. |

**Requête**

La requête suivante publie le brouillon de la connexion de base pour [!DNL Azure File Storage] qui a été créé à une étape précédente.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f9377f50-607a-4818-b77f-50607a181860/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie l’identifiant et l’etag correspondant à votre connexion de base publiée.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Création d’une connexion source de brouillon {#create-a-draft-source-connection}

Pour créer un brouillon de connexion source, envoyez une requête de POST à la fonction `/sourceConnections` point d’entrée du [!DNL Flow Service] API et fournir `mode=draft` comme paramètre de requête.

**Format d’API**

```http
POST /sourceConnections?mode=draft
```

| Paramètre | Description |
| --- | --- |
| `mode` | Paramètre de requête fourni par l’utilisateur qui décide de l’état de la connexion source. Pour définir une connexion source en tant que brouillon, définissez `mode` to `draft`. |

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Source Connection",
      "description: "Azure File Storage source connection for ACME data (DRAFT)",
      "baseConnectionId": "f9377f50-607a-4818-b77f-50607a181860",
      "data": {
          "format": "delimited",
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
          "version": "1.0"
      }
  }'
```

**Réponse**

Une réponse réussie renvoie l’identifiant de connexion source et l’etag correspondant à votre connexion source de brouillon. Vous pouvez utiliser cet identifiant ultérieurement pour mettre à jour et publier votre connexion source.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Publier la connexion source du brouillon {#publish-your-draft-source-connection}

>[!NOTE]
>
>Vous ne pouvez pas publier une connexion source si sa connexion de base associée est toujours en état de brouillon. Assurez-vous que votre connexion de base est publiée en premier avant de publier votre connexion source.

Une fois que votre brouillon est prêt à être publié, envoyez une requête de POST au `/sourceConnections` endpoint et indiquez l’identifiant de la connexion source du brouillon que vous souhaitez publier, ainsi qu’une opération d’action pour la publication.

**Format d’API**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `op` | Opération d’action qui met à jour l’état de la connexion source interrogée. Pour publier un brouillon de connexion source, définissez `op` to `publish`. |

**Requête**

La requête suivante publie le brouillon de la connexion source pour [!DNL Azure File Storage] qui a été créé à une étape précédente.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/26b53912-1005-49f0-b539-12100559f0e2/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie l’identifiant et l’etag correspondant à votre connexion source publiée.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Création d’une connexion cible de brouillon {#create-a-draft-target-connection}

Pour créer une connexion cible de brouillon, envoyez une requête de POST à la fonction `/targetConnections` point d’entrée du [!DNL Flow Service] API et fournir `mode=draft` comme paramètre de requête.

**Format d’API**

```http
POST /targetConnections?mode=draft
```

| Paramètre | Description |
| --- | --- |
| `mode` | Paramètre de requête fourni par l’utilisateur qui décide de l’état de la connexion cible. Pour définir une connexion cible en tant que brouillon, définissez `mode` to `draft`. |

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Target Connection",
      "description": "Azure File Storage target connection ACME data (DRAFT)",
      "data": {
          "schema": {
              "id": "{SCHEMA_ID}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{DATASET_ID}"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Réponse**

Une réponse réussie renvoie l’identifiant de connexion cible et l’etag correspondant à votre connexion cible de brouillon. Vous pouvez utiliser cet identifiant ultérieurement pour mettre à jour et publier votre connexion cible.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Publier votre connexion cible de brouillon {#publish-your-draft-target-connection}

>[!NOTE]
>
>Vous ne pouvez pas publier une connexion cible si sa connexion de base associée est toujours en état de création. Assurez-vous que votre connexion de base est publiée en premier avant de publier votre connexion cible.

Une fois que votre brouillon est prêt à être publié, envoyez une requête de POST au `/targetConnections` point de terminaison et indiquez l’identifiant de la connexion cible de brouillon que vous souhaitez publier, ainsi qu’une opération d’action pour la publication.

**Format d’API**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `op` | Opération d’action qui met à jour l’état de la connexion cible interrogée. Pour publier un brouillon de connexion cible, définissez `op` to `publish`. |

**Requête**

La requête suivante publie le brouillon de la connexion cible pour [!DNL Azure File Storage] qui a été créé à une étape précédente.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dbc5c132-bc2a-4625-85c1-32bc2a262558/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie l’identifiant et l’etag correspondant à votre connexion cible publiée.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Création d’un flux de données de brouillon {#create-a-draft-dataflow}

Pour définir un flux de données en tant que brouillon, envoyez une requête POST au point d’entrée `/flows` et indiquez le paramètre de requête `mode=draft`. Vous pouvez ainsi créer un flux de données et l’enregistrer en tant que brouillon.

**Format d’API**

```http
POST /flows?mode=draft
```

| Paramètre | Description |
| --- | --- |
| `mode` | Paramètre de requête fourni par l’utilisateur ou l’utilisatrice qui décide du statut du flux de données. Pour définir un flux de données en tant que brouillon, définissez `mode` sur `draft`. |

**Requête**

La requête suivante permet de créer un brouillon de flux de données.

```shell
  'https://platform.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "ACME Azure File Storage Dataflow",
    "description": "Azure File Storage dataflow for ACME data (DRAFT)",
    "sourceConnectionIds": [
        "26b53912-1005-49f0-b539-12100559f0e2"
    ],
    "targetConnectionIds": [
        "dbc5c132-bc2a-4625-85c1-32bc2a262558"
    ],
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    }
  }'
```

**Réponse**

Une réponse réussie renvoie l’identifiant de flux et l’etag correspondant à votre flux de données de brouillon. Vous pouvez utiliser cet identifiant ultérieurement pour mettre à jour et publier votre flux de données.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Publication du flux de données de brouillon {#publish-your-draft-dataflow}

>[!NOTE]
>
>Vous ne pouvez pas publier un flux de données si ses connexions source et cible associées sont toujours à l’état de brouillon. Assurez-vous que vos connexions source et cible sont publiées en premier avant de publier votre flux de données.

Une fois que votre brouillon est prêt à être publié, envoyez une requête POST au point d’entrée `/flows` et indiquez l’identifiant du brouillon de flux de données que vous souhaitez publier, ainsi qu’une opération d’action pour la publication.

**Format d’API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Paramètre | Description |
| --- | --- |
| `op` | Opération d’action qui met à jour le statut du flux de données interrogé. Pour publier un brouillon de flux de données, définissez `op` sur `publish`. |

**Requête**

La requête suivante permet de publier le brouillon de flux de données.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie l’identifiant et l’`etag` correspondant du flux de données.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez appris à créer des brouillons de votre [!DNL Flow Service] entités et publiez ces brouillons. Pour plus d’informations sur les sources, veuillez lire le [présentation des sources](../../home.md).