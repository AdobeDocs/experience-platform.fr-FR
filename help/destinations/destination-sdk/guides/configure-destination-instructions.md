---
description: Cette page répertorie et décrit les étapes de configuration d’une destination de diffusion en continu à l’aide de Destination SDK.
title: Utiliser Destination SDK pour configurer une destination de diffusion en continu
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 57%

---

# Utiliser Destination SDK pour configurer une destination de diffusion en continu

## Présentation {#overview}

Cette page décrit comment utiliser les informations dans la section [Options de configuration de Destination SDK](../functionality/configuration-options.md) et dans d’autres documents de référence sur les fonctionnalités et l’API Destination SDK pour configurer une [destination de diffusion en continu](../../destination-types.md#streaming-destinations). Les étapes sont présentées dans l’ordre séquentiel ci-dessous.

## Conditions préalables {#prerequisites}

Avant de passer aux étapes illustrées ci-dessous, veuillez lire la page de prise en main de Destination SDK [&#128279;](../getting-started.md) pour plus d’informations sur l’obtention des informations d’authentification Adobe I/O nécessaires et d’autres conditions préalables pour travailler avec les API Destination SDK. Cela suppose que vous ayez rempli les conditions préalables de partenariat et d’autorisation et que vous soyez prêt à commencer à développer votre destination.

## Étapes à suivre pour utiliser les options de configuration de Destination SDK afin de configurer votre destination. {#steps}

![Étapes illustrées d’utilisation des points d’entrée de Destination SDK](../assets/guides/destination-sdk-steps.png)

## Étape 1 : créer une configuration de serveur et de modèle {#create-server-template-configuration}

Commencez par [créer une configuration de serveur et de modèle](../authoring-api/destination-server/create-destination-server.md) à l’aide du point d’entrée `/destinations-server`.

Retrouvez ci-dessous un exemple de configuration. Notez que le modèle de transformation du message dans le paramètre `requestBody.value` est abordé à l’étape 3, [Créer un modèle de transformation](#create-transformation-template).

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## Étape 2 : créer une configuration de destination {#create-destination-configuration}

Vous trouverez ci-dessous un exemple de configuration d’un modèle de destination, créé à l’aide du point d’entrée d’API `/destinations`. Pour plus d’informations, voir [création d’une configuration de destination](../authoring-api/destination-configuration/create-destination-configuration.md).

Pour connecter la configuration du serveur et du modèle de l’étape 1 à cette configuration de destination, ajoutez l’ID d’instance de la configuration de serveur et de modèle en tant que `destinationServerId` ici.

>[!IMPORTANT]
>
>Pour créer une destination en temps réel (streaming) correctement configurée, vous *devez* ajouter au moins une identité cible dans `identityNamespaces`, comme illustré ci-dessous. Si aucune identité cible n’est configurée, les utilisateurs ne pourront pas aller plus loin que l’[Étape de mappage](../../ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation.

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
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
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },  
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## Étape 3 : créer un modèle de transformation de message : utilisez un langage de modèle pour spécifier le format de sortie du message {#create-transformation-template}

En fonction des payloads pris en charge par votre destination, vous devez créer un modèle qui transforme le format des données exportées à partir du format XDM d’Adobe dans un format pris en charge par votre destination. Consultez les exemples de modèles dans la section [Utilisation d’une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance à une audience](../functionality/destination-server/message-format.md#using-templating) et utilisez l’outil de création de modèles [&#x200B; fourni par Adobe](../testing-api/streaming-destinations/create-template.md).

Une fois que vous avez conçu un modèle de transformation de messages qui vous convient, ajoutez-le à la configuration de serveur et de modèle que vous avez créée à l’étape 1.

```json {line-numbers="true" highlight="13-14"}
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## Étape 4 : créer une configuration de métadonnées d’audience {#create-audience-metadata-configuration}

Pour certaines destinations, Destination SDK exige que vous configuriez des métadonnées d’audience afin de créer, mettre à jour ou supprimer des audiences par programmation dans votre destination. Pour plus d’informations sur le moment et la manière d’effectuer cette configuration, consultez la section [Gestion des métadonnées d’audience](../functionality/audience-metadata-management.md).

Si vous utilisez une configuration de métadonnées d’audience, vous devez la connecter à la configuration de destination créée à l’étape 2. Ajoutez l’ID d’instance de votre configuration de métadonnées d’audience à votre configuration de destination en tant que `audienceTemplateId`.

```json {line-numbers="true" highlight="53"}
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
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },   
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```


## Étape 5 : configurer l’authentification {#set-up-authentication}

Selon que vous spécifiez `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` dans la configuration de destination ci-dessus, vous pouvez configurer l’authentification pour votre destination à l’aide du point d’entrée `/destination` ou `/credentials`.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` est la plus commune des deux règles d’authentification. C’est celle à utiliser si vous demandez aux utilisateurs de fournir une forme d’authentification à la destination avant de pouvoir configurer une connexion et exporter des données.

Si vous avez sélectionné `"authenticationRule": "CUSTOMER_AUTHENTICATION"` dans la configuration de destination et que votre destination prend en charge la méthode d’authentification OAuth 2, lisez [Authentification OAuth 2](../functionality/destination-configuration/oauth2-authorization.md).

Si vous avez sélectionné `"authenticationRule": "PLATFORM_AUTHENTICATION"`, vous devez créer une configuration [informations d’identification](../credentials-api/create-credential-configuration.md) et transmettre l’identifiant de l’objet d’identification dans le paramètre `authenticationId` de la configuration [diffusion de destination](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication).

## Étape 6 : tester votre destination {#test-destination}

Une fois votre destination configurée à l’aide des points d’entrée de configuration dans les étapes précédentes, vous pouvez utiliser l’[outil de test des destinations](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) afin de tester l’intégration entre Adobe Experience Platform et votre destination.

Dans le cadre du processus de test de votre destination, vous devez utiliser l’interface utilisateur d’Experience Platform pour créer des segments que vous activerez vers votre destination. Reportez-vous aux deux ressources ci-dessous pour obtenir des instructions sur la création d’audiences dans Experience Platform :

* [Création d’une page de documentation sur les audiences](/help/segmentation/ui/audience-portal.md#create-audience)
* [Présentation vidéo Créer une audience](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=fr)

## Étape 7 : publier votre destination {#publish-destination}

>[!NOTE]
>
>Cette étape n’est pas obligatoire si vous créez une destination privée pour votre propre usage et que vous ne souhaitez pas la publier dans le catalogue des destinations pour que d’autres clients puissent l’utiliser.

Une fois votre destination configurée et testée, utilisez l’[API de publication de destination](../publishing-api/create-publishing-request.md) afin d’envoyer votre configuration à Adobe pour révision.

## Étape 8 : documenter votre destination {#document-destination}

>[!NOTE]
>
>Cette étape n’est pas obligatoire si vous créez une destination privée pour votre propre usage et que vous ne souhaitez pas la publier dans le catalogue des destinations pour que d’autres clients puissent l’utiliser.

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) créant une [intégration personnalisée](../overview.md#productized-custom-integrations), utilisez le [processus de documentation en libre-service](../docs-framework/documentation-instructions.md) pour créer une page de documentation du produit pour votre destination dans le [Catalogue des destinations Experience Platform](/help/destinations/catalog/overview.md).

## Étape 9 : envoyer la destination pour révision Adobe {#submit-for-review}

>[!NOTE]
>
>Cette étape n’est pas obligatoire si vous créez une destination privée pour votre propre usage et que vous ne souhaitez pas la publier dans le catalogue des destinations pour que d’autres clients puissent l’utiliser.

Enfin, avant que la destination puisse être publiée dans le catalogue Experience Platform et visible par tous les clients Experience Platform, vous devez envoyer officiellement la destination pour révision Adobe. Obtenez des informations complètes sur la manière d’[envoyer pour révision une destination personnalisée créée dans Destination SDK](../guides/submit-destination.md).
