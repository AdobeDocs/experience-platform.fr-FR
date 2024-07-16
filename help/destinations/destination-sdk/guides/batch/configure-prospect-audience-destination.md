---
description: Découvrez comment utiliser Destination SDK pour configurer une destination basée sur des fichiers afin d’exporter des audiences de prospects vers un emplacement de stockage.
title: Configuration d’une destination basée sur des fichiers pour exporter des audiences de prospects vers un emplacement de stockage
exl-id: 052fd185-294a-4c1d-8d82-12b27b661e22
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 8%

---

# Configuration d’une destination basée sur des fichiers pour exporter des audiences de prospects vers un emplacement de stockage

## Vue d’ensemble {#overview}

Cette page décrit comment utiliser la Destination SDK pour configurer une destination basée sur un fichier avec des [ options de formatage de fichier ](configure-file-formatting-options.md) personnalisées et une [ configuration de nom de fichier ](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration) personnalisée pour exporter des [audiences prospect](/help/destinations/ui/activate-prospect-audiences.md). Les exemples de ce guide décrivent comment exporter des audiences de profils de prospect vers un emplacement Amazon S3.

Vous pouvez également configurer des emplacements de stockage STFP ou autres pour exporter des audiences de prospects. La partie importante à retenir est d’ajouter le fragment de code ci-dessous à la configuration de destination dans l’ [étape 2](#create-destination-configuration) pour permettre au [ workflow d’exporter les audiences de prospects](/help/destinations/ui/activate-prospect-audiences.md) vers la destination.

```json
  "sources": [
    "UNIFIED_PROFILE_PROSPECTS"
  ],
```

Pour obtenir des descriptions détaillées des paramètres utilisés ci-dessous, voir [options de configuration dans le SDK Destinations](../../functionality/configuration-options.md).

## Conditions préalables {#prerequisites}

Avant de passer aux étapes décrites ci-dessous, consultez la page [Prise en main de la Destination SDK](../../getting-started.md) pour plus d’informations sur l’obtention des informations d’authentification nécessaires et d’autres conditions préalables requises pour utiliser les API Destination SDK.

## Étape 1 : créer une configuration de serveur et de fichier {#create-server-file-configuration}

Commencez par utiliser le point d’entrée `/destination-server` pour [créer une configuration de serveur et de fichier](../../authoring-api/destination-server/create-destination-server.md).

**Format d’API**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Requête**

La requête suivante crée une configuration de serveur de destination, configurée par les paramètres fournis dans la payload.
La payload ci-dessous inclut une configuration Amazon S3 générique, avec des paramètres de configuration [formatage de fichier CSV](../../functionality/destination-server/file-formatting.md) personnalisés que les utilisateurs peuvent définir dans l’interface utilisateur de l’Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
   "name":"Amazon S3 destination server with custom file formatting options",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.compression}}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.sep}}"
         },
         "encoding":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.encoding}}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.quote}}"
         },
         "quoteAll":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.quoteAll}}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.escape}}"
         },
         "escapeQuotes":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.escapeQuotes}}"
         },
         "header":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.header}}"
         },
         "ignoreLeadingWhiteSpace":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.ignoreLeadingWhiteSpace}}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.nullValue}}"
         },
         "dateFormat":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.dateFormat}}"
         },
         "charToEscapeQuoteEscaping":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.charToEscapeQuoteEscaping}}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.dateFormat}}"
         }
      }
   }
}'
```

Une réponse réussie renvoie la nouvelle configuration du serveur de destination, y compris l’identifiant unique (`instanceId`) de la configuration. Conservez cette valeur, car elle est nécessaire à l’étape suivante.

## Étape 2 : créer une configuration de destination {#create-destination-configuration}

Après avoir créé la configuration de mise en forme du serveur de destination et des fichiers à l’étape précédente, vous pouvez désormais utiliser le point d’entrée de l’API `/destinations` pour créer une configuration de destination.

Pour connecter la configuration du serveur de l’ [étape 1](#create-server-file-configuration) à cette configuration de destination, remplacez la valeur `destinationServerId` de la requête API ci-dessous par la valeur obtenue lors de la création de votre serveur de destination à l’ [étape 1](#create-server-file-configuration).

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
   "name":"Amazon S3 destination to export prospect audiences",
   "description":"Amazon S3 destination to export prospect audiences",
   "status":"TEST",
   "sources": [
    "UNIFIED_PROFILE_PROSPECTS"
   ],
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
      
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
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
         "DAILY_FULL_EXPORT"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
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

![ Enregistrement d’écran affichant la page du catalogue des destinations avec une carte de destination sélectionnée.](../../assets/guides/batch/destination-card.gif)

Dans les images et enregistrements ci-dessous, notez comment les options du [workflow d’activation pour les destinations basées sur des fichiers](../../../ui/activate-batch-profile-destinations.md) correspondent aux options que vous avez sélectionnées dans la configuration de destination.

Lorsque vous renseignez des détails sur la destination, notez comment les champs sont apparus comme les champs de données personnalisés que vous configurez dans la configuration.

>[!TIP]
>
>L’ordre dans lequel vous ajoutez les champs de données personnalisés à la configuration de destination n’est pas reflété dans l’interface utilisateur. Les champs de données personnalisés sont toujours affichés dans l’ordre indiqué dans l’enregistrement à l’écran ci-dessous.

![ Renseignez les détails de destination](../../assets/guides/batch/file-configuration-options.gif)

Lors de la planification des intervalles d’exportation, notez comment les champs sont apparus comme les champs que vous avez configurés dans la configuration `batchConfig`.
![options de planification d’exportation](../../assets/guides/batch/ui-view-scheduling-prospect-destination.png)

Lors de l’affichage des options de configuration du nom de fichier, notez comment les champs sont apparus représentent les options `filenameConfig` que vous avez configurées dans la configuration.
![options de configuration du nom de fichier](../../assets/guides/batch/file-naming-options.gif)

Si vous souhaitez ajuster l’un des champs mentionnés ci-dessus, répétez les [étapes un](#create-server-file-configuration) et [deux](#create-destination-configuration) pour modifier les configurations selon vos besoins.

## Étape 4 : (facultative) Publish votre destination {#publish-destination}

>[!NOTE]
>
>Cette étape n’est pas requise si vous créez une destination privée à des fins personnelles et que vous ne souhaitez pas la publier dans le catalogue de destinations pour que d’autres clients puissent l’utiliser.

Après avoir configuré votre destination, utilisez l’ [API de publication de destination](../../publishing-api/create-publishing-request.md) pour envoyer votre configuration à Adobe pour révision.

## Étape 5 : (facultative) documenter votre destination {#document-destination}

>[!NOTE]
>
>Cette étape n’est pas requise si vous créez une destination privée à des fins personnelles et que vous ne souhaitez pas la publier dans le catalogue de destinations pour que d’autres clients puissent l’utiliser.

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) créant une [intégration personnalisée](../../overview.md#productized-custom-integrations), utilisez le [processus de documentation en libre-service](../../docs-framework/documentation-instructions.md) pour créer une page de documentation du produit pour votre destination dans le [Catalogue des destinations Experience Platform](../../../catalog/overview.md).

## Étapes suivantes {#next-steps}

En lisant cet article, vous savez maintenant comment utiliser la Destination SDK pour créer une destination [!DNL Amazon S3] personnalisée afin d’exporter des audiences de prospects.
