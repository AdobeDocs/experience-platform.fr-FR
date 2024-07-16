---
title: Mise à jour des spécifications de flux pour le SDK de diffusion en continu à l’aide de l’API Flow Service
description: Le document suivant décrit les étapes à suivre pour récupérer et mettre à jour les spécifications de flux à l’aide de l’API Flow Service pour les sources en libre-service (SDK de diffusion en continu).
exl-id: cc9dab7a-08fa-4c6c-bbac-cb658a6376fb
badge: Version bêta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 13%

---

# Mise à jour des spécifications de flux à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>Le SDK de diffusion en continu des sources en libre-service est en version bêta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Une fois que vous avez généré un nouvel identifiant de spécification de connexion, vous devez ajouter cet identifiant à une spécification de flux afin de créer un flux de données.

Les spécifications de flux contiennent des informations qui définissent un flux, notamment les identifiants de connexion source et cible pris en charge, les spécifications de transformation nécessaires à l’application aux données et les paramètres de planification requis pour générer un flux. Vous pouvez modifier les spécifications de flux à l’aide du point d’entrée `/flowSpecs`.

Le document suivant décrit les étapes à suivre pour récupérer et mettre à jour les spécifications de flux à l’aide de l’API [!DNL Flow Service] pour les sources en libre-service (SDK de diffusion en continu).

## Prise en main

Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Recherche d’une spécification de flux {#lookup}

Les sources créées avec le modèle `generic-streaming` utilisent toutes la spécification de flux `GenericStreamingAEP`. Cette spécification de flux peut être récupérée en envoyant une requête GET au point de terminaison `/flowSpecs/` et en fournissant la `flowSpec.id` de `e77fde5a-22a8-11ed-861d-0242ac120002`.

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

Vous pouvez mettre à jour les champs d’une spécification de flux via une opération de PUT. Lors de la mise à jour d’une spécification de flux via une requête de PUT, le corps doit inclure tous les champs requis lors de la création d’une spécification de flux dans une requête de POST.

>[!IMPORTANT]
>
>Lorsque vous créez une spécification de connexion pour une nouvelle source, vous devez ajouter son identifiant de spécification au tableau `sourceConnectionSpecIds` des spécifications de flux qui correspondent à votre source. Cela garantit que votre nouvelle source est prise en charge par une spécification de flux existante, ce qui vous permet d’effectuer le processus de création de flux de données avec votre nouvelle source.

**Format d’API**

```http
PUT /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**Requête**

La requête suivante met à jour la spécification de flux de `e77fde5a-22a8-11ed-861d-0242ac120002` pour inclure l’ID de spécification de connexion `bdb5b792-451b-42de-acf8-15f3195821de`.

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

Une réponse réussie renvoie les détails de la spécification de flux interrogée, y compris sa liste mise à jour de `sourceConnectionSpecIds`.

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

Une fois la nouvelle spécification de connexion ajoutée à la spécification de flux appropriée, vous pouvez passer au test et envoyer votre nouvelle source. Pour plus d’informations, consultez le guide sur le [test et l’envoi d’une nouvelle source](./submit.md) .
