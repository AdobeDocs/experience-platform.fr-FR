---
description: Cette configuration vous permet d’indiquer des informations de base telles que votre nom de destination, votre catégorie, votre description, votre logo, etc. Les paramètres de cette configuration déterminent également comment les utilisateurs d’Experience Platform s’authentifient pour votre destination, comment ils apparaissent dans l’interface utilisateur d’Experience Platform ainsi que les identités qui peuvent être exportées vers votre destination.
title: (Version Beta) Options de configuration de destinations basées sur des fichiers pour Destination SDK
source-git-commit: 5186e90b850f1e75ec358fa01bfb8a5edac29277
workflow-type: ht
source-wordcount: '1899'
ht-degree: 100%

---

# (Version Beta) Configuration de destinations basées sur des fichiers {#destination-configuration}

## Présentation {#overview}

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers dans Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Cette configuration vous permet d’indiquer les informations essentielles pour votre destination basée sur des fichiers, telles que votre nom de destination, votre catégorie, votre description, etc. Les paramètres de cette configuration déterminent également comment les utilisateurs d’Experience Platform s’authentifient pour votre destination, comment ils apparaissent dans l’interface utilisateur d’Experience Platform ainsi que les identités qui peuvent être exportées vers votre destination.

Cette configuration connecte également les autres configurations requises pour que votre destination fonctionne (métadonnées de serveur de destination et d’audience) à celle-ci. Découvrez comment vous pouvez référencer les deux configurations dans une [section ci-dessous](./destination-configuration.md#connecting-all-configurations).

Vous pouvez configurer la fonctionnalité décrite dans ce document à l’aide du point d’entrée de l’API `/authoring/destinations`. Consultez [Opérations de point d’entrée de l’API Destinations](./destination-configuration-api.md) pour obtenir une liste complète des opérations que vous pouvez effectuer sur le point d’entrée.

## Exemple de configuration de destination Amazon S3 {#batch-example-configuration}

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes": "2000",
   "maxIdentityAttributes": "10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
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
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
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
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
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
         "title":"header",
         "description":"Writes the names of columns as the first line.",
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
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
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
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
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
   "identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
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
              "name":"phoneNo",
              "title":"phoneNo",
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
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowJoinKeyFieldSelection":true,
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
         "ONCE",
         "EVERY_HOUR"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00"
   },
   "backfillHistoricalProfileData":true
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `name` | Chaîne | Indique le titre de votre destination dans le catalogue Experience Platform. |
| `description` | Chaîne | Fournissez une description de votre carte de destination dans le catalogue des destinations Experience Platform. N’utilisez pas plus de 4 à 5 phrases. |
| `status` | Chaîne | Indique le statut du cycle de vie de la carte de destination. Les valeurs acceptées sont `TEST`, `PUBLISHED` et `DELETED`. Utilisez `TEST` lorsque vous configurez votre destination pour la première fois. |
| `maxProfileAttributes` | Chaîne | Indique le nombre maximal d’attributs de profil que les clients peuvent exporter vers la destination. La valeur par défaut est `2000`. |
| `maxIdentityAttributes` | Chaîne | Indique le nombre maximal d’espaces de noms d’identité que les clients peuvent exporter vers la destination. La valeur par défaut est `10`. |

{style=&quot;table-layout:auto&quot;}

## Configurations de l’authentification du client {#customer-authentication-configurations}

Cette section de la configuration des destinations génère la page [Configurer une nouvelle destination](/help/destinations/ui/connect-destination.md) dans l’interface utilisateur d’Experience Platform, où les utilisateurs connectent Experience Platform aux comptes qu’ils possèdent avec votre destination.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

Selon l’[option d’authentification](authentication-configuration.md##supported-authentication-types) que vous indiquez dans le champ `authType`, la page Experience Platform est générée pour les utilisateurs comme suit :

### Authentification Amazon S3

Lorsque vous configurez le type d’authentification Amazon S3, les utilisateurs doivent saisir les informations d’identification S3.

![Rendu de l’interface utilisateur avec authentification S3](assets/s3-authentication-ui.png)

### Authentification Azure Blob  {#blob}

Lorsque vous configurez le type d’authentification Azure Blob, les utilisateurs doivent saisir la chaîne de connexion.

![Rendu de l’interface utilisateur avec authentification Blob](assets/blob-authentication-ui.png)

### SFTP avec authentification par mot de passe

Lorsque vous configurez le SFTP avec le type d’authentification par mot de passe, les utilisateurs doivent saisir le nom d’utilisateur et le mot de passe SFTP, ainsi que le domaine et le port SFTP (le port par défaut est 22).

![Rendu de l’interface utilisateur avec authentification par mot de passe](assets/sftp-password-authentication-ui.png)

### SFTP avec authentification par clé SSH

Lorsque vous configurez le SFTP avec le type d’authentification par clé SSH, les utilisateurs doivent saisir le nom d’utilisateur SFTP et la clé SSH, ainsi que le domaine et le port SFTP (le port par défaut est 22).

![Rendu de l’interface utilisateur avec SFTP avec authentification par clé SSH](assets/sftp-key-authentication-ui.png)

## Champs de données client {#customer-data-fields}

Utilisez cette section pour demander aux utilisateurs de renseigner des champs personnalisés, spécifiques à votre destination, lors de la connexion à la destination dans l’interface utilisateur d’Experience Platform.

Dans l’exemple ci-dessous, `customerDataFields` exige des utilisateurs qu’ils saisissent un nom pour leur destination et qu’ils fournissent un nom de compartiment [!DNL Amazon S3] et un chemin d’accès au dossier, ainsi qu’un type de compression et un format de fichier.

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
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
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
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
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
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
         "title":"header",
         "description":"Writes the names of columns as the first line.",
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
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
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
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
```

| Paramètre | Type | Description |
|---------|----------|------|
| `name` | Chaîne | Attribuez un nom au champ personnalisé que vous introduisez. |
| `title` | Chaîne | Indique le nom du champ tel qu’il est affiché par les clients dans l’interface utilisateur d’Experience Platform. |
| `description` | Chaîne | Fournissez une description du champ personnalisé. |
| `type` | Chaîne | Indique le type de champ personnalisé que vous introduisez. Les valeurs acceptées sont `string`, `object` et `integer`. |
| `isRequired` | Booléen | Indique si ce champ est requis dans le workflow de configuration de destination. |
| `pattern` | Chaîne | Impose un modèle pour le champ personnalisé, le cas échéant. Utilisez des expressions régulières pour appliquer un modèle. Par exemple, si vos identifiants de client n’incluent pas de chiffres ou de traits de soulignement, saisissez `^[A-Za-z]+$` dans ce champ. |
| `enum` | Chaîne | Rend le champ personnalisé sous forme de menu déroulant et répertorie les options disponibles pour l’utilisateur. |
| `default` | Chaîne | Définit la valeur par défaut d’une liste `enum`. |

{style=&quot;table-layout:auto&quot;}

## Attributs de l’interface utilisateur {#ui-attributes}

Cette section fait référence aux éléments de l’interface utilisateur dans la configuration ci-dessus qu’Adobe doit utiliser pour votre destination dans l’interface utilisateur d’Adobe Experience Platform.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Paramètre | Type | Description |
|---------|----------|------|
| `documentationLink` | Chaîne | Fait référence à la page de documentation du [catalogue des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=fr#catalog) pour votre destination. Utilisez `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, où `YOURDESTINATION` est le nom de votre destination. Pour une destination appelée Moviestar, cela donne `http://www.adobe.com/go/destinations-moviestar-en`. |
| `category` | Chaîne | Fait référence à la catégorie affectée à votre destination dans Adobe Experience Platform. Pour plus d’informations, reportez-vous à la section [Catégories de destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=fr). Utilisez l’une des valeurs suivantes : `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Chaîne | URL dans laquelle vous avez hébergé l’icône à afficher dans la carte du catalogue des destinations. |
| `connectionType` | Chaîne | Type de connexion en fonction de la destination. Valeurs prises en charge : <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Booléen | Indique si la connexion de destination est incluse dans l’[interface utilisateur d’exécution de flux](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Lorsque vous définissez ce paramètre sur `true` : <ul><li>La **[!UICONTROL date d’exécution du dernier flux de données]** et **[!UICONTROL le statut d’exécution du dernier flux de données]** s’affichent dans la page de navigation de destination.</li><li>Les onglets **[!UICONTROL Exécution du flux de données]** et **[!UICONTROL Données d’activation]** s’affichent dans la page d’affichage de destination.</li></ul> |
| `monitoringSupported` | Booléen | Indique si la connexion de destination est incluse dans la [surveillance de l’interface utilisateur](../ui/destinations-workspace.md#browse). Lorsque vous définissez ce paramètre sur `true`, l’option **[!UICONTROL Afficher dans la surveillance]** s’affiche sur la page de navigation de destination. |
| `frequency` | Chaîne | Fait référence au type d’exportation des données pris en charge par la destination. Définissez sur `Batch` pour les destinations basées sur des fichiers. |

{style=&quot;table-layout:auto&quot;}

## Diffusion de destination {#destination-delivery}

```json
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
   ]
```

| Paramètre | Type | Description |
|---------|----------|------|
| `authenticationRule` | Chaîne | Indique comment les clients [!DNL Platform] se connectent à votre destination. Les valeurs acceptées sont les suivantes : `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION` ou `NONE`. <br> <ul><li>Utilisez `CUSTOMER_AUTHENTICATION` si les clients Platform se connectent à votre système par l’une des méthodes suivantes : <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Utilisez `PLATFORM_AUTHENTICATION` s’il existe un système d’authentification global entre Adobe et votre destination et que le client [!DNL Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide de la configuration des [Informations d’identification](./credentials-configuration-api.md). </li><li>Utilisez `NONE` si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `destinationServerId` | Chaîne | `instanceId` de la [configuration du serveur de destination](./destination-server-api.md) utilisée pour cette destination. |

{style=&quot;table-layout:auto&quot;}

## Configuration du mappage de segments {#segment-mapping}

Cette section de la configuration de destination concerne la manière dont les métadonnées de segment telles que les noms ou les identifiants doivent être partagées entre Experience Platform et votre destination.

Par le biais du paramètre `audienceTemplateId`, cette section associe également cette configuration à la [configuration des métadonnées d’audience](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| Paramètre | Type | Description |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est le nom du segment Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est l’identifiant de segment Experience Platform. |
| `mapUserInput` | Booléen | Contrôle si l’identifiant de mappage de segments dans le workflow d’activation de destination est saisi par l’utilisateur. |
| `audienceTemplateId` | Booléen | Paramètre `instanceId` du [modèle de métadonnées d’audience](./audience-metadata-management.md) utilisé pour cette destination. Pour configurer un modèle de métadonnées d’audience, consultez la [référence de l’API de métadonnées d’audience](./audience-metadata-api.md). |

## Configuration du schéma dans l’étape de mappage {#schema-configuration}

Utilisez les paramètres de la section `schemaConfig` pour activer l’étape de mappage du processus d’activation de destination. En utilisant les paramètres décrits ci-dessous, vous pouvez déterminer si les utilisateurs d’Experience Platform peuvent mapper des attributs de profil et/ou des identités à votre destination basée sur des fichiers.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
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
```

| Paramètre | Type | Description |
|---------|----------|------|
| `profileFields` | Tableau | Lorsque vous ajoutez des champs `profileFields` prédéfinis, les utilisateurs Experience Platform ont la possibilité de mapper les attributs Platform aux attributs prédéfinis de votre destination. |
| `profileRequired` | Booléen | Utilisez `true` si les utilisateurs doivent être en mesure de mapper les attributs de profil d’Experience Platform aux attributs personnalisés du côté de votre destination, comme illustré dans l’exemple de configuration ci-dessus. |
| `segmentRequired` | Booléen | Utilisez toujours `segmentRequired:true`. |
| `identityRequired` | Booléen | Utilisez `true` si les utilisateurs doivent être en mesure de mapper des espaces de noms d’identité d’Experience Platform à votre schéma souhaité. |

{style=&quot;table-layout:auto&quot;}

### Configuration de schéma dynamique dans l’étape de mappage {#dynamic-schema-configuration}

Adobe Experience Platform Destination SDK prend en charge les schémas définis par les partenaires. Un schéma défini par un partenaire permet aux utilisateurs de mapper des attributs de profil et des identités à des schémas personnalisés définis par les partenaires de destination, comme le fait le processus de [destinations de diffusion en continu](destination-configuration.md#schema-configuration).

Utilisez les paramètres de la section `dynamicSchemaConfig` pour définir votre propre schéma auquel les attributs de profil Platform et/ou les identités peuvent être mappés.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `profileRequired` | Booléen | Utilisez `true` si les utilisateurs doivent être en mesure de mapper les attributs de profil d’Experience Platform aux attributs personnalisés du côté de votre destination, comme illustré dans l’exemple de configuration ci-dessus. |
| `segmentRequired` | Booléen | Utilisez `segmentRequired:true`. |
| `identityRequired` | Booléen | Utilisez `true` si les utilisateurs doivent être en mesure de mapper des espaces de noms d’identité Experience Platform à votre schéma souhaité. |
| `destinationServerId` | Chaîne | Valeur `instanceId` de la [configuration du serveur de destination](./destination-server-api.md) utilisée pour cette destination. |
| `authenticationRule` | Chaîne | Indique comment les clients [!DNL Platform] se connectent à votre destination. Les valeurs acceptées sont les suivantes : `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION` ou `NONE`. <br> <ul><li>Utilisez `CUSTOMER_AUTHENTICATION` si les clients Platform se connectent à votre système par l’une des méthodes suivantes : <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Utilisez `PLATFORM_AUTHENTICATION` s’il existe un système d’authentification global entre Adobe et votre destination et que le client [!DNL Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide de la configuration des [Informations d’identification](./credentials-configuration-api.md). </li><li>Utilisez `NONE` si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `value` | Chaîne | Nom du schéma à afficher dans l’interface utilisateur d’Experience Platform, à l’étape de mappage. |
| `responseFormat` | Chaîne | Toujours définie sur `SCHEMA` lors de la définition d’un schéma personnalisé. |

{style=&quot;table-layout:auto&quot;}

## Identités et attributs {#identities-and-attributes}

Les paramètres de cette section déterminent les identités acceptées par votre destination. Cette configuration renseigne également les identités et les attributs cibles à l’[étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) de l’interface utilisateur d’Experience Platform, où les utilisateurs mappent les identités et les attributs de leurs schémas XDM au schéma de votre destination.


```json
"identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

Vous devez indiquer les identités [!DNL Platform] que les clients peuvent exporter vers votre destination. Voici quelques exemples : [!DNL Experience Cloud ID], e-mail haché, identifiant d’appareil ([!DNL IDFA], [!DNL GAID]). Ces valeurs sont les suivantes : [!DNL Platform] espaces de noms d’identité que les clients peuvent mapper aux espaces de noms d’identité de votre destination. Vous pouvez également indiquer si les clients peuvent mapper des espaces de noms personnalisés à des identités prises en charge par votre destination.

Les espaces de noms d’identité ne nécessitent pas de correspondance 1-1 entre [!DNL Platform] et votre destination.
Par exemple, les clients peuvent mapper un espace de noms [!DNL Platform] [!DNL IDFA] à un espace de noms [!DNL IDFA] de votre destination ou mapper le même espace de noms [!DNL Platform] [!DNL IDFA] à un espace de noms [!DNL Customer ID] de votre destination.

## Configuration par lots {#batch-configuration}

Cette section fait référence aux paramètres d’exportation de fichiers dans la configuration ci-dessus qu’Adobe doit utiliser pour votre destination dans l’interface utilisateur d’Adobe Experience Platform.

```json
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
         "ONCE",
         "EVERY_HOUR"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00"
   }
```

| Paramètre | Type | Description |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booléen | Définissez cette valeur sur `true` afin de permettre aux clients de spécifier les attributs de profil obligatoires. La valeur par défaut est `false`. Pour plus d’informations, consultez la section [Attributs obligatoires](../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `allowDedupeKeyFieldSelection` | Booléen | Définissez cette valeur sur `true` afin de permettre aux clients de spécifier des clés de déduplication. La valeur par défaut est `false`. Pour plus d’informations, consultez la section [Clés de déduplication](../ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `defaultExportMode` | Énumération | Définit le mode d’exportation de fichier par défaut. Valeurs prises en charge :<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul><br> La valeur par défaut est `DAILY_FULL_EXPORT`. Pour plus d’informations sur la planification des exportations de fichiers, consultez la [documentation sur l’activation par lots](../ui/activate-batch-profile-destinations.md#scheduling). |
| `allowedExportModes` | Liste | Définit les modes d’exportation de fichiers disponibles pour les clients. Valeurs prises en charge :<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Liste | Définit la fréquence d’exportation des fichiers disponible pour les clients. Valeurs prises en charge :<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Énumération | Définit la fréquence d’exportation des fichiers par défaut. Les valeurs prises en charge sont les suivantes :<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> <br> La valeur par défaut est `DAILY`. |
| `defaultStartTime` | Chaîne | Définit l’heure de début par défaut de l’exportation du fichier. Utilise le format de fichier de 24 heures. La valeur par défaut est « 00:00 ». |

## Qualifications des profils historiques {#profile-backfill}

Vous pouvez utiliser le paramètre `backfillHistoricalProfileData` dans la configuration des destinations pour déterminer si les qualifications des profils historiques doivent être exportées vers votre destination.

```json
   "backfillHistoricalProfileData":true
```

| Paramètre | Type | Description |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booléen | Contrôle si les données de profil historiques sont exportées lorsque les segments sont activés vers la destination. <br> <ul><li> `true` : [!DNL Platform] envoie les profils utilisateur historiques qualifiés pour le segment avant l’activation du segment. </li><li> `false` : [!DNL Platform] inclut uniquement les profils utilisateur qui remplissent les critères pour le segment une fois le segment activé. </li></ul> |

## Comment cette configuration connecte toutes les informations nécessaires à votre destination {#connecting-all-configurations}

Certains de vos paramètres de destination doivent être configurés via le [serveur de destination](./server-and-file-configuration.md) ou la [configuration des métadonnées d’audience](./audience-metadata-management.md). La configuration de destination décrite ici connecte tous ces paramètres en référençant les deux autres configurations comme suit :

* Utilisez la variable `destinationServerId` pour référencer le serveur de destination et la configuration du modèle définis pour votre destination.
* Utilisez la variable `audienceMetadataId` pour référencer la configuration des métadonnées d’audience définie pour votre destination.
