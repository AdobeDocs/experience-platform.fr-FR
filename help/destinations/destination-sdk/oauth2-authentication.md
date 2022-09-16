---
description: Cette page décrit les différents flux d’authentification OAuth 2 pris en charge par Destination SDK et fournit des instructions pour configurer l’authentification OAuth 2 pour votre destination.
title: Authentification OAuth 2
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 87fb3ffa65449b61e05d94d2b56daf727ecebdea
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 6%

---

# Authentification OAuth 2

## Présentation {#overview}

Utilisez la Destination SDK pour permettre à Adobe Experience Platform de se connecter à votre destination à l’aide du [Structure d’authentification OAuth 2](https://tools.ietf.org/html/rfc6749).

Cette page décrit les différents flux d’authentification OAuth 2 pris en charge par Destination SDK et fournit des instructions pour configurer l’authentification OAuth 2 pour votre destination.

## Comment ajouter des détails d’authentification OAuth 2 à votre configuration de destination {#how-to-setup}

### Conditions préalables dans votre système {#prerequisites}

Pour commencer, vous devez créer une application dans votre système pour Adobe Experience Platform ou enregistrer un Experience Platform dans votre système. L’objectif est de générer un ID client et un secret client, qui sont nécessaires pour authentifier l’Experience Platform sur votre destination. Dans le cadre de cette configuration de votre système, vous avez besoin des URL de redirection/rappel OAuth 2 de Adobe Experience Platform, que vous pouvez obtenir à partir de la liste ci-dessous.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>L’étape d’enregistrement d’une URL de redirection/rappel pour Adobe Experience Platform dans votre système n’est nécessaire que pour la variable [OAuth 2 avec code d’autorisation](./oauth2-authentication.md#authorization-code) type d’octroi. Pour les deux autres types d’octroi pris en charge (mot de passe et informations d’identification du client), vous pouvez ignorer cette étape.

À la fin de cette étape, vous devez disposer des éléments suivants :
* un ID client ;
* un secret client ;
* URL de rappel de l’Adobe (pour l’octroi du code d’autorisation).

### Ce que vous devez faire en Destination SDK {#to-do-in-destination-sdk}

Pour configurer l’authentification OAuth 2 pour votre destination dans Experience Platform, vous devez ajouter les détails OAuth 2 à la variable [configuration de destination](./destination-configuration.md), sous `customerAuthenticationConfigurations` en utilisant le paramètre `platform.adobe.io/data/core/activation/authoring/destinations` [Point d’entrée API](./destination-configuration-api.md). Voir [exemple de configuration](./destination-configuration.md#example-configuration). Vous trouverez ci-dessous des instructions spécifiques sur les champs à ajouter à votre modèle de configuration, en fonction de votre type d’octroi d’authentification OAuth 2.

## Types d’octroi OAuth 2 pris en charge {#oauth2-grant-types}

Experience Platform prend en charge les trois types de subventions OAuth 2 dans le tableau ci-dessous. Si vous disposez d’une configuration OAuth 2 personnalisée, Adobe peut la prendre en charge à l’aide de champs personnalisés de votre intégration. Pour plus d’informations, reportez-vous aux sections de chaque type d’octroi.

>[!IMPORTANT]
>
>* Vous fournissez les paramètres d’entrée comme indiqué dans les sections ci-dessous. Les systèmes internes d’Adobe se connectent au système d’authentification de votre plateforme et prennent les paramètres de sortie, qui sont utilisés pour authentifier l’utilisateur et maintenir l’authentification sur votre destination.
>* Les paramètres d’entrée mis en évidence en gras dans le tableau sont des paramètres requis dans le flux d’authentification OAuth 2. Les autres paramètres sont facultatifs. D’autres paramètres d’entrée personnalisés ne sont pas affichés ici, mais sont décrits en détail dans les sections . [Personnalisation de votre configuration OAuth 2](./oauth2-authentication.md#customize-configuration) et [Actualisation du jeton d’accès](./oauth2-authentication.md#access-token-refresh).


| Subvention OAuth 2 | Entrées | Sorties |
|---------|----------|---------|
| Code d’autorisation | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Mot de passe | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>mot de passe</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Informations d’identification client | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Le tableau ci-dessus répertorie les champs utilisés dans les flux OAuth 2 standard. Outre ces champs standard, diverses intégrations de partenaires peuvent nécessiter des entrées et des sorties supplémentaires. Adobe a conçu un framework d’authentification/d’autorisation OAuth 2 flexible pour la Destination SDK qui peut gérer des variations du modèle de champs standard ci-dessus, tout en prenant en charge un mécanisme pour générer automatiquement des sorties non valides, telles que des jetons d’accès expirés.

Dans tous les cas, la sortie comprend un jeton d’accès, utilisé par l’Experience Platform pour authentifier et maintenir l’authentification auprès de votre destination.

Le système que Adobe a conçu pour l’authentification OAuth 2 :
* Prend en charge les trois autorisations OAuth 2 tout en tenant compte des variations qu’elles comportent, telles que les champs de données supplémentaires, les appels d’API non standard, etc.
* Prend en charge les jetons d’accès avec des valeurs de durée de vie variables, qu’il s’agisse de 90 jours, 30 minutes ou de toute autre valeur de durée de vie que vous spécifiez.
* Prend en charge les flux d’autorisation OAuth 2 avec ou sans jetons d’actualisation.

## OAuth 2 avec code d’autorisation {#authorization-code}

Si votre destination prend en charge un flux de code d’autorisation OAuth 2.0 standard (lisez la section [Spécifications des normes RFC](https://tools.ietf.org/html/rfc6749#section-4.1)) ou une variante de celle-ci, consultez les champs obligatoires et facultatifs ci-dessous :

| Subvention OAuth 2 | Entrées | Sorties |
|---------|----------|---------|
| Code d’autorisation | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Pour configurer cette méthode d’authentification pour votre destination, ajoutez les lignes suivantes à votre configuration, dans la section `/destinations` [endpoint](./destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `authType` | Chaîne | Utilisez &quot;OAUTH2&quot;. |
| `grant` | Chaîne | Utilisez &quot;OAUTH2_AUTHORIZATION_CODE&quot;. |
| `accessTokenUrl` | Chaîne | URL de votre côté, qui émet des jetons d’accès et, éventuellement, actualise les jetons. |
| `authorizationUrl` | Chaîne | URL de votre serveur d’autorisations, dans lequel vous redirigez l’utilisateur pour qu’il se connecte à votre application. |
| `refreshTokenUrl` | Chaîne | *Facultatif.* URL de votre côté, qui émet des jetons d’actualisation. Souvent, la variable `refreshTokenUrl` est identique au `accessTokenUrl`. |
| `clientId` | Chaîne | ID client que votre système affecte à Adobe Experience Platform. |
| `clientSecret` | Chaîne | Secret client que votre système attribue à Adobe Experience Platform. |
| `scope` | Liste de chaînes | *Facultatif*. Définissez la portée de ce que le jeton d’accès permet à l’Experience Platform d’effectuer sur vos ressources. Exemple : &quot;lire, écrire&quot;. |

{style=&quot;table-layout:auto&quot;}

## OAuth 2 avec octroi de mot de passe

Pour l’octroi du mot de passe OAuth 2 (lisez la section [Spécifications des normes RFC](https://tools.ietf.org/html/rfc6749#section-4.3)), Experience Platform requiert le nom d’utilisateur et le mot de passe de l’utilisateur. Dans le flux d’authentification, l’Experience Platform échange ces informations d’identification pour un jeton d’accès et, éventuellement, un jeton d’actualisation.
Adobe utilise les entrées standard ci-dessous pour simplifier la configuration de destination, avec la possibilité de remplacer les valeurs :

| Subvention OAuth 2 | Entrées | Sorties |
|---------|----------|---------|
| Mot de passe | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>mot de passe</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> Vous n’avez pas besoin d’ajouter de paramètres pour `username` et `password` dans la configuration ci-dessous. Lorsque vous ajoutez `"grant": "OAUTH2_PASSWORD"` dans la configuration de destination, le système demande à l’utilisateur de fournir un nom d’utilisateur et un mot de passe dans l’interface utilisateur de l’Experience Platform, lorsqu’il s’authentifie à votre destination.

Pour configurer cette méthode d’authentification pour votre destination, ajoutez les lignes suivantes à votre configuration, dans la section `/destinations` [endpoint](./destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| Paramètre | Type | Description |
|---------|----------|------|
| `authType` | Chaîne | Utilisez &quot;OAUTH2&quot;. |
| `grant` | Chaîne | Utilisez &quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | Chaîne | URL de votre côté, qui émet des jetons d’accès et, éventuellement, actualise les jetons. |
| `clientId` | Chaîne | ID client que votre système affecte à Adobe Experience Platform. |
| `clientSecret` | Chaîne | Secret client que votre système attribue à Adobe Experience Platform. |
| `scope` | Liste de chaînes | *Facultatif*. Définissez la portée de ce que le jeton d’accès permet à l’Experience Platform d’effectuer sur vos ressources. Exemple : &quot;lire, écrire&quot;. |

{style=&quot;table-layout:auto&quot;}

## OAuth 2 avec octroi des informations d’identification du client

Vous pouvez configurer des informations d’identification du client OAuth 2 (lisez la section [Spécifications des normes RFC](https://tools.ietf.org/html/rfc6749#section-4.4)), qui prend en charge les entrées et sorties standard répertoriées ci-dessous. Vous pouvez personnaliser les valeurs. Voir [Personnalisation de votre configuration OAuth 2](./oauth2-authentication.md#customize-configuration) pour plus d’informations.

| Subvention OAuth 2 | Entrées | Sorties |
|---------|----------|---------|
| Informations d’identification client | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Pour configurer cette méthode d’authentification pour votre destination, ajoutez les lignes suivantes à votre configuration, dans la section `/destinations` [endpoint](./destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `authType` | Chaîne | Utilisez &quot;OAUTH2&quot;. |
| `grant` | Chaîne | Utilisez &quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | Chaîne | URL de votre serveur d’autorisations, qui émet un jeton d’accès et un jeton d’actualisation facultatif. |
| `refreshTokenUrl` | Chaîne | *Facultatif.* URL de votre côté, qui émet des jetons d’actualisation. Souvent, la variable `refreshTokenUrl` est identique au `accessTokenUrl`. |
| `clientId` | Chaîne | ID client que votre système affecte à Adobe Experience Platform. |
| `clientSecret` | Chaîne | Secret client que votre système attribue à Adobe Experience Platform. |
| `scope` | Liste de chaînes | *Facultatif*. Définissez la portée de ce que le jeton d’accès permet à l’Experience Platform d’effectuer sur vos ressources. Exemple : &quot;lire, écrire&quot;. |

{style=&quot;table-layout:auto&quot;}

## Personnalisation de votre configuration OAuth 2 {#customize-configuration}

Les configurations décrites dans les sections ci-dessus décrivent les subventions OAuth 2 standard. Cependant, le système conçu par Adobe offre une certaine flexibilité afin que vous puissiez utiliser des paramètres personnalisés pour n’importe quelle variante de l’octroi OAuth 2. Pour personnaliser les paramètres OAuth 2 standard, utilisez le `authenticationDataFields` , comme illustré dans les exemples ci-dessous.

### Exemple 1 : Utilisation `authenticationDataFields` pour capturer les informations provenant de la réponse d’authentification {#example-1}

Dans cet exemple, une plateforme de destination dispose de jetons d’actualisation qui expirent après un certain temps. Dans ce cas, le partenaire configure la variable `refreshTokenExpiration` champ personnalisé pour obtenir l’expiration du jeton d’actualisation à partir de la propriété `refresh_token_expires_in` dans la réponse de l’API.

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### Exemple 2 : Utilisation `authenticationDataFields` pour fournir un jeton d’actualisation spécial {#example-2}

Dans cet exemple, un partenaire configure sa destination pour fournir un jeton d’actualisation spécial. De plus, la date d’expiration des jetons d’accès n’est pas renvoyée dans la réponse de l’API. Ils peuvent donc coder en dur une valeur par défaut, ici 3 600 secondes.

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### Exemple 3 : L’utilisateur saisit l’ID client et le secret client lors de la configuration de la destination. {#example-3}

Dans cet exemple, au lieu de créer un ID client global et un secret client comme illustré dans la section [Conditions préalables dans votre système](./oauth2-authentication.md#prerequisites), le client doit saisir l’ID du client, le secret client et l’ID de compte (l’ID que le client utilise pour se connecter à la destination).

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



Vous pouvez utiliser les paramètres suivants dans `authenticationDataFields` pour personnaliser votre configuration OAuth 2 :

| Paramètre | Type | Description |
|---------|----------|------|
| `authenticationDataFields.name` | Chaîne | Nom du champ personnalisé. |
| `authenticationDataFields.title` | Chaîne | Titre que vous pouvez fournir pour le champ personnalisé. |
| `authenticationDataFields.description` | Chaîne | Description du champ de données personnalisé que vous configurez. |
| `authenticationDataFields.type` | Chaîne | Définit le type du champ de données personnalisé. <br> Valeurs acceptées : `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Booléen | Indique si le champ de données personnalisé est requis dans le flux d’authentification. |
| `authenticationDataFields.format` | Chaîne | Lorsque vous sélectionnez `"format":"password"`, Adobe chiffre la valeur du champ de données d’authentification. Utilisé avec `"fieldType": "CUSTOMER"`, cela masque également l’entrée dans l’interface utilisateur lorsque l’utilisateur saisit le champ . |
| `authenticationDataFields.fieldType` | Chaîne | Indique si l’entrée provient du partenaire (vous) ou de l’utilisateur, lorsqu’il configure votre destination dans Experience Platform. |
| `authenticationDataFields.value` | Chaîne. Booléen. Nombre entier | La valeur du champ de données personnalisé. La valeur correspond au type sélectionné parmi `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Chaîne | Indique le champ du chemin de réponse de l’API que vous référencez. |

{style=&quot;table-layout:auto&quot;}

## Actualisation du jeton d’accès {#access-token-refresh}

Adobe a conçu un système qui actualise les jetons d’accès expirés sans que l’utilisateur doive se reconnecter à votre plateforme. Le système peut générer un nouveau jeton afin que l’activation vers votre destination se poursuive de manière transparente pour le client.

Pour configurer l’actualisation du jeton d’accès, vous devrez peut-être configurer une requête HTTP modélisée qui permet à l’Adobe d’obtenir un nouveau jeton d’accès à l’aide d’un jeton d’actualisation. Si le jeton d’accès a expiré, Adobe accepte la demande modélisée que vous avez fournie, en ajoutant les paramètres que vous avez fournis. Utilisez la variable `accessTokenRequest` pour configurer un mécanisme d’actualisation du jeton d’accès.


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

Vous pouvez utiliser les paramètres suivants dans `accessTokenRequest` pour personnaliser votre processus d’actualisation de jeton :

| Paramètre | Type | Description |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Chaîne | Utilisez `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Chaîne | <ul><li>Utilisation `PEBBLE_V1` si vous utilisez des modèles pour la valeur dans `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Utilisation `NONE` si la valeur du champ `accessTokenRequest.urlBasedDestination.url.value` est une constante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Chaîne | URL dans laquelle l’Experience Platform demande le jeton d’accès. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Chaîne | <ul><li>Utilisation `PEBBLE_V1` si vous utilisez des modèles pour les valeurs de la variable `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Utilisation `NONE` si la valeur du champ `accessTokenRequest.httpTemplate.requestBody.value` est une constante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Chaîne | Utilisez le langage de modèle pour personnaliser les champs de la requête HTTP au point de terminaison du jeton d’accès. Pour plus d’informations sur l’utilisation du modèle pour personnaliser des champs, reportez-vous à la section [conventions de création de modèles](./oauth2-authentication.md#templating-conventions) . |
| `accessTokenRequest.httpTemplate.httpMethod` | Chaîne | Indique la méthode HTTP utilisée pour appeler votre point de terminaison de jeton d’accès. Dans la plupart des cas, cette valeur est `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Chaîne | Indique le type de contenu de l’appel HTTP au point de terminaison du jeton d’accès. <br> Par exemple : `application/x-www-form-urlencoded` ou `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Chaîne | Indique si des en-têtes doivent être ajoutés à l’appel HTTP au point de terminaison du jeton d’accès. |
| `accessTokenRequest.responseFields.templatingStrategy` | Chaîne | <ul><li>Utilisation `PEBBLE_V1` si vous utilisez des modèles pour les valeurs de la variable `accessTokenRequest.responseFields.value`.</li><li> Utilisation `NONE` si la valeur du champ `accessTokenRequest.responseFields.value` est une constante. </li></li> |
| `accessTokenRequest.responseFields.value` | Chaîne | Utilisez le langage de modèle pour accéder aux champs de la réponse HTTP à partir de votre point d’entrée de jeton d’accès. Pour plus d’informations sur l’utilisation du modèle pour personnaliser des champs, reportez-vous à la section [conventions de création de modèles](./oauth2-authentication.md#templating-conventions) . |
| `accessTokenRequest.validations.name` | Chaîne | Indique le nom que vous avez fourni pour cette validation. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Chaîne | <ul><li>Utilisation `PEBBLE_V1` si vous utilisez des modèles pour les valeurs de la variable `accessTokenRequest.validations.actualValue.value`.</li><li> Utilisation `NONE` si la valeur du champ `accessTokenRequest.validations.actualValue.value` est une constante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Chaîne | Utilisez le langage de modèle pour accéder aux champs de la réponse HTTP. Pour plus d’informations sur l’utilisation du modèle pour personnaliser des champs, reportez-vous à la section [conventions de création de modèles](./oauth2-authentication.md#templating-conventions) . |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Chaîne | <ul><li>Utilisation `PEBBLE_V1` si vous utilisez des modèles pour les valeurs de la variable `accessTokenRequest.validations.expectedValue.value`.</li><li> Utilisation `NONE` si la valeur du champ `accessTokenRequest.validations.expectedValue.value` est une constante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Chaîne | Utilisez le langage de modèle pour accéder aux champs de la réponse HTTP. Pour plus d’informations sur l’utilisation du modèle pour personnaliser des champs, reportez-vous à la section [conventions de création de modèles](./oauth2-authentication.md#templating-conventions) . |

{style=&quot;table-layout:auto&quot;}

## Conventions relatives aux modèles {#templating-conventions}

Selon la personnalisation de votre authentification, vous devrez peut-être accéder aux champs de données dans la réponse d’authentification, comme indiqué dans la section précédente. Pour ce faire, familiarisez-vous avec le [Langage de modèle de bloc](https://pebbletemplates.io/) utilisé par Adobe et reportez-vous aux conventions de création de modèles ci-dessous pour personnaliser votre implémentation OAuth 2.


| Préfixe | Description | Exemple |
|---------|----------|---------|
| authData | Accédez à la valeur d’un champ de données de partenaire ou de client. | ``{{ authData.accessToken }}`` |
| response.body | Corps de réponse HTTP | ``{{ response.body.access_token }}`` |
| response.status | Statut de réponse HTTP | ``{{ response.status }}`` |
| response.headers | En-têtes de réponse HTTP | ``{{ response.headers.server[0] }}`` |
| userContext | Accès aux informations sur la tentative d’authentification actuelle | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authentication attempt `</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Étapes suivantes {#next-steps}

En lisant cet article, vous comprenez maintenant les modèles d’authentification OAuth 2 pris en charge par Adobe Experience Platform et vous savez comment configurer votre destination avec la prise en charge de l’authentification OAuth 2. Ensuite, vous pouvez configurer votre destination OAuth 2 prise en charge à l’aide de Destination SDK. Lecture [Utiliser la Destination SDK pour configurer votre destination](./configure-destination-instructions.md) pour les étapes suivantes.
