---
description: Cette page répertorie et décrit les étapes de configuration d’une destination basée sur des fichiers à l’aide de Destination SDK.
title: Utilisation de Destination SDK pour configurer une destination basée sur des fichiers
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 71%

---

# Utilisation de Destination SDK pour configurer une destination basée sur des fichiers

## Vue d’ensemble {#overview}

Cette page décrit comment utiliser les informations contenues dans la section [Options de configuration dans Destination SDK](../functionality/configuration-options.md) et dans dʼautres documents de référence sur les fonctionnalités et lʼAPI Destination SDK pour configurer une [destination basée sur des fichiers](../../destination-types.md#file-based). Les étapes sont présentées dans l’ordre séquentiel ci-dessous.

## Conditions préalables {#prerequisites}

Avant dʼeffectuer les étapes illustrées ci-dessous, consultez la page [Prise en main de Destination SDK](../getting-started.md) pour plus d’informations sur l’obtention des informations d’authentification Adobe I/O nécessaires et d’autres conditions préalables requises pour utiliser les API Destination SDK.

## Étapes à suivre pour utiliser les options de configuration de Destination SDK afin de configurer votre destination. {#steps}

![Étapes illustrées d’utilisation des points d’entrée de Destination SDK](../assets/guides/destination-sdk-steps-batch.png)

## Étape 1 : créer une configuration de serveur et de fichier {#create-server-file-configuration}

Commencer par [création d’une configuration de serveur et de fichier](../authoring-api/destination-server/create-destination-server.md) en utilisant la variable `/destinations-server` point de terminaison .

Vous trouverez ci-dessous un exemple de configuration pour une destination [!DNL Amazon S3]. Pour configurer d’autres types de destinations basées sur des fichiers, consultez leurs [configurations de serveur](../functionality/destination-server/server-specs.md).

**Format d’API**

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucketName": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
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
}
```

## Étape 2 : créer une configuration de destination {#create-destination-configuration}

Vous trouverez ci-dessous un exemple de configuration de destination, créée à l’aide du point d’entrée de l’API `/destinations`. 

Pour connecter la configuration du serveur et des fichiers de l’étape 1 à cette configuration de destination, ajoutez l’ID d’instance du serveur et la configuration de modèle en tant que `destinationServerId` ici.

**Format d’API**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="84"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
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
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
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
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## Étape 3 : créer une configuration de métadonnées d’audience {#create-audience-metadata-configuration}

Pour certaines destinations, Destination SDK exige que vous configuriez des métadonnées d’audience afin de créer, mettre à jour ou supprimer des audiences par programmation dans votre destination. Pour plus d’informations sur le moment et la manière d’effectuer cette configuration, consultez la section [Gestion des métadonnées d’audience](../functionality/audience-metadata-management.md).

Si vous utilisez une configuration de métadonnées d’audience, vous devez la connecter à la configuration de destination créée à l’étape 2. Ajoutez l’ID d’instance de votre configuration de métadonnées d’audience à votre configuration de destination en tant que `audienceTemplateId`.

```json {line-numbers="true" highlight="91"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
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
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "audienceMetadataConfig":{
    "mapExperiencePlatformSegmentName":false,
    "mapExperiencePlatformSegmentId":false,
    "mapUserInput":false,
    "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
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
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## Étape 4 : configurer l’authentification {#set-up-authentication}

Selon que vous spécifiez `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` dans la configuration de destination ci-dessus, vous pouvez configurer l’authentification pour votre destination à l’aide du point d’entrée `/destination` ou `/credentials`.

* Si vous avez sélectionné `"authenticationRule": "CUSTOMER_AUTHENTICATION"` dans la configuration des destinations, reportez-vous aux sections suivantes pour connaître les types d’authentification pris en charge par Destination SDK pour les destinations basées sur des fichiers :

   * [Authentification Amazon S3](../functionality/destination-configuration/customer-authentication.md#s3)
   * [Azure Blob](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Azure Data Lake Storage](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Google Cloud Storage](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [Authentification SFTP avec clé SSH](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [Authentification SFTP avec mot de passe](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* Si vous avez sélectionné `"authenticationRule": "PLATFORM_AUTHENTICATION"`, reportez-vous à la section [documentation de l’API de configuration des informations d’identification](../credentials-api/create-credential-configuration.md#when-to-use).


## Étape 5 : tester votre destination {#test-destination}

Une fois votre destination configurée à l’aide des points d’entrée de configuration dans les étapes précédentes, vous pouvez utiliser l’[outil de test des destinations](../testing-api/batch-destinations/file-based-destination-testing-overview.md) afin de tester l’intégration entre Adobe Experience Platform et votre destination.

Dans le cadre du processus de test de votre destination, vous devez utiliser l’interface utilisateur d’Experience Platform pour créer des segments que vous activerez vers votre destination. Reportez-vous aux deux ressources ci-dessous pour savoir comment créer des audiences dans Experience Platform :

* [Création d’une page de documentation sur l’audience](/help/segmentation/ui/overview.md#create-segment)
* [Présentation vidéo de la création d’une audience](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=fr)

## Étape 6 : publier votre destination {#publish-destination}

>[!NOTE]
>
>Cette étape n’est pas requise si vous créez une destination privée à des fins personnelles et que vous ne souhaitez pas la publier dans le catalogue de destinations pour que d’autres clients puissent l’utiliser.

Une fois votre destination configurée et testée, utilisez l’[API de publication de destination](../publishing-api/create-publishing-request.md) afin d’envoyer votre configuration à Adobe pour révision.

## Étape 7 : documenter votre destination {#document-destination}

>[!NOTE]
>
>Cette étape n’est pas requise si vous créez une destination privée à des fins personnelles et que vous ne souhaitez pas la publier dans le catalogue de destinations pour que d’autres clients puissent l’utiliser.

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) créant une [intégration personnalisée](../overview.md#productized-custom-integrations), utilisez le [processus de documentation en libre-service](../docs-framework/documentation-instructions.md) pour créer une page de documentation du produit pour votre destination dans le [Catalogue des destinations Experience Platform](/help/destinations/catalog/overview.md).

## Étape 8 : Envoyer la destination pour la révision de l’Adobe {#submit-for-review}

>[!NOTE]
>
>Cette étape n’est pas requise si vous créez une destination privée à des fins personnelles et que vous ne souhaitez pas la publier dans le catalogue de destinations pour que d’autres clients puissent l’utiliser.

Enfin, avant que la destination puisse être publiée dans le catalogue des Experience Platform et visible par tous les clients Experience Platform, vous devez envoyer officiellement la destination pour la révision de l’Adobe. Obtention d’informations complètes sur la procédure à suivre [envoyer pour révision une destination productisée créée en Destination SDK](../guides/submit-destination.md).
