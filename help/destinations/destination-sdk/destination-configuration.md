---
description: Cette configuration vous permet d’indiquer des informations de base telles que votre nom de destination, votre catégorie, votre description, votre logo, etc. Les paramètres de cette configuration déterminent également comment les utilisateurs Experience Platform s’authentifient pour votre destination, comment ils apparaissent dans l’interface utilisateur Experience Platform et les identités qui peuvent être exportées vers votre destination.
title: Options de configuration de destination pour le SDK de destination
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 63fe3b7cc429a1c18cebe998bc82fdea99a6679b
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 5%

---

# Configuration de la destination {#destination-configuration}

## Présentation {#overview}

Cette configuration vous permet d’indiquer des informations de base telles que votre nom de destination, votre catégorie, votre description, votre logo, etc. Les paramètres de cette configuration déterminent également comment les utilisateurs Experience Platform s’authentifient pour votre destination, comment ils apparaissent dans l’interface utilisateur Experience Platform et les identités qui peuvent être exportées vers votre destination.

Vous pouvez configurer les fonctionnalités décrites dans ce document à l’aide du point de terminaison de l’API `/authoring/destinations`. Lisez [Opérations de point d’entrée de l’API Destinations](./destination-configuration-api.md) pour obtenir la liste complète des opérations que vous pouvez effectuer sur le point d’entrée.

## Exemple de configuration  {#example-configuration}

Vous trouverez ci-dessous un exemple de configuration pour une destination fictive, Moviestar, qui comporte des points de terminaison dans quatre endroits sur le globe. La destination appartient à la catégorie des destinations mobiles. Les sections ci-dessous présentent la manière dont cette configuration est créée.

```json
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
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   }
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `name` | Chaîne | Indique le titre de votre destination dans le catalogue des Experience Platform. |
| `description` | Chaîne | Fournissez une description que l’Adobe utilisera dans le catalogue des destinations Experience Platform pour votre carte de destination. Ne vise pas plus de 4 à 5 phrases. |
| `status` | Chaîne | Indique l’état du cycle de vie de la carte de destination. Les valeurs acceptées sont `TEST`, `PUBLISHED` et `DELETED`. Utilisez `TEST` lorsque vous configurez votre destination pour la première fois. |

{style=&quot;table-layout:auto&quot;}

## Configurations de l’authentification du client {#customer-authentication-configurations}

Cette section génère la page du compte dans l’interface utilisateur de l’Experience Platform, où les utilisateurs se connectent Experience Platform aux comptes qu’ils possèdent avec votre destination. Selon l’option d’authentification que vous indiquez dans le champ `authType` , la page Experience Platform est générée pour les utilisateurs comme suit :

**Authentification du porteur**

Les utilisateurs doivent saisir le jeton porteur qu’ils obtiennent de votre destination.

![Rendu de l’interface utilisateur avec authentification du porteur](./assets/bearer-authentication-ui.png)

**Authentification OAuth 2**

Les utilisateurs sélectionnent **[!UICONTROL Se connecter à la destination]** pour déclencher le flux d’authentification OAuth 2 vers votre destination.

![Rendu de l’interface utilisateur avec authentification OAuth 2](./assets/oauth2-authentication-ui.png)


| Paramètre | Type | Description |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Chaîne | Indique la configuration utilisée pour authentifier les clients Experience Platform sur votre serveur. Voir `authType` ci-dessous pour connaître les valeurs acceptées. |
| `authType` | Chaîne | Les valeurs acceptées sont `OAUTH2, BEARER`. <br><ul><li> Si votre destination prend en charge l’authentification OAuth 2, sélectionnez la valeur `OAUTH2` et ajoutez les champs requis pour OAuth 2, comme indiqué dans la page d’authentification du SDK de destination OAuth 2. De plus, vous devez sélectionner `authenticationRule=CUSTOMER_AUTHENTICATION` dans la section [Diffusion de destination](./destination-configuration.md). </li><li>Pour l’authentification du porteur, sélectionnez `BEARER` et sélectionnez `authenticationRule=CUSTOMER_AUTHENTICATION` dans la [section de diffusion de destination](./destination-configuration.md).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Champs de données client {#customer-data-fields}

Cette section permet aux partenaires d’introduire des champs personnalisés. Dans l’exemple de configuration ci-dessus, `customerDataFields` exige que les utilisateurs sélectionnent un point de terminaison dans le flux d’authentification et indiquent leur ID de client avec la destination. La configuration se reflète dans le flux d’authentification comme illustré ci-dessous :

![Flux d’authentification de champ personnalisé](./assets/custom-field-authentication-flow.png)

| Paramètre | Type | Description |
|---------|----------|------|
| `name` | Chaîne | Attribuez un nom au champ personnalisé que vous introduisez. |
| `type` | Chaîne | Indique le type de champ personnalisé que vous introduisez. Les valeurs acceptées sont `string`, `object`, `integer`. |
| `title` | Chaîne | Indique le nom du champ, tel qu’il est affiché par les clients dans l’interface utilisateur de l’Experience Platform. |
| `description` | Chaîne | Fournissez une description du champ personnalisé. |
| `isRequired` | Booléen | Indique si ce champ est requis dans le workflow de configuration de destination. |
| `enum` | Chaîne | Rend le champ personnalisé sous forme de menu déroulant et répertorie les options disponibles pour l’utilisateur. |
| `pattern` | Chaîne | Impose un modèle pour le champ personnalisé, si nécessaire. Utilisez des expressions régulières pour appliquer un modèle. Par exemple, si vos ID de client n’incluent pas de chiffres ou de traits de soulignement, saisissez `^[A-Za-z]+$` dans ce champ. |

{style=&quot;table-layout:auto&quot;}

## Attributs de l’interface utilisateur {#ui-attributes}

Cette section fait référence aux éléments de l’interface utilisateur dans la configuration ci-dessus que l’Adobe doit utiliser pour votre destination dans l’interface utilisateur de Adobe Experience Platform. Voir ci-dessous :

| Paramètre | Type | Description |
|---------|----------|------|
| `documentationLink` | Chaîne | Fait référence à la page de documentation du [catalogue des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) pour votre destination. Utilisez `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, où `YOURDESTINATION` est le nom de votre destination. Pour une destination appelée Moviestar, vous utiliseriez `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Chaîne | Fait référence à la catégorie affectée à votre destination dans Adobe Experience Platform. Pour plus d’informations, consultez [Catégories de destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilisez l’une des valeurs suivantes : `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Chaîne | `Server-to-server` est actuellement la seule option disponible. |
| `frequency` | Chaîne | `Streaming` est actuellement la seule option disponible. |

{style=&quot;table-layout:auto&quot;}

## Configuration du schéma dans l’étape de mappage {#schema-configuration}

![Activer l’étape de mappage](./assets/enable-mapping-step.png)

Utilisez les paramètres de `schemaConfig` pour activer l’étape de mappage du workflow d’activation de destination. En utilisant les paramètres décrits ci-dessous, vous pouvez déterminer si les utilisateurs Experience Platform peuvent mapper des attributs de profil et/ou des identités au schéma souhaité du côté de votre destination.

| Paramètre | Type | Description |
|---------|----------|------|
| `profileFields` | Tableau | *Non affiché dans l’exemple de configuration ci-dessus.* Lorsque vous ajoutez des attributs prédéfinis  `profileFields`, les utilisateurs auront la possibilité de mapper les attributs Experience Platform aux attributs prédéfinis du côté de votre destination. |
| `profileRequired` | Booléen | Utilisez `true` si les utilisateurs doivent être en mesure de mapper les attributs de profil de l’Experience Platform aux attributs personnalisés du côté de votre destination, comme illustré dans l’exemple de configuration ci-dessus. |
| `segmentRequired` | Booléen | Utilisez toujours `segmentRequired:true`. |
| `identityRequired` | Booléen | Utilisez `true` si les utilisateurs doivent pouvoir mapper les espaces de noms d’identité de l’Experience Platform à votre schéma souhaité. |

{style=&quot;table-layout:auto&quot;}

## Identités et attributs {#identities-and-attributes}

Les paramètres de cette section déterminent la manière dont les identités et attributs de la cible sont renseignés à l’étape de mappage de l’interface utilisateur de l’Experience Platform, où les utilisateurs mappent leurs schémas XDM au schéma de votre destination.

Adobe doit savoir quelles [!DNL Platform] identités les clients pourront exporter vers votre destination. Voici quelques exemples : [!DNL Experience Cloud ID], adresse électronique hachée, ID d’appareil ([!DNL IDFA], [!DNL GAID]). Ces valeurs sont des [!DNL Platform] espaces de noms d’identité que les clients peuvent mapper aux espaces de noms d’identité de votre destination.

Les espaces de noms d’identité ne nécessitent pas de correspondance 1-à-1 entre [!DNL Platform] et votre destination.
Par exemple, les clients peuvent mapper un espace de noms [!DNL Platform] [!DNL IDFA] à un espace de noms [!DNL IDFA] à partir de votre destination, ou ils peuvent mapper le même [!DNL Platform] [!DNL IDFA] à un espace de noms [!DNL Customer ID] dans votre destination.

Pour en savoir plus, consultez la [présentation de l’espace de noms d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr).

![Rendu des identités cibles dans l’interface utilisateur](./assets/target-identities-ui.png)

| Paramètre | Type | Description |
|---------|----------|------|
| `acceptsAttributes` | Booléen | Indique si votre destination accepte les attributs de profil standard. En règle générale, ces attributs sont mis en évidence dans la documentation de nos partenaires. |
| `acceptsCustomNamespaces` | Booléen | Indique si les clients peuvent configurer des espaces de noms personnalisés dans votre destination. |
| `allowedAttributesTransformation` | Chaîne | *Non affiché dans l’exemple de configuration*. Utilisé, par exemple, lorsque le client [!DNL Platform] a des adresses électroniques ordinaires comme attribut et que votre plateforme n’accepte que des emails hachés. C’est là que vous fournissez la transformation à appliquer (par exemple, transformez l’email en minuscules, puis en hachage). |
| `acceptedGlobalNamespaces` | - | *Non affiché dans l’exemple de configuration*. Utilisé dans les cas où votre plateforme accepte des [espaces de noms d’identité standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (IDFA, par exemple), afin que vous puissiez empêcher les utilisateurs de Platform de sélectionner uniquement ces espaces de noms d’identité. |

{style=&quot;table-layout:auto&quot;}

## Diffusion de destination {#destination-delivery}

| Paramètre | Type | Description |
|---------|----------|------|
| `authenticationRule` | Chaîne | Indique comment les clients [!DNL Platform] se connectent à votre destination. Les valeurs acceptées sont `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilisez `CUSTOMER_AUTHENTICATION` si les clients Platform se connectent à votre système par l’intermédiaire d’un nom d’utilisateur et d’un mot de passe, d’un jeton porteur ou d’une autre méthode d’authentification. Par exemple, sélectionnez cette option si vous avez également sélectionné `authType: OAUTH2` ou `authType:BEARER` dans `customerAuthenticationConfigurations`. </li><li> Utilisez `PLATFORM_AUTHENTICATION` s’il existe un système d’authentification global entre l’Adobe et votre destination et que le client [!DNL Platform] n’a pas besoin de fournir d’informations d’identification d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide de la configuration [Credentials](./credentials-configuration.md) . </li><li>Utilisez `NONE` si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `destinationServerId` | Chaîne | `instanceId` de la [configuration du serveur de destination](./destination-server-api.md) utilisée pour cette destination. |
| `backfillHistoricalProfileData` | Booléen | Contrôle si les données de profil historiques sont exportées lorsque les segments sont activés vers la destination. <br> <ul><li> `true`:  [!DNL Platform] envoie les profils utilisateur historiques qualifiés pour le segment avant l’activation du segment. </li><li> `false`:  [!DNL Platform] inclut uniquement les profils utilisateur qui remplissent les critères pour le segment une fois le segment activé. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Configuration du mappage de segments {#segment-mapping}

![Section de configuration du mappage de segments](./assets/segment-mapping-configuration.png)

Cette section de la configuration de destination concerne la manière dont les métadonnées de segment telles que les noms ou les identifiants doivent être partagées entre l’Experience Platform et votre destination.

Grâce à la section `audienceTemplateId`, cette section associe également cette configuration à la [configuration des métadonnées d’audience](./audience-metadata-management.md).

Les paramètres affichés dans la configuration ci-dessus sont décrits dans la [référence de l’API du point de terminaison des destinations](./destination-configuration-api.md).

## Stratégie d’agrégation {#aggregation}

![Stratégie d’agrégation dans le modèle de configuration](./assets/aggregation-configuration.png)

Cette section vous permet de définir les stratégies d’agrégation que l’Experience Platform utilisera lors de l’exportation de données vers votre destination.

Une stratégie d’agrégation détermine la manière dont les profils exportés sont combinés dans les exportations de données. Les options disponibles sont les suivantes :
* Agrégation des meilleurs efforts
* Agrégation configurable (affichée dans la configuration ci-dessus)

Lisez la section sur [à l’aide du modèle](./message-format.md#using-templating) et des [exemples de clés d’agrégation](./message-format.md#template-aggregation-key) pour comprendre comment inclure la stratégie d’agrégation dans votre modèle de transformation de messages en fonction de la stratégie d’agrégation que vous avez sélectionnée.

### Agrégation des meilleurs efforts {#best-effort-aggregation}

>[!TIP]
>
>Utilisez cette option si votre point de terminaison API accepte moins de 100 profils par appel d’API.

Cette option fonctionne mieux pour les destinations qui préfèrent moins de profils par requête et qui préfèrent recevoir plus de requêtes avec moins de données que de requêtes avec plus de données.

Utilisez le paramètre `maxUsersPerRequest` pour spécifier le nombre maximal de profils que votre destination peut prendre dans une requête.

### Agrégation configurable {#configurable-aggregation}

Cette option fonctionne mieux si vous préférez prendre des lots volumineux, avec des milliers de profils sur le même appel. Cette option permet également d&#39;agréger les profils exportés en fonction de règles d&#39;agrégation complexes.

Cette option vous permet d’effectuer les opérations suivantes :
* Définissez la durée et le nombre maximal de profils à agréger avant qu’un appel API ne soit effectué vers votre destination.
* Agrégez les profils exportés mappés à la destination en fonction des éléments suivants :
   * identifiant de segment
   * état du segment
   * identité ou groupes d’identités

Pour obtenir des explications détaillées sur les paramètres d’agrégation, consultez la page de référence [Opérations de point d’entrée de l’API Destinations](./destination-configuration-api.md), où chaque paramètre est décrit.

<!--

commenting out the `backfillHistoricalProfileData` parameter, which will only be used after an April release

|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

-->
