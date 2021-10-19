---
description: Cette page répertorie et décrit les étapes de configuration d’une destination de diffusion en continu à l’aide du SDK de destination.
title: Comment utiliser le SDK de destination pour configurer une destination de diffusion en continu
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: a7c36f1a157b6020fede53e5c1074d966f26cf3d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Comment utiliser le SDK de destination pour configurer une destination de diffusion en continu

## Présentation {#overview}

Cette page décrit comment utiliser les informations dans [Options de configuration dans le SDK Destinations](./configuration-options.md) et dans d’autres fonctionnalités du SDK de destination et documents de référence d’API pour configurer un [destination de diffusion](/help/destinations/destination-types.md#streaming-destinations). Les étapes sont présentées dans l’ordre séquentiel ci-dessous.

>[!NOTE]
>
>Configuring a batch destination through Destination SDK is currently not supported.

## Conditions préalables {#prerequisites}

Before advancing to the steps illustrated below, please read the [Destination SDK getting started](./getting-started.md) page for information on obtaining the necessary Adobe I/O authentication credentials and other prerequisites to work with Destination SDK APIs.

## Étapes à suivre pour utiliser les options de configuration dans le SDK de destination pour configurer votre destination {#steps}

![Illustrated steps of using Destination SDK endpoints](./assets/destination-sdk-steps.png)

## Étape 1 : Création d’une configuration de serveur et de modèle {#create-server-template-configuration}

Commencez par créer une configuration de serveur et de modèle à l’aide de la `/destinations-server` point de terminaison (lecture) [Référence API](./destination-server-api.md)). For more information about the server and template configuration, refer to [Server and template specs](./configuration-options.md#server-and-template) in the reference section.

Shown below is an example configuration. Notez que le modèle de transformation de message dans le fichier `requestBody.value` est traité à l&#39;étape 3, [Créer un modèle de transformation](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

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

## Step 2: Create destination configuration {#create-destination-configuration}

Voici un exemple de configuration pour un modèle de destination, créé à l’aide de la `/destinations` Point de terminaison API. For more information about this template, refer to [Destination configuration](./destination-configuration.md).

Pour connecter la configuration du serveur et du modèle à l’étape 1 à cette configuration de destination, ajoutez l’ID d’instance de la configuration du serveur et du modèle en tant que `destinationServerId` ici.

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
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
      "mapUserInput":false,
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
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
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

## Étape 3 : Créer un modèle de transformation de message - utiliser un langage de modèle pour spécifier le format de sortie de message {#create-transformation-template}

Based on the payloads that your destination supports, you must create a template that transforms the format of the exported data from Adobe XDM format into a format supported by your destination. Voir des exemples de modèles dans la section [Utilisation d’une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance aux segments](./message-format.md#using-templating) et utilisez la [outil de création de modèles](./create-template.md) fourni par Adobe.

Once you have crafted a message transformation template that works for you, add it to the server and template configuration you created in step 1.

## Étape 4 : Créer une configuration de métadonnées d’audience {#create-audience-metadata-configuration}

Pour certaines destinations, le SDK de destination nécessite que vous configuriez une configuration de métadonnées d’audience pour créer, mettre à jour ou supprimer des publics dans votre destination par programme. Refer to [Audience metadata management](./audience-metadata-management.md) for information on when you need to set up this configuration and how to do it.

Si vous utilisez une configuration de métadonnées d’audience, vous devez la connecter à la configuration de destination que vous avez créée à l’étape 2. Add the instance ID of your audience metadata configuration to your destination configuration as `audienceTemplateId`.

## Étape 5 : Créer une configuration des informations d&#39;identification / Configurer l&#39;authentification {#set-up-authentication}

Selon que vous spécifiez `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` dans la configuration de destination ci-dessus, vous pouvez configurer l’authentification pour votre destination à l’aide de la `/destination` ou `/credentials` point de terminaison.

* **Cas le plus courant**: Si vous avez sélectionné `"authenticationRule": "CUSTOMER_AUTHENTICATION"` dans la configuration de destination et votre destination prend en charge la méthode d’authentification OAuth 2, lire [Authentification OAuth 2](./oauth2-authentication.md).
* Si vous avez sélectionné `"authenticationRule": "PLATFORM_AUTHENTICATION"`, reportez-vous à [Configuration des informations d&#39;identification](./credentials-configuration.md) dans la documentation de référence.

## Étape 6 : Test de votre destination {#test-destination}

Après avoir configuré votre destination à l’aide des points de terminaison de configuration des étapes précédentes, vous pouvez utiliser la [outil de test de destination](./create-template.md) pour tester l&#39;intégration entre Adobe Experience Platform et votre destination.

Dans le cadre du processus de test de votre destination, vous devez utiliser l’interface utilisateur de l’Experience Platform pour créer des segments que vous activerez vers votre destination. Reportez-vous aux deux ressources ci-dessous pour savoir comment créer des segments dans l’Experience Platform :

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Création d’une présentation vidéo de segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Étape 7 : Publication de votre destination {#publish-destination}

Après avoir configuré et testé votre destination, utilisez la [API de publication de destination](./destination-publish-api.md) pour soumettre votre configuration à Adobe pour révision.

## Étape 8 : Document de destination {#document-destination}

If you are an Independent Software Vendor (ISV) or System Integrator (SI) creating a [productized integration](./overview.md#productized-custom-integrations), use the [self-service documentation process](./docs-framework/documentation-instructions.md) to create a product documentation page for your destination in the [Experience League destinations catalog](/help/destinations/catalog/overview.md).
