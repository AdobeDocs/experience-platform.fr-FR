---
description: Cette page illustre l’appel API utilisé pour mettre à jour une configuration de destination existante en Adobe Experience Platform Destination SDK.
title: Mise à jour d’une configuration de destination
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 28%

---


# Mise à jour d’une configuration de destination

Cette page illustre la requête d’API et la charge utile que vous pouvez utiliser pour mettre à jour une configuration de destination existante, en utilisant la variable `/authoring/destinations` Point d’entrée de l’API.

>[!TIP]
>
>Toute opération de mise à jour sur des destinations productisées/publiques n’est visible qu’après avoir utilisé la variable [API de publication](../../publishing-api/create-publishing-request.md) et envoyer la mise à jour pour la révision des Adobes.

Pour une description détaillée des fonctionnalités d’une configuration de destination, lisez les articles suivants :

* [Configuration de l’authentification du client](../../functionality/destination-configuration/customer-authentication.md)
* [Authentification OAuth 2](../../functionality/destination-configuration/oauth2-authentication.md)
* [Champs de données client](../../functionality/destination-configuration/customer-data-fields.md)
* [Attributs de l’interface utilisateur](../../functionality/destination-configuration/ui-attributes.md)
* [Configuration du schéma](../../functionality/destination-configuration/schema-configuration.md)
* [Configuration de l’espace de noms d’identité](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Diffusion de destination](../../functionality/destination-configuration/destination-delivery.md)
* [Configuration des métadonnées d’audience](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configuration des métadonnées d’audience](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Politique d’agrégation](../../functionality/destination-configuration/aggregation-policy.md)
* [Configuration par lots](../../functionality/destination-configuration/batch-configuration.md)
* [Qualifications des profils historiques](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API de configuration de destination {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Mise à jour d’une configuration de destination {#update}

Vous pouvez mettre à jour une [existant](create-destination-configuration.md) configuration de destination en effectuant une `PUT` à la fonction `/authoring/destinations` point de terminaison avec la payload mise à jour.

>[!TIP]
>
>Point d’entrée de l’API: `platform.adobe.io/data/core/activation/authoring/destinations`

Pour obtenir une configuration de destination existante et sa `{INSTANCE_ID}`, voir l’article sur [récupération d’une configuration de destination](retrieve-destination-configuration.md).

**Format d’API**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration de destination à mettre à jour. Pour obtenir une configuration de destination existante et sa `{INSTANCE_ID}`, voir [Récupération d’une configuration de destination](retrieve-destination-configuration.md). |

+++Requête

La requête suivante met à jour la destination que nous avons créée dans [cet exemple](create-destination-configuration.md#create) avec différent `filenameConfig` options.

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration de destination mise à jour.

+++

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment mettre à jour une configuration de destination via la Destination SDK `/authoring/destinations` Point d’entrée de l’API.

Pour en savoir plus sur ce que vous pouvez faire avec ce point de terminaison, consultez les articles suivants :

* [Création d’une configuration de destination](create-destination-configuration.md)
* [Récupération d’une configuration de destination](retrieve-destination-configuration.md)
* [Suppression d’une configuration de destination](delete-destination-configuration.md)