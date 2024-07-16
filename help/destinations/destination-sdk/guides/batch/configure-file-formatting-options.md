---
description: Configuration des options de formatage de fichier pour les destinations basées sur des fichiers
title: Découvrez comment utiliser Destination SDK pour configurer les options de formatage de fichier pour les destinations basées sur des fichiers.
exl-id: e61c7989-1123-4b3b-9781-a6097cd0e2b4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 22%

---

# Configuration des options de formatage de fichier pour les destinations basées sur des fichiers

## Vue d’ensemble {#overview}

Destination SDK vous permet d’ajuster considérablement les options de formatage et de compression de vos fichiers exportés, afin de répondre à toutes les exigences en aval de votre emplacement de stockage.

Cette page décrit comment utiliser la Destination SDK pour configurer les options de formatage de fichier pour les destinations basées sur des fichiers.

## Conditions préalables {#prerequisites}

Avant de passer aux étapes décrites ci-dessous, consultez la page [Prise en main de la Destination SDK](../../getting-started.md) pour plus d’informations sur l’obtention des informations d’identification d’authentification d’Adobe I/O nécessaires et d’autres conditions préalables requises pour utiliser les API Destination SDK.

Adobe vous recommande également de lire et de vous familiariser avec la documentation suivante avant de poursuivre :

* Chaque option de mise en forme de fichier disponible est documentée en détail dans la section [configuration de mise en forme de fichier](../../functionality/destination-server/file-formatting.md) .
* Suivez les étapes pour [configurer une destination basée sur un fichier](../../guides/configure-file-based-destination-instructions.md) à l’aide de Destination SDK.

## Création d’une configuration de serveur et de fichier {#create-server-file-configuration}

Commencez par utiliser le point de terminaison `/destination-server` pour déterminer les options de configuration de formatage de fichier que vous souhaitez configurer pour les fichiers exportés.

Vous trouverez ci-dessous un exemple de configuration de serveur de destination pour une destination [!DNL Amazon S3], avec plusieurs options de mise en forme de fichier sélectionnées.

**Format d’API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
{
  "name": "Amazon S3 Server with several CSV Options",
  "destinationServerType": "FILE_BASED_S3",
  "fileBasedS3Destination": {
    "bucket": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.bucket}}"
    },
    "path": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.path}}"
    }
  },
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
}
}'
```

## Ajouter les options de formatage de fichier à la configuration de destination {#create-destination-configuration}

>[!TIP]
>
>**Vérifiez l’interface utilisateur Experience Platform**. Lorsque vous configurez les options de formatage de fichier avec les configurations illustrées dans les sections ci-dessous, vous devez vérifier le rendu de ces options dans l’interface utilisateur de l’Experience Platform.

Après avoir ajouté les options de formatage de fichier souhaitées à la configuration du serveur de destination et du formatage des fichiers à l’étape précédente, vous pouvez désormais utiliser le point de terminaison de l’API `/destinations` pour ajouter les champs de votre choix en tant que champs de données client à la configuration de destination.

>[!IMPORTANT]
>
>Cette étape est facultative et détermine uniquement les options de formatage de fichier qui doivent être affichées pour les utilisateurs dans l’interface utilisateur de l’Experience Platform. Si vous ne configurez pas les options de formatage de fichier en tant que champs de données client, les exportations de fichiers se dérouleront avec les valeurs par défaut configurées dans la [configuration du serveur et du fichier](#create-server-file-configuration).

Au cours de cette étape, vous pouvez regrouper les options affichées dans l’ordre de votre choix. Vous pouvez ainsi créer des regroupements personnalisés, des champs de liste déroulante et des regroupements conditionnels en fonction des types de fichiers sélectionnés. Tous ces paramètres sont affichés dans l’enregistrement et dans les sections ci-dessous.

![Enregistrement d’écran présentant diverses options de formatage de fichier pour les fichiers de lot.](../../assets/guides/batch/file-formatting-options.gif)

### Classer les options de formatage du fichier {#ordering}

L’ordre dans lequel vous ajoutez les options de formatage de fichier en tant que champs de données client dans la configuration de destination est reflété dans l’interface utilisateur. Par exemple, la configuration ci-dessous est reflétée en conséquence dans l’interface utilisateur, avec les options qui s’affichent dans l’ordre **[!UICONTROL Délimiteur]**, **[!UICONTROL Caractère de citation]**, **[!UICONTROL Caractère d’échappement]**, **[!UICONTROL Valeur vide]**, **[!UICONTROL Valeur nulle]**.

![Image indiquant l’ordre des options de formatage de fichier dans l’interface utilisateur d’Experience Platform.](../../assets/guides/batch/file-formatting-order.png)

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\u0000",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": ""
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
```

### Regrouper les options de formatage de fichier {#grouping}

Vous pouvez regrouper plusieurs options de formatage de fichier dans une seule section. Lors de la configuration de la connexion à la destination dans l’interface utilisateur, l’utilisateur peut voir et bénéficier d’un regroupement visuel de champs similaires.

Pour ce faire, utilisez `"type": "object"` pour créer le groupe et collecter les options de formatage de fichier souhaitées dans un paramètre `properties`, comme illustré dans l’exemple ci-dessous, où le regroupement **[!UICONTROL CSV Options]** est mis en surbrillance.

```json {line-numbers="true" start-number="100" highlight="106-128"}
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![Image présentant le regroupement des options CSV dans l’interface utilisateur.](../../assets/guides/batch/file-formatting-grouping.png)

### Création de sélecteurs de liste déroulante pour les options de formatage de fichier {#dropdown-selectors}

Dans les cas où vous souhaitez permettre aux utilisateurs de sélectionner plusieurs options (par exemple, le caractère qui doit être utilisé pour délimiter les champs dans les fichiers CSV), vous pouvez ajouter des champs de liste déroulante à l’interface utilisateur.

Pour ce faire, utilisez l’objet `namedEnum` comme illustré ci-dessous et configurez une valeur `default` pour les options que l’utilisateur peut sélectionner.

```json {line-numbers="true" start-number="100" highlight="114-124"}
[...]
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![Enregistrement d’écran montrant un exemple de sélecteurs de liste déroulante créée avec la configuration affichée ci-dessus.](../../assets/guides/batch/dropdown-options-file-formatting.gif)

### Création d’options de mise en forme de fichier conditionnelle {#conditional-options}

Vous pouvez créer des options de mise en forme de fichier conditionnel qui s’affichent dans le workflow d’activation uniquement lorsque l’utilisateur sélectionne un certain type de fichier à exporter. Par exemple, la configuration ci-dessous crée un regroupement conditionnel pour les options de fichier CSV. Les options de fichier CSV s’affichent uniquement quand l’utilisateur sélectionne CSV comme type de fichier souhaité pour l’exportation.

Pour définir un champ comme conditionnel, utilisez le paramètre `conditional` comme illustré ci-dessous :

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

Dans un contexte plus large, vous pouvez voir le champ `conditional` utilisé dans la configuration de destination ci-dessous, avec le champ `fileType` et l’objet `csvOptions` dans lequel il est défini.

```json
        {
            "name": "fileType",
            "title": "File Type",
            "description": "Select your file type",
            "type": "string",
            "isRequired": true,
            "enum": [
                "PARQUET",
                "CSV",
                "JSON"
            ],
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            },            
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": "\u0000"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
            ],
            "isRequired": false,
            "readOnly": false,
            "hidden": false
        }
```

Vous trouverez ci-dessous l’écran de l’interface utilisateur qui en résulte, en fonction de la configuration ci-dessus. Quand l’utilisateur sélectionne le type de fichier CSV, d’autres options de mise en forme de fichier faisant référence au type de fichier CSV s’affichent dans l’interface utilisateur.

![Enregistrement d’écran affichant l’option de formatage de fichier conditionnel pour les fichiers CSV.](../../assets/guides/batch/conditional-file-formatting.gif)

### Demande d’API complète incluant toutes les options ci-dessus

La requête d’API ci-dessous combine dans une configuration toutes les options décrites dans les sections ci-dessus.

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "name": "My S3 Destination",
  "description": "Test destination",
  "status": "TEST",
  "sources": [
    "UNIFIED_PROFILE"
  ],
  "customerAuthenticationConfigurations": [
    {
      "authType": "S3"
    }
  ],
  "customerDataFields": [
    {
      "name": "bucket",
      "type": "string",
      "title": "Bucket",
      "description": "Enter your S3 Bucket",
      "isRequired": true
    },
    {
      "name": "path",
      "type": "string",
      "title": "Path",
      "description": "Enter your S3 Path",
      "isRequired": true
    },
    {
      "name": "fileType",
      "type": "string",
      "enum": [
        "CSV",
        "JSON",
        "PARQUET"
      ],
      "title": "File Type",
      "description": "Select your file type",
      "isRequired": true
    },
    {
      "name": "csvOptions",
      "type": "object",
      "title": "CSV Options",
      "description": "Select your CSV options",
      "conditional": {
        "field": "fileType",
        "operator": "EQUALS",
        "value": "CSV"
      },
      "properties": [
        {
          "name": "delimiter",
          "type": "string",
          "title": "Delimiter",
          "description": "Select your Delimiter",
          "namedEnum": [
            {
              "name": "Comma (,)",
              "value": ","
            },
            {
              "name": "Tab (\\t)",
              "value": "\t"
            }
          ],
          "default": ","
        },
        {
          "name": "quote",
          "type": "string",
          "title": "Quote Character",
          "description": "Select your Quote character",
          "namedEnum": [
            {
              "name": "Double Quotes (\")",
              "value": "\""
            },
            {
              "name": "Null Character (\\u0000)",
              "value": "\u0000"
            }
          ],
          "default": "\u0000"
        },
        {
          "name": "escape",
          "type": "string",
          "title": "Escape Character",
          "description": "Select your Escape character",
          "namedEnum": [
            {
              "name": "Back Slash (\\)",
              "value": "\\"
            },
            {
              "name": "Single Quote (')",
              "value": "'"
            }
          ],
          "default": "\\"
        },
        {
          "name": "emptyValue",
          "type": "string",
          "title": "Empty Value",
          "description": "Select the output value of blank fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": ""
        },
        {
          "name": "nullValue",
          "type": "string",
          "title": "Null Value",
          "description": "Select the output value of 'null' fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": "null"
        }
      ]
    }
  ],
  "uiAttributes": {
    "documentationLink": "https://www.adobe.com/go/aep",
    "category": "cloudStorage",
    "connectionType": "Server-to-server",
    "frequency": "Batch",
    "monitoringSupported": true,
    "flowRunsSupported": true
  },
  "schemaConfig": {
    "profileRequired": true,
    "segmentRequired": true,
    "identityRequired": true
  },
  "batchConfig": {
    "allowMandatoryFieldSelection": true,
    "allowDedupeKeyFieldSelection": true,
    "defaultExportMode": "DAILY_FULL_EXPORT",
    "allowedExportMode": [
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
    ],
    "allowedScheduleFrequency": [
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
    ],
    "defaultFrequency": "DAILY",
    "defaultStartTime": "00:00",
    "filenameConfig": {
      "allowedFilenameAppendOptions": [
        "SEGMENT_NAME",
        "DESTINATION_INSTANCE_ID",
        "DESTINATION_INSTANCE_NAME",
        "ORGANIZATION_NAME",
        "SANDBOX_NAME",
        "DATETIME",
        "CUSTOM_TEXT"
      ],
      "defaultFilenameAppendOptions": [
        "DATETIME"
      ],
      "defaultFilename": "%DESTINATION%_%SEGMENT_ID%"
    }
  },
  "destinationDelivery": [
    {
      "deliveryMatchers": [
        {
          "type": "SOURCE",
          "value": [
            "batch"
          ]
        }
      ],
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "destinationServerId": "<server-id>"
    }
  ]
}'
```

Une réponse réussie renvoie la configuration de destination, y compris l’identifiant unique (`instanceId`) de la configuration.

## Limites connues {#known-limitations}

Une certaine combinaison d’options de formatage de fichier peut entraîner des résultats d’exportation de fichier indésirables.
Adobe recommande de ne pas sélectionner la combinaison d’options CSV suivante :

```
nullValue -> ""
quote -> "
emptyValue -> ""
```

Pour illustrer cette limitation, envisagez d’exporter un fichier avec les valeurs ci-dessous :

| prénom | nom | pays | state |
|---------|----------|---------|--------|
| Michael | Rose | USA | NY |
| James | Smith |  | null |

{style="table-layout:auto"}

Cela entraînerait une sortie comme illustré ci-dessous. Notez comment la valeur nulle de la table est incorrectement exportée sous forme de guillemet avec échappement.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## Étapes suivantes {#next-steps}

En lisant cet article, vous savez maintenant comment configurer des options de formatage de fichier personnalisées pour vos fichiers exportés, à l’aide de Destination SDK. Ensuite, votre équipe peut utiliser le [workflow d’activation pour les destinations basées sur des fichiers](../../../ui/activate-batch-profile-destinations.md) pour exporter des données vers la destination.
