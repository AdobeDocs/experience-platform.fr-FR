---
title: Création d’une spécification de connexion pour le SDK de diffusion en continu à l’aide de l’API Flow Service
description: Le document suivant décrit les étapes à suivre pour créer une spécification de connexion à l’aide de l’API Flow Service et intégrer une nouvelle source par le biais de sources en libre-service.
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Version bêta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 36%

---

# Créez une nouvelle spécification de connexion à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>Le SDK de diffusion en continu des sources en libre-service est en version bêta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Une spécification de connexion représente la structure d’une source. Elle contient des informations sur les exigences d’authentification d’une source, définit la manière dont les données sources peuvent être explorées et inspectées et fournit des informations sur les attributs d’une source donnée. Le point dʼentrée `/connectionSpecs` de l’API [!DNL Flow Service] vous permet de gérer par programmation les spécifications de connexion au sein de votre organisation.

Le document suivant décrit les étapes à suivre pour créer une spécification de connexion à l’aide de l’API [!DNL Flow Service] et intégrer une nouvelle source par le biais de sources en libre-service (SDK de diffusion en continu).

## Prise en main

Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Collecter des artefacts

Pour créer une source de diffusion en continu à l’aide de la fonctionnalité Sources en libre-service, vous devez d’abord vous coordonner avec Adobe, demander un référentiel Git privé et vous aligner sur l’Adobe en ce qui concerne le libellé, la description, la catégorie et l’icône de votre source.

Une fois fourni, vous devez structurer votre référentiel Git privé comme suit :

* Sources
   * {your_source}
      * Artefacts
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefacts (noms de fichier) | Description | Exemple |
| --- | --- | --- |
| {your_source} | Nom de la source. Ce dossier doit contenir tous les artefacts liés à votre source, dans votre référentiel Git privé. | `medallia` |
| {your_source}-category.txt | Catégorie à laquelle appartient votre source, formatée en tant que fichier texte. **Remarque** : Si vous pensez que votre source ne rentre dans aucune des catégories ci-dessus, contactez votre représentant Adobe pour discuter. | `medallia-category.txt` Dans le fichier, spécifiez la catégorie de votre source, par exemple : `streaming`. |
| {your_source}-description.txt | Brève description de votre source. | [!DNL Medallia] est une source d’automatisation du marketing que vous pouvez utiliser pour importer des données [!DNL Medallia] dans Experience Platform. |
| {your_source}-icon.svg | L’image à utiliser pour représenter votre source dans le catalogue de sources Experience Platform. Cette icône doit être un fichier de SVG. |
| {your_source}-label.txt | Le nom de votre source tel qu’il doit apparaître dans le catalogue des sources Experience Platform. | Medallia |
| {your_source}-connectionSpec.json | Un fichier JSON contenant la spécification de connexion de votre source. Ce fichier n’est pas initialement requis, car vous renseignez votre spécification de connexion à mesure que vous suivez ce guide. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>Pendant la période de test de votre spécification de connexion, au lieu des valeurs clés, vous pouvez utiliser `text` dans la spécification de connexion.

Une fois que vous avez ajouté les fichiers nécessaires à votre référentiel Git privé, vous devez créer une requête de tirage (PR) que l’Adobe doit examiner. Une fois votre requête de tirage approuvée et fusionnée, vous recevez un identifiant qui peut être utilisé pour votre spécification de connexion pour faire référence au libellé, à la description et à l’icône de votre source.

Suivez ensuite les étapes décrites ci-dessous pour configurer votre spécification de connexion. Pour plus d’informations sur les différentes fonctionnalités que vous pouvez ajouter à votre source, telles que la planification avancée, le schéma personnalisé ou différents types de pagination, consultez le guide sur la [configuration des spécifications de la source](../config/sourcespec.md).

## Copier le modèle de spécification de connexion

Une fois que vous avez rassemblé les artefacts requis, copiez et collez le modèle de spécification de connexion ci-dessous dans l’éditeur de texte de votre choix. Mettez ensuite à jour les attributs entre crochets `{}` avec des informations relatives à votre source spécifique.

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## Créer une spécification de connexion {#create}

Une fois que vous avez acquis le modèle de spécification de connexion, vous pouvez commencer à créer une spécification de connexion en renseignant les valeurs appropriées qui correspondent à votre source.

Une spécification de connexion peut être divisée en deux parties distinctes : les spécifications source et les spécifications d’exploration.

Consultez les documents suivants pour plus d’informations sur les sections d’une spécification de connexion :

* [Configurer votre spécification de source](../config/sourcespec.md)
* [Configurer votre spécification d’exploration](../config/explorespec.md)

Une fois vos informations de spécification mises à jour, vous pouvez envoyer la nouvelle spécification de connexion via une requête POST au point dʼentrée `/connectionSpecs` de l’API [!DNL Flow Service].

**Format d’API**

```http
POST /connectionSpecs
```

**Requête**

La requête suivante est un exemple de spécification de connexion entièrement créée pour une source de diffusion en continu :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**Réponse**

Une réponse réussie renvoie la spécification de connexion nouvellement créée, y compris son `id` unique.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
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
    }
  ]
}
```

## Étapes suivantes

Maintenant que vous avez créé une spécification de connexion, vous devez ajouter son identifiant de spécification de connexion correspondant à une spécification de flux existante. Pour plus d’informations, suivez le tutoriel sur la [mise à jour des spécifications de flux](./update-flow-specs.md).

Pour apporter des modifications à la spécification de connexion que vous avez créée, consultez le tutoriel sur la [mise à jour des spécifications de connexion](./update-connection-specs.md).
