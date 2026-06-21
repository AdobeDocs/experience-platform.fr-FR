---
title: Mettre à jour les spécifications de flux pour Streaming SDK à l’aide de l’API Flow Service
description: Le document suivant décrit la procédure à suivre pour récupérer et mettre à jour des spécifications de flux à l’aide de l’API Flow Service pour les sources en libre-service (Streaming SDK).
exl-id: cc9dab7a-08fa-4c6c-bbac-cb658a6376fb
badge: Beta
TQID: https://experienceleague.adobe.com/ls6GnhzgPZ2ntR-WOI-mLZrRXfig7VOQMuzKkVohfto
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 427
ht-degree: 13%

---

# Mettre à jour les spécifications de flux à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>La diffusion en continu de SDK par les sources en libre-service est en version bêta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Une fois que vous avez généré un nouvel identifiant de spécification de connexion, vous devez l’ajouter à une spécification de flux afin de créer un flux de données.

Les spécifications de flux contiennent des informations qui définissent un flux, y compris les identifiants de connexion source et cible pris en charge, les spécifications de transformation qui doivent être appliquées aux données et les paramètres de planification requis pour générer un flux. Vous pouvez modifier les spécifications de flux à l’aide du point d’entrée `/flowSpecs`.

Le document suivant décrit les étapes à suivre pour récupérer et mettre à jour les spécifications de flux à l’aide de l’API [!DNL Flow Service] pour les sources en libre-service (Streaming SDK).

## Prise en main

Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Recherche d’une spécification de flux {#lookup}

Les sources créées avec le modèle de `generic-streaming` utilisent toutes la spécification de flux `GenericStreamingAEP`. Cette spécification de flux peut être récupérée en adressant une requête GET au point d’entrée `/flowSpecs/` et en fournissant le `flowSpec.id` de `e77fde5a-22a8-11ed-861d-0242ac120002`.

**Format d’API**

```http
GET /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**Requête**

La requête suivante récupère la spécification de flux `e77fde5a-22a8-11ed-861d-0242ac120002`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

Une réponse réussie renvoie les détails de la spécification de flux interrogée.

```json
{
  "items": [
    {
      "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
      "name": "GenericStreamingAEP",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "sourceConnectionSpecIds": [
        "e77fd9d2-22a8-11ed-861d-0242ac120002"
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
            },
            "inletUrl": {
              "title": "Inlet Url.",
              "description": "Inlet Url which defines the streaming endpoint.",
              "type": "string"
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
        }
      ],
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "frequency": "streaming",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": true,
            "flowRunsSupported": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
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

## Mettre à jour une spécification de flux {#update}

Vous pouvez mettre à jour les champs d’une spécification de flux par le biais d’une opération PUT. Lors de la mise à jour d’une spécification de flux par le biais d’une requête PUT, le corps doit inclure tous les champs qui seraient requis lors de la création d’une spécification de flux dans une requête POST.

>[!IMPORTANT]
>
>Lorsque vous créez une spécification de connexion pour une nouvelle source, vous devez ajouter son identifiant de spécification au tableau `sourceConnectionSpecIds` des spécifications de flux qui correspondent à votre source. Cela garantit que votre nouvelle source est prise en charge par une spécification de flux existante, ce qui vous permet d’effectuer le processus de création de flux de données avec votre nouvelle source.

**Format d’API**

```http
PUT /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**Requête**

La requête suivante met à jour la spécification de flux de `e77fde5a-22a8-11ed-861d-0242ac120002` pour inclure l’identifiant de spécification de connexion `bdb5b792-451b-42de-acf8-15f3195821de`.

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/e77fde5a-22a8-11ed-861d-0242ac120002' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
      "name": "GenericStreamingAEP",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "sourceConnectionSpecIds": [
          "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "bdb5b792-451b-42de-acf8-15f3195821de"
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
                  },
                  "inletUrl": {
                      "title": "Inlet Url.",
                      "description": "Inlet Url which defines the streaming endpoint.",
                      "type": "string"
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
          }
      ],
      "attributes": {
          "isSourceFlow": true,
          "flacValidationSupported": true,
          "frequency": "streaming",
          "uiAttributes": {
              "apiFeatures": {
                  "updateSupported": true,
                  "flowRunsSupported": true
              }
          }
      },
      "permissionsInfo": {
          "view": [
              {
                  "@type": "lowLevel",
                  "name": "StreamingSource",
                  "permissions": [
                      "read"
                  ]
              }
          ],
          "manage": [
              {
                  "@type": "lowLevel",
                  "name": "StreamingSource",
                  "permissions": [
                      "write"
                  ]
              }
          ]
      }
  }'
```

**Réponse**

Une réponse réussie renvoie les détails de la spécification de flux interrogée, y compris sa liste de `sourceConnectionSpecIds` mise à jour.

```json
{
    "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "GenericStreamingAEP",
    "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
    "version": "1.0",
      "sourceConnectionSpecIds": [
        "e77fd9d2-22a8-11ed-861d-0242ac120002"
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
            },
            "inletUrl": {
              "title": "Inlet Url.",
              "description": "Inlet Url which defines the streaming endpoint.",
              "type": "string"
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
        }
      ],
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "frequency": "streaming",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": true,
            "flowRunsSupported": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
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

## Étapes suivantes

Maintenant que votre nouvelle spécification de connexion a été ajoutée à la spécification de flux appropriée, vous pouvez procéder au test et à l’envoi de votre nouvelle source. Pour plus d’informations, consultez le guide sur le [test et envoi d’une nouvelle source](./submit.md).
