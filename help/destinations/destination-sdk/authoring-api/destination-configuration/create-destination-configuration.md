---
description: Découvrez comment structurer un appel API pour créer une configuration de destination avec Adobe Experience Platform Destination SDK.
title: Création d’une configuration de destination
exl-id: aae4aaa8-1dd0-4041-a86c-5c86f04d7d13
source-git-commit: 20cb2dbfbfc8e73c765073818c8e7e561d4e6629
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 99%

---

# Création d’une configuration de destination

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour créer votre propre configuration de destination à l’aide du point d’entrée de l’API `/authoring/destinations`.

Pour obtenir une description détaillée des fonctionnalités configurables avec ce point d’entrée, consultez les articles suivants :

* [Configuration de l’authentification du client](../../functionality/destination-configuration/customer-authentication.md)
* [Autorisation OAuth2](../../functionality/destination-configuration/oauth2-authorization.md)
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
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations dʼAPI de configuration de destinations {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Création d’une configuration de destination {#create}

Vous pouvez créer une configuration de destination en effectuant une requête POST au point d’entrée `/authoring/destinations`.

>[!TIP]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations`

**Format d’API**

```http
POST /authoring/destinations
```

La requête suivante crée une configuration de destination [!DNL Amazon S3], configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres des destinations basées sur des fichiers acceptés par le point d’entrée `/authoring/destinations`.

Notez que vous n’avez pas à ajouter tous les paramètres à l’appel API et que la payload est personnalisable, conformément aux exigences de votre API.

+++Requête

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
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
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

| Paramètre | Type | Description |
|---------|----------|------|
| `name` | Chaîne | Indique le titre de la destination dans le catalogue Experience Platform. |
| `description` | Chaîne | Fournissez une description qu’Adobe utilisera dans le catalogue des destinations Experience Platform pour votre carte de destination. N’utilisez pas plus de 4 à 5 phrases. ![Image de l’interface utilisateur de Platform montrant la description de la destination.](../../assets/authoring-api/destination-configuration/destination-description.png "Description de la destination"){width="100" zoomable="yes"} |
| `status` | Chaîne | Indique le statut du cycle de vie de la carte de destination. Les valeurs acceptées sont `TEST`, `PUBLISHED` et `DELETED`. Utilisez `TEST` lorsque vous configurez votre destination pour la première fois. |
| `customerAuthenticationConfigurations.authType` | Chaîne | Indique la configuration utilisée pour authentifier la clientèle d’Experience Platform sur votre serveur de destination. Pour en savoir plus sur les types d’authentification pris en charge, consultez la [configuration de l’authentification du client](../../functionality/destination-configuration/customer-authentication.md). |
| `customerDataFields.name` | Chaîne | Attribuez un nom au champ personnalisé que vous introduisez. <br/><br/> Pour en savoir plus sur les types d’authentification pris en charge, consultez les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md). ![Image de l’interface utilisateur de Platform montrant les champs de données client.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "Champs de données client"){width="100" zoomable="yes"} |
| `customerDataFields.type` | Chaîne | Indique le type de champ personnalisé que vous introduisez. Les valeurs acceptées sont les suivantes : `string`, `object` ou `integer`. <br/><br/> Pour en savoir plus sur les types d’authentification pris en charge, consultez les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.title` | Chaîne | Indique le nom du champ tel qu’il est affiché par les clients dans l’interface utilisateur d’Experience Platform. <br/><br/> Pour en savoir plus sur les types d’authentification pris en charge, consultez les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.description` | Chaîne | Fournissez une description du champ personnalisé. Pour en savoir plus sur ces paramètres, consultez les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.isRequired` | Booléen | Indique si ce champ est obligatoire dans le workflow de configuration de destination. <br/><br/> Pour en savoir plus sur les types d’authentification pris en charge, consultez les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.enum` | Chaîne | Rend le champ personnalisé sous forme de menu déroulant et répertorie les options disponibles pour l’utilisateur. <br/><br/> Pour en savoir plus sur les types d’authentification pris en charge, consultez les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.default` | Chaîne | Définit la valeur par défaut d’une liste `enum`. |
| `customerDataFields.pattern` | Chaîne | Impose un modèle pour le champ personnalisé, le cas échéant. Utilisez des expressions régulières pour appliquer un modèle. Par exemple, si vos identifiants de client n’incluent pas de chiffres ou de traits de soulignement, saisissez `^[A-Za-z]+$` dans ce champ. <br/><br/> Pour en savoir plus sur les types d’authentification pris en charge, consultez les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md). |
| `uiAttributes.documentationLink` | Chaîne | Fait référence à la page de documentation du [Catalogue des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html#catalog) pour votre destination. Utilisez `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, où `YOURDESTINATION` est le nom de votre destination. Par exemple, pour une destination appelée Moviestar, vous utiliseriez `https://www.adobe.com/go/destinations-moviestar-en`. Notez que ce lien ne fonctionne qu’une fois la destination mise en ligne par Adobe et la documentation publiée. <br/><br/> Pour en savoir plus sur ces paramètres, consultez les [attributs de l’interface utilisateur](../../functionality/destination-configuration/ui-attributes.md). ![Image de l’interface utilisateur de Platform montrant le lien vers la documentation.](../../assets/authoring-api/destination-configuration/documentation-url.png "URL de documentation"){width="100" zoomable="yes"} |
| `uiAttributes.category` | Chaîne | Fait référence à la catégorie affectée à votre destination dans Adobe Experience Platform. Pour plus d’informations, consultez la section [Catégories de destinations](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html#destination-categories). Utilisez l’une des valeurs suivantes : `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> Pour en savoir plus sur ces paramètres, consultez les [attributs de l’interface utilisateur](../../functionality/destination-configuration/ui-attributes.md). |
| `uiAttributes.connectionType` | Chaîne | Type de connexion en fonction de la destination. Valeurs prises en charge : <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | Chaîne | Fait référence au type d’exportation des données pris en charge par la destination. Définissez-le sur `Streaming` quand les intégrations sont basées sur des API, ou sur `Batch` lorsque vous exportez des fichiers vers les destinations. |
| `identityNamespaces.externalId.acceptsAttributes` | Booléen | Indique si la clientèle peut mapper des attributs de profil standard à l’identité que vous configurez. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booléen | Indique s’il est possible de mapper des identités appartenant à des [espaces de noms personnalisés](/help/identity-service/features/namespaces.md#manage-namespaces) à l’identité que vous êtes en train de configurer. |
| `identityNamespaces.externalId.transformation` | Chaîne | _Non affiché dans l’exemple de configuration_. Utilisé, par exemple, lorsque le client [!DNL Platform] dispose d’adresses e-mail simples en tant qu’attribut et que votre plateforme accepte les e-mails hachés uniquement. C’est ici que vous devez fournir la transformation à appliquer (transformer l’adresse e-mail en minuscules, puis la hacher, par exemple). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Indique quels [espaces de noms d’identité standard](/help/identity-service/features/namespaces.md#standard) (par exemple, IDFA) la clientèle peut mapper à l’identité que vous configurez. <br> Lorsque vous utilisez `acceptedGlobalNamespaces`, vous pouvez employer `"requiredTransformation":"sha256(lower($))"` pour mettre en minuscules ou hacher des adresses e-mails ou des numéros de téléphone. |
| `destinationDelivery.authenticationRule` | Chaîne | Indique comment la clientèle [!DNL Platform] se connecte à votre destination. Les valeurs acceptées sont les suivantes : `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilisez `CUSTOMER_AUTHENTICATION` si les clients Platform se connectent à votre système par le biais d’un nom d’utilisateur et d’un mot de passe, d’un jeton porteur ou d’une autre méthode d’authentification. Par exemple, sélectionnez cette option si vous avez également sélectionné `authType: OAUTH2` ou `authType:BEARER` dans `customerAuthenticationConfigurations`. </li><li> Utilisez `PLATFORM_AUTHENTICATION` s’il existe un système d’authentification global entre Adobe et votre destination et que la clientèle [!DNL Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer des informations d’identification à l’aide de la configuration des [informations d’identification API](../../credentials-api/create-credential-configuration.md). </li><li>Utilisez `NONE` si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `destinationDelivery.destinationServerId` | Chaîne | `instanceId` du [modèle de serveur de destination](../destination-server/create-destination-server.md) utilisé pour cette destination. |
| `backfillHistoricalProfileData` | Booléen | Contrôle si les données de profil historiques sont exportées quand les audiences sont activées vers la destination. Définissez toujours ce paramètre sur `true`. |
| `segmentMappingConfig.mapUserInput` | Booléen | Contrôle si l’identifiant de mappage d’audiences dans le workflow d’activation de destination est saisi par l’utilisateur ou l’utilisatrice. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booléen | Contrôle si l’identifiant de mappage d’audience dans le workflow d’activation de destination est l’identifiant d’audience Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booléen | Contrôle si l’identifiant de mappage d’audiences dans le workflow d’activation de destination est le nom de l’audience Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Chaîne | `instanceId` du [modèle de métadonnées d’audience](../../metadata-api/create-audience-template.md) utilisé pour cette destination. |
| `schemaConfig.profileFields` | Tableau | Lorsque vous ajoutez des champs `profileFields` prédéfinis, comme illustré dans la configuration ci-dessus, les utilisateurs ont la possibilité de mapper les attributs Experience Platform aux attributs prédéfinis du côté de votre destination. |
| `schemaConfig.profileRequired` | Booléen | Utilisez `true` si les utilisateurs doivent être en mesure de mapper les attributs de profil d’Experience Platform aux attributs personnalisés du côté de votre destination, comme indiqué dans l’exemple de configuration ci-dessus. |
| `schemaConfig.segmentRequired` | Booléen | Utilisez toujours `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booléen | Utilisez `true` si vous souhaitez que les utilisateurs puissent mapper des espaces de noms d’identité d’Experience Platform au schéma souhaité. |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration de destination que vous venez de créer.

+++

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment créer une configuration de destination avec le point d’entrée `/authoring/destinations` Destination SDK de l’API.

Pour en savoir plus sur les fonctionnalités offertes par ce point d’entrée, consultez les articles suivants :

* [Récupération d’une configuration de destination](retrieve-destination-configuration.md)
* [Mise à jour d’une configuration de destination](update-destination-configuration.md)
* [Suppression d’une configuration de destination](delete-destination-configuration.md)

Pour comprendre la place de ce point d’entrée dans le processus de création de destinations, consultez les articles suivants :

* [Utiliser Destination SDK pour configurer une destination de diffusion en streaming](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
