---
description: Découvrez comment utiliser Destination SDK pour configurer une destination Amazon S3 avec des options de formatage de fichier prédéfinies et une configuration de nom de fichier personnalisée.
title: Configurez une destination Amazon S3 avec des options de formatage de fichier prédéfinies et une configuration de nom de fichier personnalisée.
exl-id: 0ecd3575-dcda-4e5c-af5c-247d4ea13fa1
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 10%

---

# Configurez une [!DNL Amazon S3] destination avec options de formatage de fichier prédéfinies et configuration de nom de fichier personnalisé

## Présentation {#overview}

Cette page décrit l’utilisation de la Destination SDK pour configurer une destination Amazon S3 avec des valeurs par défaut prédéfinies. [options de formatage de fichier](../../server-and-file-configuration.md#file-configuration) et une [configuration du nom de fichier](../../file-based-destination-configuration.md#file-name-configuration).

Cette page affiche toutes les options de configuration disponibles pour [!DNL Amazon S3] destinations. Vous pouvez modifier les configurations affichées dans les étapes ci-dessous ou supprimer certaines parties des configurations, si nécessaire.

## Conditions préalables {#prerequisites}

Avant de passer aux étapes décrites ci-dessous, veuillez lire la section [Prise en main de la Destination SDK](../../getting-started.md) pour plus d’informations sur l’obtention des informations d’authentification d’Adobe I/O nécessaires et d’autres conditions préalables requises pour utiliser les API Destination SDK.

## Étape 1 : créer une configuration de serveur et de fichier {#create-server-file-configuration}

Commencez par utiliser la variable `/destination-server` point d’entrée pour créer une configuration de serveur et de fichier. Pour obtenir des descriptions détaillées des paramètres de la requête HTTP, lisez la section [spécifications de configuration du serveur et des fichiers pour les destinations basées sur des fichiers](../../server-and-file-configuration.md#s3-example) et le [configurations de mise en forme des fichiers](../../server-and-file-configuration.md#file-configuration).

**Format d’API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Requête**

La requête suivante crée une nouvelle configuration de serveur de destination, configurée en fonction des paramètres fournis dans la payload.
La payload ci-dessous inclut un [!DNL Amazon S3] configuration, avec prédéfini, par défaut [Formatage des fichiers CSV](../../server-and-file-configuration.md#file-configuration) paramètres de configuration que les utilisateurs peuvent définir dans l’interface utilisateur de l’Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "Amazon S3 destination server with predefined default CSV options",
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
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}'
```

Une réponse réussie renvoie la nouvelle configuration du serveur de destination, y compris l’identifiant unique (`instanceId`) de la configuration. Conservez cette valeur, car elle est nécessaire à l’étape suivante.

## Étape 2 : créer une configuration de destination {#create-destination-configuration}

Après avoir créé la configuration du serveur de destination et du formatage des fichiers à l’étape précédente, vous pouvez désormais utiliser la variable `/destinations` Point de terminaison de l’API pour créer une configuration de destination.

Pour connecter la configuration du serveur dans [étape 1](#create-server-file-configuration) sur cette configuration de destination, remplacez la variable `destinationServerId` dans la requête d’API ci-dessous avec la variable `instanceId` valeur obtenue lors de la création du serveur de destination dans [étape 1](#create-server-file-configuration).

Pour obtenir des descriptions détaillées des paramètres utilisés ci-dessous, consultez les pages suivantes :

* [Configuration de l’authentification](../../authentication-configuration.md#s3)
* [Configuration de la destination du lot](../../file-based-destination-configuration.md#batch-configuration)
* [Opérations de l’API de configuration des destinations basées sur des fichiers](../../destination-configuration-api.md#create-file-based)

**Format d’API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

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
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "releaseNotes":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"File type",
         "description":"Select the exported file type.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

Une réponse réussie renvoie la nouvelle configuration de destination, y compris l’identifiant unique (`instanceId`) de la configuration. Conservez cette valeur, car elle est nécessaire si vous devez effectuer d’autres requêtes HTTP pour mettre à jour la configuration de votre destination.

## Étape 3 : Vérification de l’interface utilisateur Experience Platform {#verify-ui}

En fonction des configurations ci-dessus, le catalogue des Experience Platform affiche désormais une nouvelle carte de destination privée que vous pouvez utiliser.

![Enregistrement de l’écran affichant la page du catalogue des destinations avec une carte de destination sélectionnée.](../../assets/destination-card.gif)

Dans les images et enregistrements ci-dessous, notez comment les options de la variable [workflow d’activation pour les destinations basées sur des fichiers](/help/destinations/ui/activate-batch-profile-destinations.md) correspondent aux options que vous avez sélectionnées dans la configuration de destination.

Lorsque vous renseignez des détails sur la destination, notez comment les champs sont apparus comme les champs de données personnalisés que vous configurez dans la configuration.

>[!TIP]
>
>L’ordre dans lequel vous ajoutez les champs de données personnalisés à la configuration de destination n’est pas reflété dans l’interface utilisateur. Les champs de données du client sont toujours affichés dans l&#39;ordre indiqué dans l&#39;enregistrement à l&#39;écran ci-dessous.

![Enregistrement d’écran présentant les champs de données client définis dans votre configuration.](../../assets/file-configuration-options.gif)

Lors de la planification des intervalles d’exportation, notez comment les champs apparaissaient sont les champs que vous configurez dans la variable `batchConfig` configuration.
![options de planification d’exportation](../../assets/file-export-scheduling.png)

Lors de l’affichage des options de configuration du nom de fichier, notez comment les champs affichés représentent le `filenameConfig` options que vous configurez dans la configuration.
![options de configuration du nom de fichier](../../assets/file-naming-options.gif)

Si vous souhaitez ajuster l’un des champs mentionnés ci-dessus, répétez l’opération. [étapes 1](#create-server-file-configuration) et [two](#create-destination-configuration) pour modifier les configurations selon vos besoins.

## Étape 4 : (Facultatif) Publiez votre destination {#publish-destination}

>[!NOTE]
>
>Cette étape n’est pas requise si vous créez une destination privée à des fins personnelles et que vous ne souhaitez pas la publier dans le catalogue de destinations pour que d’autres clients puissent l’utiliser.

Après avoir configuré votre destination, utilisez la variable [API de publication de destination](../../destination-publish-api.md) pour envoyer votre configuration à Adobe en vue de la révision.

## Étape 5 : (Facultatif) Document de votre destination {#document-destination}

>[!NOTE]
>
>Cette étape n’est pas requise si vous créez une destination privée à des fins personnelles et que vous ne souhaitez pas la publier dans le catalogue de destinations pour que d’autres clients puissent l’utiliser.

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) créant une [intégration personnalisée](../../overview.md#productized-custom-integrations), utilisez le [processus de documentation en libre-service](../../docs-framework/documentation-instructions.md) pour créer une page de documentation du produit pour votre destination dans le [Catalogue des destinations Experience Platform](../../../catalog/overview.md).

## Étapes suivantes {#next-steps}

En lisant cet article, vous savez maintenant comment créer une [!DNL Amazon S3] destination à l’aide de Destination SDK. Ensuite, votre équipe peut utiliser la variable [workflow d’activation pour les destinations basées sur des fichiers](../../../ui/activate-batch-profile-destinations.md) pour exporter des données vers la destination.
