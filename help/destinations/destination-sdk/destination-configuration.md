---
description: Cette configuration vous permet d’indiquer des informations de base telles que votre nom de destination, votre catégorie, votre description, votre logo, etc. Les paramètres de cette configuration déterminent également comment les utilisateurs Experience Platform s’authentifient pour votre destination, comment ils apparaissent dans l’interface utilisateur Experience Platform et les identités qui peuvent être exportées vers votre destination.
title: Options de configuration de destination de diffusion en continu pour Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 51417bee5dba7a96d3a7a7eb507fc95711fad4a5
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 4%

---

# Configuration de destination de diffusion en continu {#destination-configuration}

## Présentation {#overview}

Cette configuration vous permet d’indiquer les informations essentielles à votre destination de diffusion en continu, telles que votre nom de destination, votre catégorie, votre description, etc. Les paramètres de cette configuration déterminent également comment les utilisateurs Experience Platform s’authentifient pour votre destination, comment ils apparaissent dans l’interface utilisateur Experience Platform et les identités qui peuvent être exportées vers votre destination.

Cette configuration connecte également les autres configurations requises pour que votre destination fonctionne (métadonnées de serveur de destination et d’audience) à celle-ci. Découvrez comment vous pouvez référencer les deux configurations dans une [voir ci-dessous](./destination-configuration.md#connecting-all-configurations).

Vous pouvez configurer les fonctionnalités décrites dans ce document à l’aide du `/authoring/destinations` Point d’entrée de l’API. Lecture [Opérations de point d’entrée de l’API Destinations](./destination-configuration-api.md) pour obtenir une liste complète des opérations que vous pouvez effectuer sur le point de terminaison .

## Exemple de configuration de diffusion en continu {#example-configuration}

Voici un exemple de configuration d’une destination fictive de diffusion en continu, Moviestar, qui a des points de terminaison dans quatre endroits sur le globe. La destination appartient à la catégorie des destinations mobiles.

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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000,
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
   },
   "backfillHistoricalProfileData":true
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `name` | Chaîne | Indique le titre de votre destination dans le catalogue des Experience Platform. |
| `description` | Chaîne | Fournissez une description de votre carte de destination dans le catalogue des destinations Experience Platform. Ne vise pas plus de 4 à 5 phrases. |
| `status` | Chaîne | Indique l’état du cycle de vie de la carte de destination. Les valeurs acceptées sont `TEST`, `PUBLISHED` et `DELETED`. Utilisation `TEST` lorsque vous configurez votre destination pour la première fois. |

{style=&quot;table-layout:auto&quot;}

## Configurations de l’authentification du client {#customer-authentication-configurations}

Cette section de la configuration des destinations génère la variable [Configuration d’une nouvelle destination](/help/destinations/ui/connect-destination.md) dans l’interface utilisateur de l’Experience Platform, où les utilisateurs se connectent Experience Platform aux comptes qu’ils possèdent avec votre destination. Selon l’option d’authentification que vous indiquez dans la variable `authType` , la page Experience Platform est générée pour les utilisateurs comme suit :

### Authentification du porteur

Lorsque vous configurez le type d’authentification du porteur, les utilisateurs doivent saisir le jeton du porteur qu’ils obtiennent de votre destination.

![Rendu de l’interface utilisateur avec authentification du porteur](assets/bearer-authentication-ui.png)

### Authentification OAuth 2

Sélection des utilisateurs **[!UICONTROL Se connecter à la destination]** pour déclencher le flux d’authentification OAuth 2 vers votre destination, comme illustré dans l’exemple ci-dessous pour la destination Audiences personnalisées de Twitter. Pour plus d’informations sur la configuration de l’authentification OAuth 2 à votre point de terminaison de destination, consultez le [Page d’authentification OAuth 2 de la Destination SDK](./oauth2-authentication.md).

![Rendu de l’interface utilisateur avec authentification OAuth 2](assets/oauth2-authentication-ui.png)

| Paramètre | Type | Description |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Chaîne | Indique la configuration utilisée pour authentifier les clients Experience Platform sur votre serveur. Voir `authType` ci-dessous pour les valeurs acceptées. |
| `authType` | Chaîne | Les valeurs acceptées pour les destinations de diffusion en continu sont les suivantes :<ul><li>`BEARER`. Si votre destination prend en charge l’authentification du porteur, définissez `"authType":"Bearer"` et  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` dans le [section de diffusion de destination](./destination-configuration.md).</li><li>`OAUTH2`. Si votre destination prend en charge l’authentification OAuth 2, définissez `"authType":"OAUTH2"` et ajoutez les champs requis pour OAuth 2, comme indiqué dans la section [Page d’authentification OAuth 2 de la Destination SDK](./oauth2-authentication.md). En outre, définissez `"authenticationRule":"CUSTOMER_AUTHENTICATION"` dans le [section de diffusion de destination](./destination-configuration.md).</li> |

{style=&quot;table-layout:auto&quot;}

## Champs de données client {#customer-data-fields}

Utilisez cette section pour demander aux utilisateurs de renseigner des champs personnalisés, spécifiques à votre destination, lors de la connexion à la destination dans l’interface utilisateur de l’Experience Platform. La configuration se reflète dans le flux d’authentification comme illustré ci-dessous :

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
| `documentationLink` | Chaîne | Fait référence à la page de documentation de la [Catalogue des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) pour votre destination. Utilisation `http://www.adobe.com/go/destinations-YOURDESTINATION-en`où `YOURDESTINATION` est le nom de votre destination. Pour une destination appelée Moviestar, vous utiliseriez `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Chaîne | Fait référence à la catégorie affectée à votre destination dans Adobe Experience Platform. Pour plus d’informations, reportez-vous à la section [Catégories de destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilisez l’une des valeurs suivantes : `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Chaîne | `Server-to-server` est actuellement la seule option disponible. |
| `frequency` | Chaîne | Fait référence au type d’exportation des données pris en charge par la destination. Valeurs prises en charge : <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Configuration du schéma dans l’étape de mappage {#schema-configuration}

![Activer l’étape de mappage](./assets/enable-mapping-step.png)

Utilisez les paramètres de la section `schemaConfig` pour activer l’étape de mappage du workflow d’activation de destination. En utilisant les paramètres décrits ci-dessous, vous pouvez déterminer si les utilisateurs Experience Platform peuvent mapper des attributs de profil et/ou des identités au schéma souhaité du côté de votre destination.

| Paramètre | Type | Description |
|---------|----------|------|
| `profileFields` | Tableau | *Non affiché dans l’exemple de configuration ci-dessus.* Lorsque vous ajoutez une prédéfinie `profileFields`, les utilisateurs Experience Platform ont la possibilité de mapper les attributs de Platform aux attributs prédéfinis du côté de votre destination. |
| `profileRequired` | Booléen | Utilisation `true` si les utilisateurs doivent être en mesure de mapper les attributs de profil de l’Experience Platform aux attributs personnalisés du côté de votre destination, comme illustré dans l’exemple de configuration ci-dessus. |
| `segmentRequired` | Booléen | Toujours utiliser `segmentRequired:true`. |
| `identityRequired` | Booléen | Utilisation `true` si les utilisateurs doivent être en mesure de mapper des espaces de noms d’identité d’Experience Platform à votre schéma souhaité. |

{style=&quot;table-layout:auto&quot;}


## Identités et attributs {#identities-and-attributes}

Les paramètres de cette section déterminent quelles identités votre destination accepte. Cette configuration renseigne également les identités et les attributs de la cible dans la variable [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) de l’interface utilisateur de l’Experience Platform, où les utilisateurs mappent les identités et les attributs de leurs schémas XDM au schéma de votre destination.

Vous devez indiquer laquelle [!DNL Platform] identités les clients peuvent exporter vers votre destination. Voici quelques exemples : [!DNL Experience Cloud ID], courrier électronique haché, ID d’appareil ([!DNL IDFA], [!DNL GAID]). Ces valeurs sont les suivantes : [!DNL Platform] espaces de noms d’identité que les clients peuvent mapper aux espaces de noms d’identité de votre destination. Vous pouvez également indiquer si les clients peuvent mapper des espaces de noms personnalisés à des identités prises en charge par votre destination.

Les espaces de noms d’identité ne nécessitent pas de correspondance 1-1 entre [!DNL Platform] et votre destination.
Par exemple, les clients peuvent mapper une [!DNL Platform] [!DNL IDFA] d’un espace de noms [!DNL IDFA] ou mapper le même espace de noms à partir de votre destination. [!DNL Platform] [!DNL IDFA] d’un espace de noms [!DNL Customer ID] dans votre destination.

En savoir plus dans la section [Présentation d’Identity Namespace](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr).

![Rendu des identités cibles dans l’interface utilisateur](./assets/target-identities-ui.png)

| Paramètre | Type | Description |
|---------|----------|------|
| `acceptsAttributes` | Booléen | Indique si votre destination accepte les attributs de profil standard. En règle générale, ces attributs sont mis en évidence dans la documentation des partenaires. |
| `acceptsCustomNamespaces` | Booléen | Indique si les clients peuvent configurer des espaces de noms personnalisés dans votre destination. |
| `allowedAttributesTransformation` | Chaîne | *Non affiché dans l’exemple de configuration*. Utilisé, par exemple, lorsque la variable [!DNL Platform] Le client dispose d’adresses électroniques simples en tant qu’attribut et votre plateforme accepte uniquement les emails hachés. Dans cet objet, vous pouvez effectuer la transformation qui doit être appliquée (par exemple, transformer l&#39;email en minuscules, puis en hachage). Pour consulter un exemple, reportez-vous à la section `requiredTransformation` dans le [référence de l’API de configuration de destination](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | Utilisé pour les cas où votre plateforme accepte [espaces de noms d’identité standard](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (IDFA, par exemple), afin que vous puissiez empêcher les utilisateurs de Platform de sélectionner uniquement ces espaces de noms d’identité. |

{style=&quot;table-layout:auto&quot;}

## Diffusion de destination {#destination-delivery}

| Paramètre | Type | Description |
|---------|----------|------|
| `authenticationRule` | Chaîne | Indique comment [!DNL Platform] les clients se connectent à votre destination. Les valeurs acceptées sont `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilisation `CUSTOMER_AUTHENTICATION` si les clients Platform se connectent à votre système par le biais d’un nom d’utilisateur et d’un mot de passe, d’un jeton porteur ou d’une autre méthode d’authentification. Par exemple, sélectionnez cette option si vous avez également sélectionné `authType: OAUTH2` ou `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Utilisation `PLATFORM_AUTHENTICATION` s’il existe un système d’authentification global entre l’Adobe et votre destination et la variable [!DNL Platform] Le client n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide de la variable [Informations d’identification](./credentials-configuration-api.md) configuration. </li><li>Utilisation `NONE` si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `destinationServerId` | Chaîne | Le `instanceId` de [configuration du serveur de destination](./destination-server-api.md) utilisé pour cette destination. |

{style=&quot;table-layout:auto&quot;}

## Configuration du mappage de segments {#segment-mapping}

![Section de configuration du mappage de segments](./assets/segment-mapping-configuration.png)

Cette section de la configuration de destination concerne la manière dont les métadonnées de segment telles que les noms ou les identifiants doivent être partagées entre l’Experience Platform et votre destination.

Par le biais de la `audienceTemplateId`, cette section associe également cette configuration à la variable [configuration des métadonnées d’audience](./audience-metadata-management.md).

Les paramètres affichés dans la configuration ci-dessus sont décrits dans la section [référence de l’API du point d’entrée des destinations](./destination-configuration-api.md).

## Stratégie d’agrégation {#aggregation}

![Stratégie d’agrégation dans le modèle de configuration](./assets/aggregation-configuration.png)

Cette section vous permet de définir les stratégies d’agrégation que l’Experience Platform doit utiliser lors de l’exportation de données vers votre destination.

Une stratégie d’agrégation détermine la manière dont les profils exportés sont combinés dans les exportations de données. Les options disponibles sont les suivantes :
* Agrégation des meilleurs efforts
* Agrégation configurable (affichée dans la configuration ci-dessus)

Lisez la section sur [utilisation de modèles](./message-format.md#using-templating) et le [exemples clés d’agrégation](./message-format.md#template-aggregation-key) pour comprendre comment inclure la stratégie d’agrégation dans votre modèle de transformation des messages en fonction de votre stratégie d’agrégation sélectionnée.

### Agrégation des meilleurs efforts {#best-effort-aggregation}

>[!TIP]
>
>Utilisez cette option si votre point de terminaison API accepte moins de 100 profils par appel d’API.

Cette option fonctionne mieux pour les destinations qui préfèrent moins de profils par requête et qui préfèrent recevoir plus de requêtes avec moins de données que de requêtes avec plus de données.

Utilisez la variable `maxUsersPerRequest` pour spécifier le nombre maximal de profils que votre destination peut prendre dans une requête.

### Agrégation configurable {#configurable-aggregation}

Cette option fonctionne mieux si vous préférez prendre des lots volumineux, avec des milliers de profils sur le même appel. Cette option permet également d&#39;agréger les profils exportés en fonction de règles d&#39;agrégation complexes.

Cette option vous permet d’effectuer les opérations suivantes :
* Définissez la durée maximale et le nombre maximal de profils à agréger avant qu’un appel API ne soit effectué vers votre destination.
* Agrégez les profils exportés mappés à la destination en fonction des éléments suivants :
   * Identifiant de segment;
   * État du segment ;
   * Identité ou groupes d’identités.

>[!NOTE]
>
>Lorsque vous utilisez l’option d’agrégation configurable pour votre destination, gardez à l’esprit les valeurs minimale et maximale que vous pouvez utiliser pour les deux paramètres. `maxBatchAgeInSecs` (minimum 1 800 et maximum 3 600) et `maxNumEventsInBatch` (minimum 1 000, maximum 10 000).

Pour des explications détaillées des paramètres d&#39;agrégation, reportez-vous à la section [Opérations de point d’entrée de l’API Destinations](./destination-configuration-api.md) page de référence, où chaque paramètre est décrit.

## Qualifications des profils historiques {#profile-backfill}

Vous pouvez utiliser la variable `backfillHistoricalProfileData` dans la configuration des destinations pour déterminer si les qualifications de profil historiques doivent être exportées vers votre destination.

| Paramètre | Type | Description |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booléen | Contrôle si les données de profil historiques sont exportées lorsque les segments sont activés vers la destination. <br> <ul><li> `true`: [!DNL Platform] envoie les profils utilisateur historiques qualifiés pour le segment avant l’activation du segment. </li><li> `false`: [!DNL Platform] inclut uniquement les profils utilisateur qui remplissent les critères pour le segment une fois le segment activé. </li></ul> |

## Comment cette configuration connecte toutes les informations nécessaires à votre destination {#connecting-all-configurations}

Certains de vos paramètres de destination doivent être configurés via le [serveur de destination](./server-and-template-configuration.md) ou le [configuration des métadonnées d’audience](./audience-metadata-management.md). La configuration de destination décrite ici connecte tous ces paramètres en référençant les deux autres configurations comme suit :

* Utilisez la variable `destinationServerId` pour référencer la configuration du serveur de destination et du modèle configurée pour votre destination.
* Utilisez la variable `audienceMetadataId` pour référencer la configuration des métadonnées d’audience configurée pour votre destination.