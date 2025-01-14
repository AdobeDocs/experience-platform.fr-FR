---
keywords: Experience Platform;accueil;rubriques populaires;OneTrust
solution: Experience Platform
title: Créer un flux de données pour une source d’intégration OneTrust à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à l’intégration OneTrust à l’aide de l’API Flow Service.
exl-id: e224efe0-4756-4b8a-b446-a3e1066f2050
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1913'
ht-degree: 61%

---

# Créer un flux de données pour une source de [!DNL OneTrust Integration] à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>La source [!DNL OneTrust Integration] prend uniquement en charge l’ingestion des données de consentement et de préférences, et non des cookies.

Le tutoriel suivant vous guide tout au long des étapes de création d’une connexion source et d’un flux de données pour importer à la fois les données de consentement historiques et planifiées d’[[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) vers Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Conditions préalables

>[!IMPORTANT]
>
>Le connecteur source [!DNL OneTrust Integration] et la documentation ont été créés par l’équipe [!DNL OneTrust Integration]. Pour toute demande ou information, contactez directement l&#39;[[!DNL OneTrust] équipe](https://my.onetrust.com/s/contactsupport?language=en_US).

Avant de pouvoir connecter [!DNL OneTrust Integration] à Platform, vous devez d’abord récupérer votre jeton d’accès. Pour obtenir des instructions détaillées sur la recherche de votre jeton d’accès, consultez le guide [[!DNL OneTrust Integration] OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Le jeton d’accès ne s’actualise pas automatiquement après son expiration, car les jetons d’actualisation système à système ne sont pas pris en charge par [!DNL OneTrust]. Par conséquent, il est nécessaire de s’assurer que votre jeton d’accès est mis à jour dans la connexion avant son expiration. La durée de vie configurable maximale d’un jeton d’accès est d’un an. Pour en savoir plus sur la mise à jour de votre jeton d’accès, consultez le document [[!DNL OneTrust]  sur la gestion des informations d’identification de votre client OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

## Connecter [!DNL OneTrust Integration] à Platform à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>Les spécifications de l’API [!DNL OneTrust Integration] sont partagées avec Adobe pour l’ingestion de données.

Le tutoriel suivant vous guide tout au long des étapes nécessaires à la création d’une connexion source [!DNL OneTrust Integration] et d’un flux de données pour importer des données [!DNL OneTrust Integration] dans Platform à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Créer une connexion de base {#base-connection}

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL OneTrust Integration] dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST base connection",
      "description": "ONETRUST base connection to authenticate to Platform",
      "connectionSpec": {
          "id": "cf16d886-c627-4872-9936-fb08d6cba8cc",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion de base. Assurez-vous que le nom de votre connexion de base est explicite, car vous pouvez lʼutiliser pour rechercher des informations sur votre connexion de base. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `connectionSpec.id` | Identifiant de spécification de connexion de votre source. Cet identifiant peut être récupéré une fois que votre source est enregistrée et approuvée par le biais de l’API [!DNL Flow Service]. |
| `auth.specName` | Type d’authentification que vous utilisez pour authentifier votre source sur Platform. |
| `auth.params.` | Contient les informations d’identification requises pour authentifier votre source, y compris le jeton d’accès pour se connecter à l’API. |
| `auth.params.accessToken` | Jeton d’accès correspondant à votre compte [!DNL OneTrust Integration]. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de base, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer la structure de fichiers et le contenu de votre source à l’étape suivante.

```json
{
     "id": "622124ca-6d18-47f7-999c-66f599955309",
     "etag": "\"2e026443-0000-0200-0000-621f1af80000\""
}
```

### Explorer votre source {#explore}

À l’aide de l’identifiant de connexion de base généré à l’étape précédente, vous pouvez explorer les fichiers et répertoires en exécutant des requêtes GET.

Utilisez les appels suivants pour trouver le chemin d’accès au fichier que vous souhaitez importer en [!DNL Platform] :

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

Lors de l’exécution de requêtes GET pour explorer la structure et le contenu des fichiers de votre source, vous devez inclure les paramètres de requête répertoriés dans le tableau ci-dessous :


| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base généré à l’étape précédente. |
| `objectType=rest` | Type d’objet que vous souhaitez explorer. Actuellement, cette valeur est toujours définie sur `rest`. |
| `{OBJECT}` | Ce paramètre est requis uniquement lors de l’affichage d’un répertoire spécifique. Sa valeur représente le chemin dʼaccès au répertoire que vous souhaitez explorer. |
| `fileType=json` | Type de fichier du fichier que vous souhaitez importer dans Platform. Actuellement, `json` est le seul type de fichier pris en charge. |
| `{PREVIEW}` | Valeur booléenne qui définit si le contenu de la connexion prend en charge la prévisualisation. |

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/622124ca-6d18-47f7-999c-66f599955309/explore?objectType=rest&object=json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure du fichier interrogé.

>[!NOTE]
>
>La payload de réponse JSON ci-dessous est masquée par souci de concision. Sélectionnez Cliquer sur moi pour afficher la payload de réponse.

+++Cliquez sur moi

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "numberOfElements": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "last": {
                "type": "boolean"
            },
            "pageable": {
                "type": "object",
                "properties": {
                    "paged": {
                        "type": "boolean"
                    },
                    "pageNumber": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "offset": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "tokenId": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "limit": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "pageSize": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "unpaged": {
                        "type": "boolean"
                    },
                    "sort": {
                        "type": "object",
                        "properties": {
                            "unsorted": {
                                "type": "boolean"
                            },
                            "sorted": {
                                "type": "boolean"
                            },
                            "empty": {
                                "type": "boolean"
                            }
                        }
                    }
                }
            },
            "sort": {
                "type": "object",
                "properties": {
                    "unsorted": {
                        "type": "boolean"
                    },
                    "sorted": {
                        "type": "boolean"
                    },
                    "empty": {
                        "type": "boolean"
                    }
                }
            },
            "content": {
                "type": "object",
                "properties": {
                    "LastUpdatedDate": {
                        "type": "string"
                    },
                    "Identifier": {
                        "type": "string"
                    },
                    "Language": {
                        "type": "string"
                    },
                    "TestDataSubject": {
                        "type": "boolean"
                    },
                    "CreatedDate": {
                        "type": "string"
                    },
                    "DataElements": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "Id": {
                        "type": "string"
                    },
                    "Purposes": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "Status": {
                                    "type": "string"
                                },
                                "LastTransactionDate": {
                                    "type": "string"
                                },
                                "CustomPreferences": {
                                    "type": "array",
                                    "items": {
                                        "type": "object",
                                        "properties": {}
                                    }
                                },
                                "LastUpdatedDate": {},
                                "ExpiryDate": {},
                                "Topics": {
                                    "type": "array",
                                    "items": {
                                        "type": "object",
                                        "properties": {
                                            "IsConsented": {
                                                "type": "boolean"
                                            },
                                            "Id": {
                                                "type": "string"
                                            },
                                            "Name": {
                                                "type": "string"
                                            }
                                        }
                                    }
                                },
                                "TotalTransactionCount": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "LastReceiptId": {},
                                "ConsentDate": {
                                    "type": "string"
                                },
                                "LastInteractionDate": {},
                                "Name": {
                                    "type": "string"
                                },
                                "FirstTransactionDate": {
                                    "type": "string"
                                },
                                "LastTransactionCollectionPointId": {
                                    "type": "string"
                                },
                                "LastTransactionCollectionPointVersion": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "Version": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "attributes": {
                                    "type": "object",
                                    "properties": {}
                                },
                                "Id": {
                                    "type": "string"
                                },
                                "PurposeNote": {},
                                "WithdrawalDate": {
                                    "type": "string"
                                }
                            }
                        }
                    }
                }
            },
            "first": {
                "type": "boolean"
            },
            "empty": {
                "type": "boolean"
            }
        }
    },
    "data": [
        {
            "number": 0,
            "size": 100,
            "numberOfElements": 100,
            "last": false,
            "pageable": {
                "limit": 100,
                "offset": 0,
                "sort": {
                    "sorted": true,
                    "unsorted": false,
                    "empty": false
                },
                "tokenId": 100,
                "pageSize": 100,
                "pageNumber": 0,
                "unpaged": false,
                "paged": true
            },
            "sort": {
                "sorted": true,
                "unsorted": false,
                "empty": false
            },
            "content": {
                "Id": "de1ab4d2-6ccf-42bd-b363-2d8cac60c88c",
                "Language": "en-us",
                "Identifier": "gkumar@onetrust.com",
                "LastUpdatedDate": "2019-06-05T12:02:07Z",
                "CreatedDate": "2018-05-02T03:14:28Z",
                "Purposes": [
                    {
                        "Id": "9edf57bb-0449-4c15-98e4-8641522e5ff4",
                        "Name": "Purpose_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:14:27Z",
                        "LastTransactionDate": "2019-05-29T11:08:26Z",
                        "WithdrawalDate": "2019-05-29T11:05:30Z",
                        "ConsentDate": "2018-05-02T03:14:27Z",
                        "TotalTransactionCount": 5,
                        "Topics": [
                            {
                                "Id": "d6e3d675-3d6f-4f4e-a157-bd93829ee632",
                                "Name": "Topic_UAT",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "814c073a-95f1-4fc9-8263-1ec62225c5e9",
                        "Name": "Multi Pur_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:17:33Z",
                        "LastTransactionDate": "2018-05-02T03:19:49Z",
                        "ConsentDate": "2018-05-02T03:17:33Z",
                        "TotalTransactionCount": 4,
                        "LastTransactionCollectionPointId": "9a5b7375-bc13-47e8-8a58-1ca7d9c06c8e",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "4d52dcc4-82bf-44bf-ac49-854eba6ff8f3",
                        "Name": "Eloqua_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:26:36Z",
                        "LastTransactionDate": "2019-03-07T03:23:25Z",
                        "ConsentDate": "2018-05-02T03:26:36Z",
                        "TotalTransactionCount": 3,
                        "Topics": [
                            {
                                "Id": "690ad782-6280-4ea4-b62a-1514c39fc838",
                                "Name": "Eloqua_topic",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "f8886377-e4b1-45e4-b1c0-d7dacb744db8",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "723300e3-96cb-4da4-abdd-4913c05be215",
                        "Name": "Purpose 1",
                        "Version": 2,
                        "Status": "EXPIRED",
                        "FirstTransactionDate": "2019-02-27T06:29:48Z",
                        "LastTransactionDate": "2019-02-28T12:00:45Z",
                        "ConsentDate": "2019-02-27T06:29:48Z",
                        "ExpiryDate": "2019-02-28T12:00:45Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "3dbfb978-10f9-44a9-9669-d699674edd9d",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "4a5e6278-17f1-4283-beee-29f81cde2bd0",
                        "Name": "kbpurpose1",
                        "Version": 1,
                        "Status": "NO_CONSENT",
                        "FirstTransactionDate": "2019-03-07T03:21:58Z",
                        "LastTransactionDate": "2019-05-29T03:56:37Z",
                        "TotalTransactionCount": 6,
                        "LastTransactionCollectionPointId": "cea42a12-5de4-421a-b429-092e8d523948",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a36f98d0-c662-4f61-a2a1-8bdab69e3c3a",
                        "Name": "Pur 1",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-03-07T03:23:25Z",
                        "LastTransactionDate": "2019-03-07T03:23:27Z",
                        "ConsentDate": "2019-03-07T03:23:25Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "f8886377-e4b1-45e4-b1c0-d7dacb744db8",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "41ebdf32-068b-4239-89ac-42e20262c5a9",
                        "Name": "Send Notifications about Changes to Preferences",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-03-07T03:24:11Z",
                        "LastTransactionDate": "2019-03-07T03:27:29Z",
                        "ConsentDate": "2019-03-07T03:24:11Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "c29a99a9-de4d-4367-973b-95b0217d0640",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "759d8b24-e4c0-4107-86e2-3a408db13e6b",
                        "Name": "GJ Purpose 07",
                        "Version": 2,
                        "Status": "WITHDRAWN",
                        "FirstTransactionDate": "2019-03-07T03:27:29Z",
                        "LastTransactionDate": "2019-05-29T11:09:03Z",
                        "WithdrawalDate": "2019-05-29T11:09:03Z",
                        "ConsentDate": "2019-03-07T03:27:29Z",
                        "TotalTransactionCount": 18,
                        "LastTransactionCollectionPointId": "cea42a12-5de4-421a-b429-092e8d523948",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a57ee9da-b494-49e2-b562-6dfa31f190df",
                        "Name": "kbpurpose2",
                        "Version": 1,
                        "Status": "WITHDRAWN",
                        "FirstTransactionDate": "2019-03-28T03:23:44Z",
                        "LastTransactionDate": "2019-03-28T03:24:29Z",
                        "WithdrawalDate": "2019-03-28T03:24:29Z",
                        "ConsentDate": "2019-03-28T03:23:44Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "c29a99a9-de4d-4367-973b-95b0217d0640",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a1ccd810-94a0-4b58-946b-6705eae15c5b",
                        "Name": "Purpose01 v2",
                        "Version": 2,
                        "Status": "EXPIRED",
                        "FirstTransactionDate": "2019-05-29T04:05:42Z",
                        "LastTransactionDate": "2019-06-05T12:02:06Z",
                        "WithdrawalDate": "2019-05-29T11:09:12Z",
                        "ConsentDate": "2019-05-29T04:05:42Z",
                        "ExpiryDate": "2019-06-05T12:02:06Z",
                        "TotalTransactionCount": 8,
                        "Topics": [
                            {
                                "Id": "af7bf604-2058-4089-985c-c84083e3e3e3",
                                "Name": "New_Topic",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a313353a-e13b-4554-be08-22cf4a78a31c",
                        "Name": "Purpose_1804 v2",
                        "Version": 2,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-05-29T04:05:42Z",
                        "LastTransactionDate": "2019-05-29T11:09:30Z",
                        "WithdrawalDate": "2019-05-29T11:05:30Z",
                        "ConsentDate": "2019-05-29T04:05:42Z",
                        "TotalTransactionCount": 4,
                        "CustomPreferences": [
                            {
                                "Id": "4935d35a-7216-480d-9da9-1aef0e078b89",
                                "Name": "Custom_S",
                                "Options": [
                                    {
                                        "Id": "8acc2f9f-37f8-4ace-a513-fae6b7dd0aa9",
                                        "Name": "Option2",
                                        "IsConsented": true
                                    }
                                ]
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    }
                ],
                "TestDataSubject": false
            },
            "first": true,
            "empty": false
        }
    ]
}
```

+++

### Créer une connexion source {#source-connection}

Vous pouvez créer une connexion source en effectuant une requête POST à l’API [!DNL Flow Service]. Une connexion source se compose d’un identifiant de connexion, d’un chemin d’accès au fichier de données source et d’un identifiant de spécification de connexion.

**Format d’API**

```https
POST /sourceConnections
```

**Requête**

La requête suivante crée une connexion source pour [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST Source Connection",
      "description": "ONETRUST Source Connection",
      "baseConnectionId": "622124ca-6d18-47f7-999c-66f599955309",
      "connectionSpec": {
          "id": "cf16d886-c627-4872-9936-fb08d6cba8cc",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {}
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion source. |
| `baseConnectionId` | Identifiant de connexion de base de [!DNL OneTrust Integration]. Cet identifiant a été généré lors d’une étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion correspondant à votre source. |
| `data.format` | Format des données [!DNL OneTrust Integration] que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

```json
{
     "id": "eb5833d3-230d-4700-80cc-bda396e7af8a",
     "etag": "\"da04c07f-0000-0200-0000-621f1afc0000\""
}
```

### Créer un schéma XDM cible {#target-schema}

Pour que les données sources soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Le schéma cible est ensuite utilisé pour créer un jeu de données Platform contenant les données sources.

Un schéma XDM cible peut être créé en adressant une requête POST à l’[API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, suivez le tutoriel sur la [création d’un schéma à l’aide de l’API](../../../../../xdm/api/schemas.md).

### Créer un jeu de données cible {#target-dataset}

Un jeu de données cible peut être créé en adressant une requête POST à l’[API Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/) et en fournissant l’identifiant du schéma cible dans la payload.

Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, suivez le tutoriel sur la [création d’un jeu de données à l’aide de l’API](../../../../../catalog/api/create-dataset.md).

### Créer une connexion cible {#target-connection}

Une connexion cible représente la connexion à la destination où les données ingérées doivent être stockées. Pour créer une connexion cible, vous devez fournir l’identifiant de spécification de connexion fixe qui correspond au [!DNL Data Lake]. Cet identifiant est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez à présent des identifiants uniques d’un schéma et d’un jeu de données cibles et de l’identifiant de spécification de connexion au [!DNL Data Lake]. À lʼaide de ces identifiants, vous pouvez créer une connexion cible à l’aide de l’API [!DNL Flow Service] pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

```https
POST /targetConnections
```

**Requête**

La requête suivante crée une connexion cible pour [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST Target Connection",
      "description": "ONETRUST Target Connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "dataSetId": "61f6ca3f33978c19486bb463"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom de la connexion cible. Assurez-vous que le nom de votre connexion cible est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion cible. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion cible. |
| `connectionSpec.id` | Identifiant de spécification de connexion qui correspond à [!DNL Data Lake]. Cet ID fixe est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Format des données [!DNL OneTrust Integration] que vous souhaitez importer dans Platform. |
| `params.dataSetId` | Identifiant du jeu de données cible récupéré lors d’une étape précédente. |


**Réponse**

Une réponse réussie renvoie l’identifiant unique de la nouvelle connexion cible (`id`). Cet identifiant est requis aux étapes suivantes.

```json
{
     "id": "495f761f-310a-4a7b-ae78-5b1152d74b38",
     "etag": "\"410a7b0c-0000-0200-0000-621f1afd0000\""
}
```

### Créer un mappage {#mapping}

Pour que les données sources soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible se rattache. Pour ce faire, il suffit d’adresser une requête de POST à [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) avec des mappages de données définis dans la payload de la requête.

**Format d’API**

```http
POST /conversion/mappingSets
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/cfc8cee182e546c1fb35071185524b465e06bf1acb74f30d",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [{
              "sourceType": "ATTRIBUTE",
              "source": "content.Identifier",
              "destination": "_id",
              "name": "id",
              "description": "Identifier field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Identifier",
              "destination": "_exchangesandboxbravo.Identifier"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Language",
              "destination": "_exchangesandboxbravo.Language",
              "description": "Language field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.CreatedDate",
              "destination": "_exchangesandboxbravo.CreatedDate",
              "description": "Created Date field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.LastUpdatedDate",
              "destination": "_exchangesandboxbravo.LastUpdatedDate",
              "description": "Created Date field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.DataElements",
              "destination": "_exchangesandboxbravo.DataElements"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Purposes",
              "destination": "_exchangesandboxbravo.Purposes"
          }

      ]
  }'
```

| Propriété | Description |
| --- | --- |
| `xdmSchema` | Identifiant du [schéma XDM cible](#target-schema) généré lors d’une étape précédente. |
| `mappings.destinationXdmPath` | Chemin XDM de destination vers lequel l’attribut source est mappé. |
| `mappings.sourceAttribute` | Attribut source qui doit être mappé à un chemin XDM de destination. |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Cette valeur est requise lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "a87f130e82f04d5188da01f087805c4b",
    "version": 0,
    "createdDate": 1646205694395,
    "modifiedDate": 1646205694395,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Créer un flux {#flow}

La dernière étape pour importer des données de [!DNL OneTrust Integration] vers Platform consiste à créer un flux de données. Vous disposez à présent des valeurs requises suivantes :

* [ID de connexion source](#source-connection)
* [ID de connexion cible](#target-connection)
* [Identifiant de mappage](#mapping)

Un flux de données est chargé de planifier et de collecter les données provenant d’une source. Vous pouvez créer un flux de données en exécutant une requête POST et en fournissant les valeurs mentionnées précédemment dans la payload.

Pour planifier une ingestion, vous devez d’abord définir la valeur de l’heure de début en temps Unix en secondes. Vous devez ensuite définir la valeur de fréquence sur l’une des cinq options suivantes : `once`, `minute`, `hour`, `day` ou `week`. La valeur de l’intervalle désigne la période entre deux ingestions consécutives. Toutefois, il n’est pas nécessaire de définir un intervalle pour la création d’une ingestion unique. Pour toutes les autres fréquences, la valeur de l’intervalle doit être égale ou supérieure à `15`.

**Format d’API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST dataflow",
      "description": "ONETRUST dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "eb5833d3-230d-4700-80cc-bda396e7af8a"
      ],
      "targetConnectionIds": [
          "495f761f-310a-4a7b-ae78-5b1152d74b38"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "a87f130e82f04d5188da01f087805c4b",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du flux de données. Assurez-vous que le nom de votre flux de données est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre flux de données. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre flux de données. |
| `flowSpec.id` | Identifiant de spécification de flux requis pour créer un flux de données. Cet ID fixe est `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Version correspondante de l’identifiant de spécification de flux. Cette valeur est définie par défaut sur `1.0`. |
| `sourceConnectionIds` | L’[identifiant de connexion source](#source-connection) généré lors d’une étape précédente. |
| `targetConnectionIds` | [Identifiant de connexion cible](#target-connection) généré lors d’une étape précédente. |
| `transformations` | Cette propriété contient les différentes transformations qui doivent être appliquées à vos données. Cette propriété est requise lors de l’importation de données non conformes à XDM dans Platform. |
| `transformations.name` | Nom attribué à la transformation. |
| `transformations.params.mappingId` | [Identifiant de mappage](#mapping) généré lors d’une étape précédente. |
| `transformations.params.mappingVersion` | Version correspondante de l’identifiant de mappage. Ce paramètre est défini par défaut sur `0`. |
| `scheduleParams.startTime` | Cette propriété contient des informations sur la planification de l’ingestion du flux de données. |
| `scheduleParams.frequency` | Fréquence de collecte des données par le flux de données. Les valeurs possibles sont les suivantes : `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un nombre entier non nul. L’intervalle n’est pas requis lorsque la fréquence est définie sur `once` et doit être supérieur ou égal à `15` pour d’autres valeurs de fréquence. |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du flux de données nouvellement créé. Vous pouvez utiliser cet identifiant pour surveiller, mettre à jour ou supprimer votre flux de données.

```json
{
     "id": "70045189-42f0-493d-9b9e-be1045a9f4fa",
     "etag": "\"1601e900-0000-0200-0000-621f1b080000\""
}
```

## Annexe

La section suivante fournit des informations sur les étapes que vous pouvez suivre pour surveiller, mettre à jour et supprimer votre flux de données.

### Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les exécutions du flux, le statut d’achèvement et les erreurs. Pour obtenir des exemples d’API complets, consultez le guide sur la [surveillance des flux de données sources à l’aide de l’API](../../monitor.md).

### Mettre à jour votre flux de données

Mettez à jour les détails de votre flux de données, tels que son nom et sa description, ainsi que son planning d’exécution et les jeux de mappages associés en envoyant une requête de PATCH au point d’entrée `/flows` de [!DNL Flow Service]’API , tout en fournissant l’identifiant de votre flux de données. Lors de l’exécution d’une requête de PATCH, vous devez fournir le `etag` unique de votre flux de données dans l’en-tête `If-Match`. Pour obtenir des exemples d’API complets, consultez le guide sur la [mise à jour des flux de données sources à l’aide de l’API](../../update-dataflows.md).

### Mettre à jour votre compte

Mettez à jour le nom, la description et les informations d’identification de votre compte source en adressant une requête de PATCH à l’API [!DNL Flow Service] et en fournissant votre identifiant de connexion de base comme paramètre de requête. Lors de l’exécution d’une requête de PATCH, vous devez indiquer le `etag` unique de votre compte source dans l’en-tête `If-Match`. Pour obtenir des exemples d’API complets, consultez le guide sur la [mise à jour de votre compte source à l’aide de l’API](../../update.md).

### Supprimer le flux de données

Supprimez votre flux de données en adressant une requête de DELETE à l’API [!DNL Flow Service] et en fournissant l’identifiant du flux de données à supprimer dans le cadre du paramètre de requête. Pour obtenir des exemples d’API complets, consultez le guide sur la [suppression de vos flux de données à l’aide de l’API](../../delete-dataflows.md).

### Supprimer votre compte

Supprimez votre compte en adressant une requête de DELETE à l’API [!DNL Flow Service] et en fournissant l’identifiant de connexion de base du compte que vous souhaitez supprimer. Pour obtenir des exemples d’API complets, consultez le guide sur la [suppression de votre compte source à l’aide de l’API](../../delete.md).