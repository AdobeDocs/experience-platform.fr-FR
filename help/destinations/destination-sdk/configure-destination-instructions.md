---
description: Cette page répertorie et décrit les étapes de configuration d’une destination de diffusion en continu à l’aide du SDK de destination.
title: Comment utiliser le SDK de destination pour configurer une destination de diffusion en continu
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Comment utiliser le SDK de destination pour configurer une destination de diffusion en continu

## Présentation {#overview}

Cette page décrit comment utiliser les informations dans [Options de configuration dans le SDK Destinations](./configuration-options.md) et dans d’autres fonctionnalités du SDK de destination et documents de référence d’API pour configurer un [destination de diffusion](/help/destinations/destination-types.md#streaming-destinations). Les étapes sont présentées dans l’ordre séquentiel ci-dessous.

>[!NOTE]
>
>La configuration d’une destination par lots via le SDK de destination n’est actuellement pas prise en charge.

## Conditions préalables {#prerequisites}

Avant de passer aux étapes illustrées ci-dessous, veuillez lire la section [Prise en main du SDK de destination](./getting-started.md) pour plus d’informations sur l’obtention des informations d’identification d’authentification d’Adobe I/O nécessaires et d’autres conditions préalables à l’utilisation des API SDK de destination.

## Étapes à suivre pour utiliser les options de configuration dans le SDK de destination pour configurer votre destination {#steps}

![Etapes illustrées d’utilisation des points de terminaison du SDK de destination](./assets/destination-sdk-steps.png)

## Étape 1 : Création d’une configuration de serveur et de modèle {#create-server-template-configuration}

Commencez par créer une configuration de serveur et de modèle à l’aide de la `/destinations-server` point de terminaison (lecture) [Référence API](./destination-server-api.md)). Pour plus d’informations sur la configuration du serveur et du modèle, reportez-vous à la section [Spécifications relatives aux serveurs et aux modèles](./configuration-options.md#server-and-template) dans la section de référence.

Voici un exemple de configuration. Notez que le modèle de transformation de message dans le fichier `requestBody.value` est traité à l&#39;étape 3, [Créer un modèle de transformation](./configure-destination-instructions.md#create-transformation-template).

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

## Étape 2 : Créer une configuration de destination {#create-destination-configuration}

Voici un exemple de configuration pour un modèle de destination, créé à l’aide de la `/destinations` Point de terminaison API. Pour plus d’informations sur ce modèle, voir [Configuration de destination](./destination-configuration.md).

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

En fonction des charges prises en charge par votre destination, vous devez créer un modèle qui transforme le format des données exportées à partir du format XDM Adobe en un format pris en charge par votre destination. Voir des exemples de modèles dans la section [Utilisation d’une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance aux segments](./message-format.md#using-templating) et utilisez la [outil de création de modèles](./create-template.md) fourni par Adobe.

Une fois que vous avez conçu un modèle de transformation de message qui fonctionne pour vous, ajoutez-le à la configuration de serveur et de modèle que vous avez créée à l’étape 1.

## Étape 4 : Créer une configuration de métadonnées d’audience {#create-audience-metadata-configuration}

Pour certaines destinations, le SDK de destination nécessite que vous configuriez une configuration de métadonnées d’audience pour créer, mettre à jour ou supprimer des publics dans votre destination par programme. Reportez-vous à [Gestion des métadonnées du public](./audience-metadata-management.md) pour plus d’informations sur le moment où vous devez configurer cette configuration et comment le faire.

Si vous utilisez une configuration de métadonnées d’audience, vous devez la connecter à la configuration de destination que vous avez créée à l’étape 2. Ajoutez l’ID d’instance de votre configuration de métadonnées d’audience à votre configuration de destination en tant que `audienceTemplateId`.

## Étape 5 : Créer une configuration des informations d&#39;identification / Configurer l&#39;authentification {#set-up-authentication}

Selon que vous spécifiez `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` dans la configuration de destination ci-dessus, vous pouvez configurer l’authentification pour votre destination à l’aide de la `/destination` ou `/credentials` point de terminaison.

* **Cas le plus courant**: Si vous avez sélectionné `"authenticationRule": "CUSTOMER_AUTHENTICATION"` dans la configuration de destination et votre destination prend en charge la méthode d’authentification OAuth 2, lire [Authentification OAuth 2](./oauth2-authentication.md).
* Si vous avez sélectionné `"authenticationRule": "PLATFORM_AUTHENTICATION"`, reportez-vous à [Configuration des informations d&#39;identification](./credentials-configuration.md) dans la documentation de référence.

## Étape 6 : Test de votre destination {#test-destination}

Après avoir configuré votre destination à l’aide des points de terminaison de configuration des étapes précédentes, vous pouvez utiliser la [outil de test de destination](./create-template.md) pour tester l&#39;intégration entre Adobe Experience Platform et votre destination.

Dans le cadre du processus de test de votre destination, vous devez utiliser l’interface utilisateur de l’Experience Platform pour créer des segments que vous activerez vers votre destination. Reportez-vous aux deux ressources ci-dessous pour savoir comment créer des segments dans l’Experience Platform :

* [Création d’une page de documentation sur les segments](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Création d’une présentation vidéo de segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Étape 7 : Publication de votre destination {#publish-destination}

Après avoir configuré et testé votre destination, utilisez la [API de publication de destination](./destination-publish-api.md) pour soumettre votre configuration à Adobe pour révision.

## Étape 8 : Document de destination {#document-destination}

Si vous êtes un fournisseur de logiciels indépendants (ISV) ou un intégrateur de système (SI), créez un [intégration productive](./overview.md#productized-custom-integrations), utilisez la [processus de documentation en libre-service](./docs-framework/documentation-instructions.md) pour créer une page de documentation de produit pour votre destination dans le dossier [Catalogue de destinations Experience Platform](/help/destinations/catalog/overview.md).
