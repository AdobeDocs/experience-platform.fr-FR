---
description: Cette page décrit comment utiliser les informations de référence dans les options de configuration du SDK Destinations pour configurer votre destination à l’aide du SDK Destination.
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: Comment utiliser le SDK de destination pour configurer votre destination
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Comment utiliser le SDK de destination pour configurer votre destination

## Présentation {#overview}

Cette page décrit comment utiliser les informations de référence dans les [options de configuration dans le SDK Destinations](./configuration-options.md) pour configurer votre destination. Les étapes sont présentées dans l’ordre séquentiel ci-dessous.

## Conditions préalables {#prerequisites}

Avant de passer aux étapes illustrées ci-dessous, consultez la page [Prise en main du SDK de destination](./getting-started.md) pour plus d’informations sur l’obtention des informations d’identification d’authentification d’Adobe I/O nécessaires et d’autres conditions préalables pour travailler avec les API du SDK de destination.

## Étapes d’utilisation des options de configuration dans le SDK de destination pour configurer votre destination {#steps}

![Étapes illustrées d’utilisation des points d’entrée du SDK de destination](./assets/destination-sdk-steps.png)

## Étape 1 : Création d’une configuration de serveur et de modèle {#create-server-template-configuration}

Commencez par créer une configuration de serveur et de modèle à l’aide du point de terminaison `/destinations-server` (lire [Référence d’API](./destination-server-api.md)). Pour plus d’informations sur la configuration du serveur et des modèles, voir [Spécifications du serveur et des modèles](./configuration-options.md#server-and-template) dans la section de référence.

Vous trouverez ci-dessous un exemple de configuration. Notez que le modèle de transformation du message dans le paramètre `requestBody.value` est abordé à l’étape 3, [Créer un modèle de transformation](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
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

## Étape 2 : Création d’une configuration de destination {#create-destination-configuration}

Vous trouverez ci-dessous un exemple de configuration pour un modèle de destination, créé à l’aide du point de terminaison de l’API `/destinations`. Pour plus d’informations sur ce modèle, voir [Configuration de la destination](./destination-configuration.md).

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
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed"
}
```

## Étape 3 : Créer un modèle de transformation de message : utilisez un langage de modèle pour spécifier le format de sortie du message. {#create-transformation-template}

En fonction des payloads pris en charge par votre destination, vous devez créer un modèle qui transforme le format des données exportées à partir du format XDM Adobe dans un format pris en charge par votre destination. Consultez les exemples de modèles dans la section [Utilisation d’un langage de modèle pour les transformations d’identité, d’attributs et d’appartenance à un segment](./message-format.md#using-templating) et utilisez l’[outil de création de modèles](./create-template.md) fourni par Adobe.

## Étape 4 : Création d’une configuration de métadonnées d’audience {#create-audience-metadata-configuration}

Pour certaines destinations, le SDK de destination requiert que vous configuriez un modèle de métadonnées d’audience pour créer, mettre à jour ou supprimer des audiences par programmation dans votre destination. Consultez la section [Gestion des métadonnées d’audience](./audience-metadata-management.md) pour plus d’informations sur le moment où vous devez configurer cette configuration et la manière de procéder.

## Étape 5 : Création de la configuration des informations d’identification / Configuration de l’authentification {#set-up-authentication}

Selon que vous spécifiez `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ou `"authenticationRule": "PLATFORM_AUTHENTICATION"` dans la configuration de destination ci-dessus, vous pouvez configurer l’authentification pour votre destination à l’aide du point de terminaison `/destination` ou `/credentials`.

* **Cas** le plus courant : Si vous avez sélectionné  `"authenticationRule": "CUSTOMER_AUTHENTICATION"` et que votre destination prend en charge la méthode d’authentification OAuth 2, lisez  [Authentification OAuth 2](./oauth2-authentication.md).
* Si vous avez sélectionné `"authenticationRule": "PLATFORM_AUTHENTICATION"`, reportez-vous à la section [Configuration des informations d’identification](./credentials-configuration.md) dans la documentation de référence.

## Étape 6 : Tester votre destination {#test-destination}

Après avoir configuré votre destination à l’aide des modèles des étapes précédentes, vous pouvez utiliser l’[outil de test de destination](./create-template.md) pour tester l’intégration entre Adobe Experience Platform et votre destination.

Dans le cadre du processus de test de votre destination, vous devez utiliser l’interface utilisateur de l’Experience Platform pour créer des segments que vous activerez vers votre destination. Reportez-vous aux deux ressources ci-dessous pour savoir comment créer des segments dans Experience Platform :

* [Création d’une page de documentation sur les segments](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Présentation vidéo de la création d’un segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## Étape 7 : Publier votre destination {#publish-destination}

Après avoir configuré et testé votre destination, utilisez l’[API de publication de destination](./destination-publish-api.md) pour envoyer votre configuration à Adobe en vue de la révision.

## Étape 8 : Document de votre destination {#document-destination}

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) créant une [intégration productisée](./overview.md#productized-custom-integrations), utilisez le [processus de documentation en libre-service](./docs-framework/documentation-instructions.md) pour créer une page de documentation de produit pour votre destination dans le [catalogue de destinations Experience League](/help/destinations/catalog/overview.md).
