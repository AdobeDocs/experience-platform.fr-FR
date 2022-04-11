---
description: Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point d’entrée de l’API « /authoring/destinations ».
title: Opérations de point d’entrée de l’API Destinations
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 51417bee5dba7a96d3a7a7eb507fc95711fad4a5
workflow-type: tm+mt
source-wordcount: '2537'
ht-degree: 98%

---

# Opérations de l’API du point d’entrée des destinations {#destination-configuration}

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations`

Cette page répertorie et décrit toutes les opérations de l’API que vous pouvez effectuer à l’aide du point d’entrée de l’API `/authoring/destinations`. Pour une description des fonctionnalités prises en charge par ce point d’entrée, consultez la [configuration de la destination](./destination-configuration.md).

## Prise en main des opérations d’API de destination {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md), qui contient des informations importantes à connaître pour réussir à effectuer des appels vers l’API, notamment pour obtenir lʼautorisation de création de destination et les en-têtes requis.

## Créer une configuration pour une destination de diffusion en continu {#create}

Vous pouvez créer une configuration de destination en effectuant une requête POST au point d’entrée `/authoring/destinations`.

**Format d’API**

```http
POST /authoring/destinations
```

**Requête**

La requête suivante crée une destination de diffusion en continu, configurée en fonction des paramètres fournis dans la payload. Le payload ci-dessous inclut tous les paramètres pour les destinations de diffusion en continu acceptées par le point d’entrée `/authoring/destinations`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

```json
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `name` | Chaîne | Indique le titre de votre destination dans le catalogue Experience Platform. |
| `description` | Chaîne | Fournissez une description qu’Adobe utilisera dans le catalogue des destinations Experience Platform pour votre carte de destination. N’utilisez pas plus de 4 à 5 phrases. |
| `status` | Chaîne | Indique le statut du cycle de vie de la carte de destination. Les valeurs acceptées sont `TEST`, `PUBLISHED` et `DELETED`. Utilisez `TEST` lorsque vous configurez votre destination pour la première fois. |
| `customerAuthenticationConfigurations` | Chaîne | Indique la configuration utilisée pour authentifier les clients Experience Platform sur votre serveur. Consultez `authType` ci-dessous pour les valeurs acceptées. |
| `customerAuthenticationConfigurations.authType` | Chaîne | Les valeurs prises en charge pour les destinations de diffusion en continu sont les suivantes : <ul><li>`OAUTH2`</li><li>`BEARER`</li></ul> Les valeurs prises en charge pour les destinations basées sur des fichiers sont les suivantes : <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | Chaîne | Attribuez un nom au champ personnalisé que vous introduisez. |
| `customerDataFields.type` | Chaîne | Indique le type de champ personnalisé que vous introduisez. Les valeurs acceptées sont `string`, `object` et `integer`. |
| `customerDataFields.title` | Chaîne | Indique le nom du champ, tel qu’il est affiché par les clients dans l’interface utilisateur d’Experience Platform. |
| `customerDataFields.description` | Chaîne | Fournissez une description du champ personnalisé. |
| `customerDataFields.isRequired` | Booléen | Indique si ce champ est requis dans le workflow de configuration de destination. |
| `customerDataFields.enum` | Chaîne | Rend le champ personnalisé sous forme de menu déroulant et répertorie les options disponibles pour l’utilisateur. |
| `customerDataFields.pattern` | Chaîne | Impose un modèle pour le champ personnalisé, le cas échéant. Utilisez des expressions régulières pour appliquer un modèle. Par exemple, si vos identifiants de client n’incluent pas de chiffres ou de traits de soulignement, saisissez `^[A-Za-z]+$` dans ce champ. |
| `uiAttributes.documentationLink` | Chaîne | Fait référence à la page de documentation du [Catalogue des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=fr#catalog) pour votre destination. Utilisez `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, où `YOURDESTINATION` est le nom de votre destination. Par exemple, pour une destination appelée Moviestar, procédez comme suit : `https://www.adobe.com/go/destinations-moviestar-en`. |
| `uiAttributes.category` | Chaîne | Fait référence à la catégorie affectée à votre destination dans Adobe Experience Platform. Pour plus d’informations, consultez la section [Catégories de destinations](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=fr#destination-categories). Utilisez l’une des valeurs suivantes :`adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Chaîne | `Server-to-server` est actuellement la seule option disponible. |
| `uiAttributes.frequency` | Chaîne | `Streaming` est actuellement la seule option disponible. |
| `identityNamespaces.externalId.acceptsAttributes` | Booléen | Indique si votre destination accepte les attributs de profil standard. En règle générale, ces attributs sont mis en évidence dans la documentation de nos partenaires. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booléen | Indique si les clients peuvent configurer des espaces de noms personnalisés dans votre destination. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Chaîne | _Non affiché dans l’exemple de configuration_. Utilisé, par exemple, lorsque le client [!DNL Platform] dispose d’adresses e-mail simples en tant qu’attribut et que votre plateforme accepte les e-mails hachés uniquement. C’est ici que vous devez fournir la transformation à appliquer (transformer l’adresse e-mail en minuscules, puis la hacher, par exemple). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Utilisé pour les cas où votre plateforme accepte des [espaces de noms d’identité standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#standard-namespaces) (IDFA, par exemple), afin que vous puissiez empêcher les utilisateurs Platform de sélectionner uniquement ces espaces de noms d’identité. <br> Lorsque vous utilisez `acceptedGlobalNamespaces`, vous pouvez employer `"requiredTransformation":"sha256(lower($))"` pour mettre en minuscules ou hacher des adresses e-mails ou des numéros de téléphone. |
| `destinationDelivery.authenticationRule` | Chaîne | Indique comment les clients [!DNL Platform] se connectent à votre destination. Les valeurs acceptées sont les suivantes : `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilisez `CUSTOMER_AUTHENTICATION` si les clients Platform se connectent à votre système par le biais d’un nom d’utilisateur et d’un mot de passe, d’un jeton porteur ou d’une autre méthode d’authentification. Par exemple, sélectionnez cette option si vous avez également sélectionné `authType: OAUTH2` ou `authType:BEARER` dans `customerAuthenticationConfigurations`. </li><li> Utilisez `PLATFORM_AUTHENTICATION` s’il existe un système d’authentification global entre Adobe et votre destination et que le client [!DNL Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer des informations d’identification à l’aide de la configuration des [Informations d’identification](./credentials-configuration-api.md). </li><li>Utilisez `NONE` si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `destinationDelivery.destinationServerId` | Chaîne | `instanceId` du [modèle de serveur de destination](./destination-server-api.md) utilisé pour cette destination. |
| `backfillHistoricalProfileData` | Booléen | Contrôle si les données de profil historiques sont exportées lorsque les segments sont activés vers la destination. <br> <ul><li> `true` : [!DNL Platform] envoie les profils utilisateur historiques qualifiés pour le segment avant l’activation du segment. </li><li> `false` : [!DNL Platform] inclut uniquement les profils utilisateurs qui remplissent les critères pour le segment une fois celui-ci activé. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est saisi par l’utilisateur. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est l’identifiant de segment Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est le nom du segment Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booléen | `instanceId` du [modèle de métadonnées d’audience](./audience-metadata-api.md) utilisé pour cette destination. |
| `schemaConfig.profileFields` | Tableau | Lorsque vous ajoutez des champs `profileFields` prédéfinis, comme illustré dans la configuration ci-dessus, les utilisateurs ont la possibilité de mapper les attributs Experience Platform aux attributs prédéfinis du côté de votre destination. |
| `schemaConfig.profileRequired` | Booléen | Utilisez `true` si les utilisateurs doivent être en mesure de mapper les attributs de profil d’Experience Platform aux attributs personnalisés du côté de votre destination, tel qu’indiqué dans l’exemple de configuration ci-dessus. |
| `schemaConfig.segmentRequired` | Booléen | Utilisez toujours `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booléen | Utilisez `true` si vous souhaitez que les utilisateurs puissent mapper des espaces de noms d’identité d’Experience Platform au schéma souhaité. |
| `aggregation.aggregationType` | - | Sélectionnez `BEST_EFFORT` ou `CONFIGURABLE_AGGREGATION`. L’exemple de configuration ci-dessus inclut l’agrégation `BEST_EFFORT`. Pour obtenir un exemple de `CONFIGURABLE_AGGREGATION`, consultez l’exemple de configuration dans le document [Configuration de destination](./destination-configuration.md#example-configuration). Les paramètres relatifs à l’agrégation configurable sont présentés ci-dessous dans le tableau. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Nombre entier | Experience Platform peut agréger plusieurs profils exportés en un seul appel HTTP. Indiquez le nombre maximal de profils que votre point d’entrée doit recevoir dans un seul appel HTTP. Notez qu’il s’agit d’une agrégation des meilleurs efforts. Par exemple, si vous spécifiez la valeur 100, Platform peut envoyer n’importe quel nombre de profils inférieur à 100 lors d’un appel. <br> Si votre serveur n’accepte pas plusieurs utilisateurs par demande, définissez cette valeur sur 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Booléen | Utilisez cet indicateur si l’appel à la destination doit être partagé par identité. Définissez cet indicateur sur `true` si votre serveur n’accepte qu’une seule identité par appel, pour un espace de noms donné. |
| `aggregation.configurableAggregation.splitUserById` | Booléen | Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Utilisez cet indicateur si l’appel à la destination doit être partagé par identité. Définissez cet indicateur sur `true` si votre serveur n’accepte qu’une seule identité par appel, pour un espace de noms donné. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Nombre entier | <ul><li>*Valeur minimale :1800*</li><li>*Valeur maximale : 3600*</li><li>Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Configurez une valeur comprise entre les valeurs minimales et maximales acceptées. Associé à `maxNumEventsInBatch`, ce paramètre détermine la durée pendant laquelle l’Experience Platform doit attendre d’envoyer un appel API à votre point de terminaison . <br> Par exemple, si vous utilisez la valeur maximale pour les deux paramètres, Experience Platform attend 3 600 secondes OU jusqu’à ce qu’il y ait 10 000 profils qualifiés avant d’effectuer l’appel API, selon ce qui se produit en premier. </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Nombre entier | <ul><li>*Valeur minimale :1000*</li><li>*Valeur maximale : 10 000*</li><li>Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Configurez une valeur comprise entre les valeurs minimales et maximales acceptées. Pour une description de ce paramètre, voir `maxBatchAgeInSecs` juste au-dessus.</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | Booléen | Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Permet d’agréger les profils exportés mappés à la destination en fonction des paramètres ci-dessous : <br> <ul><li>identifiant du segment</li><li> statut du segment </li><li> espace de noms d’identité </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Booléen | Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Définissez ce paramètre sur `true` si vous souhaitez regrouper les profils exportés vers votre destination par identifiant de segment. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Booléen | Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Vous devez définir à la fois `includeSegmentId:true` et `includeSegmentStatus:true` si vous souhaitez regrouper les profils exportés vers votre destination par identifiant de segment ET statut de segment. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Booléen | Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Définissez ce paramètre sur `true` si vous souhaitez regrouper les profils exportés vers votre destination par espace de noms d’identité. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booléen | Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Utilisez ce paramètre pour indiquer si vous souhaitez que les profils exportés soient agrégés en groupes d’une seule identité (GAID, IDFA, numéros de téléphone, e-mail, etc.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Chaîne | Consultez le paramètre dans l’exemple de configuration [ici](./destination-configuration.md#example-configuration). Créez des listes de groupes d’identités si vous souhaitez regrouper les profils exportés vers votre destination par groupes d’espaces de noms d’identité. Par exemple, vous pouvez combiner des profils contenant les identifiants mobiles IDFA et GAID dans un appel vers votre destination et des e-mails dans un autre en utilisant la configuration de l’exemple. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration de destination que vous venez de créer.

## Créer une configuration pour une destination basée sur des fichiers {#create-file-based}

Vous pouvez créer une configuration de destination en effectuant une requête POST au point d’entrée `/authoring/destinations`.

**Format d’API**

```http
POST /authoring/destinations
```

**Requête**

La requête suivante crée une configuration de destination basée sur des fichiers [!DNL Amazon S3], configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres des destinations basées sur des fichiers acceptés par le point d’entrée `/authoring/destinations`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

```json
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
            }
        ],
        "uiAttributes": {
            "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
            "category": "S3",
            "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
            "connectionType": "S3",
            "flowRunsSupported": true,
            "monitoringSupported": true,
            "frequency": "Batch"
        },
        "destinationDelivery": [
            {
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
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
                "ONCE",
                "EVERY_HOUR"
            ],
            "defaultFrequency":"DAILY",
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

Pour une description détaillée de tous les paramètres ci-dessus, consultez la [configuration de destination basée sur des fichiers](file-based-destination-configuration.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration de destination que vous venez de créer.

## Liste des configurations de destination {#retrieve-list}

Vous pouvez récupérer une liste de toutes les configurations de destination pour votre organisation IMS en effectuant une requête GET au point d’entrée `/authoring/destinations`.

**Format d’API**


```http
GET /authoring/destinations
```

**Requête**

La demande suivante récupère la liste des configurations de destination auxquelles vous avez accès, en fonction de la configuration de l’organisation IMS et de la sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse suivante renvoie un état HTTP 200 avec une liste des configurations de destination auxquelles vous avez accès, en fonction de l’identifiant d’organisation IMS et du nom de sandbox utilisés. Une valeur `instanceId` correspond au modèle d’une destination. La réponse est tronquée à des fins de brièveté.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
         "name":"Moviestar",
         "description":"Moviestar is a fictional destination, used for this example.",
         "status":"TEST",
         "customerAuthenticationConfigurations":[
            {
               "authType":"BEARER"
            }
         ],
         "customerDataFields":[
            {
               "name":"endpointsInstance",
               "type":"string",
               "title":"Select Endpoint",
               "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
               "isRequired":true,
               "enum":[
                  "US",
                  "EU",
                  "APAC",
                  "NZ"
               ]
            },
            {
               "name":"customerID",
               "type":"string",
               "title":"Moviestar Customer ID",
               "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
               "isRequired":true,
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
            },
            "another_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true
            }
         },
         "segmentMappingConfig":{
            "mapExperiencePlatformSegmentName":false,
            "mapExperiencePlatformSegmentId":false,
            "mapUserInput":false,
            "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
         },
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Paramètre | Type | Description |
|---------|----------|------|
| `name` | Chaîne | Indique le titre de votre destination dans le catalogue Experience Platform. |
| `description` | Chaîne | Fournissez une description qu’Adobe utilisera dans le catalogue des destinations Experience Platform pour votre carte de destination. N’utilisez pas plus de 4 à 5 phrases. |
| `status` | Chaîne | Indique le statut du cycle de vie de la carte de destination. Les valeurs acceptées sont `TEST`, `PUBLISHED` et `DELETED`. Utilisez `TEST` lorsque vous configurez votre destination pour la première fois. |
| `customerAuthenticationConfigurations` | Chaîne | Indique la configuration utilisée pour authentifier les clients Experience Platform sur votre serveur. Consultez `authType` ci-dessous pour les valeurs acceptées. |
| `customerAuthenticationConfigurations.authType` | Chaîne | Les valeurs acceptées sont les suivantes : `OAUTH2, BEARER`. |
| `customerDataFields.name` | Chaîne | Attribuez un nom au champ personnalisé que vous introduisez. |
| `customerDataFields.type` | Chaîne | Indique le type de champ personnalisé que vous introduisez. Les valeurs acceptées sont `string`, `object` et `integer`. |
| `customerDataFields.title` | Chaîne | Indique le nom du champ, tel qu’il est affiché par les clients dans l’interface utilisateur d’Experience Platform. |
| `customerDataFields.description` | Chaîne | Fournissez une description du champ personnalisé. |
| `customerDataFields.isRequired` | Booléen | Indique si ce champ est requis dans le workflow de configuration de destination. |
| `customerDataFields.enum` | Chaîne | Rend le champ personnalisé sous forme de menu déroulant et répertorie les options disponibles pour l’utilisateur. |
| `customerDataFields.pattern` | Chaîne | Impose un modèle pour le champ personnalisé, le cas échéant. Utilisez des expressions régulières pour appliquer un modèle. Par exemple, si vos identifiants de client n’incluent pas de chiffres ou de traits de soulignement, saisissez `^[A-Za-z]+$` dans ce champ. |
| `uiAttributes.documentationLink` | Chaîne | Fait référence à la page de documentation du [Catalogue des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) pour votre destination. Utilisez `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, où `YOURDESTINATION` est le nom de votre destination. Par exemple, pour une destination appelée Moviestar, procédez comme suit : `https://www.adobe.com/go/destinations-moviestar-en` |
| `uiAttributes.category` | Chaîne | Fait référence à la catégorie affectée à votre destination dans Adobe Experience Platform. Pour plus d’informations, consultez la section [Catégories de destinations](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Utilisez l’une des valeurs suivantes : `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Chaîne | `Server-to-server` est actuellement la seule option disponible. |
| `uiAttributes.frequency` | Chaîne | `Streaming` est actuellement la seule option disponible. |
| `identityNamespaces.externalId.acceptsAttributes` | Booléen | Indique si votre destination accepte les attributs de profil standard. En règle générale, ces attributs sont mis en évidence dans la documentation de nos partenaires. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booléen | Indique si les clients peuvent configurer des espaces de noms personnalisés dans votre destination. Apprenez-en plus sur les [Espaces de noms personnalisés](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#manage-namespaces) dans Adobe Experience Platform. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Chaîne | _Non affiché dans l’exemple de configuration_. Utilisé, par exemple, lorsque le client [!DNL Platform] dispose d’adresses e-mail simples en tant qu’attribut et que votre plateforme accepte les e-mails hachés uniquement. C’est ici que vous devez fournir la transformation à appliquer (transformer l’adresse e-mail en minuscules, puis la hacher, par exemple). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Utilisé dans les cas où votre plateforme accepte les [espaces de noms d’identité standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (par exemple, IDFA), afin que vous puissiez empêcher les utilisateurs Platform de sélectionner uniquement ces espaces de noms d’identité. |
| `destinationDelivery.authenticationRule` | Chaîne | Indique comment les clients [!DNL Platform] se connectent à votre destination. Les valeurs acceptées sont les suivantes : `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilisez `CUSTOMER_AUTHENTICATION` si les clients Platform se connectent à votre système par le biais d’un nom d’utilisateur et d’un mot de passe, d’un jeton porteur ou d’une autre méthode d’authentification. Par exemple, sélectionnez cette option si vous avez également sélectionné `authType: OAUTH2` ou `authType:BEARER` dans `customerAuthenticationConfigurations`. </li><li> Utilisez `PLATFORM_AUTHENTICATION` s’il existe un système d’authentification global entre Adobe et votre destination et que le client [!DNL Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer des informations d’identification à l’aide de la configuration des [Informations d’identification](./authentication-configuration.md). </li><li>Utilisez `NONE` si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `destinationDelivery.destinationServerId` | Chaîne | `instanceId` du [modèle de serveur de destination](./destination-server-api.md) utilisé pour cette destination. |
| `destConfigId` | Chaîne | Ce champ est généré automatiquement, vous ne devez pas le renseigner. |
| `backfillHistoricalProfileData` | Booléen | Contrôle si les données de profil historiques sont exportées lorsque les segments sont activés vers la destination. <br> <ul><li> `true` : [!DNL Platform] envoie les profils utilisateur historiques qualifiés pour le segment avant l’activation du segment. </li><li> `false` : [!DNL Platform] inclut uniquement les profils utilisateurs qui remplissent les critères pour le segment une fois celui-ci activé. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est saisi par l’utilisateur. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est l’identifiant de segment Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est le nom du segment Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booléen | Paramètre `instanceId` du [modèle de métadonnées d’audience](./audience-metadata-management.md) utilisé pour cette destination. Pour configurer un modèle de métadonnées d’audience, lisez [Référence de l’API de métadonnées d’audience](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Mettre à jour une configuration de destination existante {#update}

Vous pouvez mettre à jour une configuration de destination existante en adressant une requête PUT au point d’entrée `/authoring/destinations` en fournissant l’identifiant d’instance de la configuration de destination que vous souhaitez mettre à jour. Dans le corps de l’appel, fournissez la configuration de destination mise à jour.

**Format d’API**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration de destination à mettre à jour. |

**Requête**

La requête suivante met à jour une configuration de destination existante, configurée selon les paramètres fournis dans la payload. Dans l’exemple d’appel ci-dessous, nous mettons à jour la configuration [créée précédemment](./destination-configuration-api.md#create) pour quʼelle accepte désormais les identifiants GAID, IDFA et les identifiants d’e-mails hachés comme espaces de noms d’identité.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## Récupérer une configuration de destination spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une configuration de destination spécifique en envoyant une requête GET au point d’entrée `/authoring/destinations` et en fournissant l’identifiant d’instance de la configuration de destination que vous souhaitez récupérer.

**Format d’API**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration de destination à récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la configuration de destination spécifiée.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## Supprimer une configuration de destination spécifique {#delete}

Vous pouvez supprimer une configuration de destination spécifique en effectuant une requête DELETE vers le point d’entrée `/authoring/destinations` et en fournissant l’identifiant de la configuration de destination que vous souhaitez supprimer du chemin d’accès de la requête.

**Format d’API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | Valeur `id` de la configuration de destination à supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment configurer votre destination à l’aide du point d’entrée de l’API `/authoring/destinations`. Consultez la section [Comment utiliser Destination SDK pour configurer votre destination](./configure-destination-instructions.md) pour comprendre où cette étape s’inscrit dans le processus de configuration de votre destination.
