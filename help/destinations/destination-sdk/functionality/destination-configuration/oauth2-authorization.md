---
description: Cette page décrit les différents flux d’autorisation OAuth 2 pris en charge par Destination SDK et fournit des instructions pour configurer l’autorisation OAuth 2 pour la destination.
title: Autorisation OAuth 2
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 78%

---


# Autorisation OAuth 2

Destination SDK prend en charge plusieurs méthodes d’autorisation pour la destination. Parmi celles-ci, vous pouvez vous authentifier à la destination en utilisant le cadre d’autorisation [OAuth 2](https://tools.ietf.org/html/rfc6749).

Cette page décrit les différents flux d’autorisation OAuth 2 pris en charge par Destination SDK et fournit des instructions pour configurer l’autorisation OAuth 2 pour la destination.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Pour en savoir plus sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page, consultez le tableau ci-dessous.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (streaming) | Oui |
| Intégrations basées sur des fichiers (par lots) | Non |

## Comment ajouter des détails d’autorisation OAuth 2 à votre configuration de destination {#how-to-setup}

### Conditions préalables dans votre système {#prerequisites}

Pour commencer, vous devez créer une application dans votre système pour Adobe Experience Platform ou enregistrer Experience Platform dans votre système. L’objectif est de générer un identifiant client et un secret client, qui sont nécessaires pour authentifier Experience Platform à la destination.

Dans le cadre de cette configuration, vous avez besoin des adresses URL de redirection/rappel OAuth 2 d’Adobe Experience Platform, que vous pouvez obtenir à partir de la liste ci-dessous.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-can2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-gbr9.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>L’étape d’enregistrement d’une URL de redirection/rappel pour Adobe Experience Platform dans votre système n’est obligatoire que pour le type d’octroi [OAuth 2 avec code d’autorisation](#authorization-code). Pour les deux autres types d’octrois pris en charge (mot de passe et informations d’identification du client), vous pouvez ignorer cette étape.

À la fin de cette étape, vous devez disposer des éléments suivants :

* un identifiant client ;
* un secret client ;
* une URL de rappel d’Adobe (pour l’octroi du code d’autorisation).

### À faire dans Destination SDK {#to-do-in-destination-sdk}

Pour configurer l’autorisation OAuth 2 pour la destination dans Experience Platform, vous devez ajouter les détails OAuth 2 à la [configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md), sous le paramètre `customerAuthenticationConfigurations` . Pour obtenir des exemples détaillés, consultez l’[authentification du client](../../functionality/destination-configuration/customer-authentication.md). Vous trouverez ci-dessous des instructions spécifiques sur les champs à ajouter à votre modèle de configuration, en fonction de votre type d’octroi d’autorisation OAuth 2.

## Types d’octroi OAuth 2 pris en charge {#oauth2-grant-types}

Experience Platform prend en charge les trois types de subventions OAuth 2 dans le tableau ci-dessous. Si vous disposez d’une configuration OAuth 2 personnalisée, Adobe peut la prendre en charge à l’aide de champs personnalisés de votre intégration. Pour plus d’informations, consultez les sections de chaque type d’octroi.

>[!IMPORTANT]
>
>* Vous devez fournir les paramètres d’entrée comme indiqué dans les sections ci-dessous. Les systèmes internes à Adobe se connectent au système d’autorisation de votre plateforme et prennent les paramètres de sortie pour authentifier l’utilisateur et maintenir l’autorisation sur la destination.
>* Les paramètres d’entrée mis en surbrillance en gras dans le tableau sont des paramètres obligatoires dans le flux d’autorisation OAuth 2. Les autres paramètres sont facultatifs. D’autres paramètres d’entrée personnalisés ne sont pas affichés ici, mais sont décrits en détail dans les sections [Personnalisation de votre configuration OAuth 2](#customize-configuration) et [Actualisation du jeton d’accès](#access-token-refresh).

| Octroi OAuth 2 | Entrées | Sorties |
|---------|----------|---------|
| Code d’autorisation | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Mot de passe | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Informations d’identification client | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Le tableau ci-dessus répertorie les champs utilisés dans les flux OAuth 2 standard. Outre ces champs standard, diverses intégrations de partenaires peuvent demander des entrées et des sorties supplémentaires. Adobe a conçu un framework d’autorisation OAuth 2 flexible pour Destination SDK qui peut gérer des variations du modèle de champs standard ci-dessus, tout en prenant en charge un mécanisme pour générer automatiquement des sorties non valides, telles que des jetons d’accès expirés.

Dans tous les cas, la sortie comprend un jeton d’accès, qui est utilisé par Experience Platform pour authentifier et gérer l’autorisation vers la destination.

Le système qu’Adobe a conçu pour l’autorisation OAuth 2 :

* prend en charge les trois autorisations OAuth 2 tout en tenant compte des variations qu’elles comportent, telles que les champs de données supplémentaires, les appels API non standard, etc. ;
* prend en charge les jetons d’accès avec des valeurs de durée de vie variables, qu’il s’agisse de 90 jours, 30 minutes ou de toute autre valeur de durée de vie que vous spécifiez ;
* prend en charge les flux d’autorisation OAuth 2 avec ou sans jetons d’actualisation.

## OAuth 2 avec code d’autorisation {#authorization-code}

Si la destination prend en charge un flux de code d’autorisation OAuth 2.0 standard (lisez la section [Spécifications des normes RFC](https://tools.ietf.org/html/rfc6749#section-4.1)) ou une variante de celle-ci, consultez les champs obligatoires et facultatifs ci-dessous :

| Octroi OAuth 2 | Entrées | Sorties |
|---------|----------|---------|
| Code d’autorisation | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Pour configurer cette méthode d’autorisation pour la destination, ajoutez les lignes suivantes à votre configuration au moment de la [création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md) :

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
| `authType` | Chaîne | Utilisez « OAUTH2 ». |
| `grant` | Chaîne | Utilisez « OAUTH2_AUTHORIZATION_CODE ». |
| `accessTokenUrl` | Chaîne | URL de votre côté qui émet des jetons d’accès et, éventuellement, actualise les jetons. |
| `authorizationUrl` | Chaîne | URL de votre serveur d’autorisation, dans lequel vous redirigez l’utilisateur pour qu’il se connecte à votre application. |
| `refreshTokenUrl` | Chaîne | *Facultatif.* URL de votre côté, qui émet des jetons d’actualisation. Souvent, l’URL de jeton d’actualisation `refreshTokenUrl` est identique à l’URL de jeton d’accès `accessTokenUrl`. |
| `clientId` | Chaîne | L’identifiant client que votre système attribue à Adobe Experience Platform. |
| `clientSecret` | Chaîne | Le secret client que votre système attribue à Adobe Experience Platform. |
| `scope` | Liste de chaînes | *Facultatif*. Définissez la portée de ce que le jeton d’accès permet à Experience Platform d’effectuer sur vos ressources. Exemple : « lire, écrire ». |

{style="table-layout:auto"}

## OAuth 2 avec octroi de mot de passe

Pour octroyer le mot de passe OAuth 2 (lisez la section [Spécifications des normes RFC](https://tools.ietf.org/html/rfc6749#section-4.3)), Experience Platform demande le nom d’utilisateur et le mot de passe de l’utilisateur. Dans le flux d’autorisation, Experience Platform échange ces informations d’identification contre un jeton d’accès et, éventuellement, un jeton d’actualisation.
Adobe utilise les entrées standard ci-dessous pour simplifier la configuration de destination, avec la possibilité de remplacer des valeurs :

| Octroi OAuth 2 | Entrées | Sorties |
|---------|----------|---------|
| Mot de passe | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> Vous n’avez pas besoin d’ajouter de paramètres pour `username` et `password` dans la configuration ci-dessous. Quand vous ajoutez `"grant": "OAUTH2_PASSWORD"` dans la configuration de destination, le système demande à l’utilisateur de fournir un nom d’utilisateur et un mot de passe dans l’interface utilisateur d’Experience Platform, quand il s’authentifie à la destination.

Pour configurer cette méthode d’autorisation pour la destination, ajoutez les lignes suivantes à votre configuration au moment de la [création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md) :

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
| `authType` | Chaîne | Utilisez « OAUTH2 ». |
| `grant` | Chaîne | Utilisez « OAUTH2_PASSWORD ». |
| `accessTokenUrl` | Chaîne | URL de votre côté qui émet des jetons d’accès et, éventuellement, actualise les jetons. |
| `clientId` | Chaîne | L’identifiant client que votre système attribue à Adobe Experience Platform. |
| `clientSecret` | Chaîne | Le secret client que votre système attribue à Adobe Experience Platform. |
| `scope` | Liste de chaînes | *Facultatif*. Définissez la portée de ce que le jeton d’accès permet à Experience Platform d’effectuer sur vos ressources. Exemple : « lire, écrire ». |

{style="table-layout:auto"}

## OAuth 2 avec octroi dʼinformations d’identification du client

Vous pouvez configurer des informations d’identification du client OAuth 2 (consultez la section [Spécifications des normes RFC](https://tools.ietf.org/html/rfc6749#section-4.4)), qui prend en charge les entrées et sorties standard répertoriées ci-dessous. Vous pouvez personnaliser les valeurs. Pour en savoir plus, consultez la section [Personnaliser votre configuration OAuth 2](#customize-configuration).

| Octroi OAuth 2 | Entrées | Sorties |
|---------|----------|---------|
| Informations d’identification client | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>portée</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Pour configurer cette méthode d’autorisation pour la destination, ajoutez les lignes suivantes à votre configuration au moment de la [création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md) :

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
| `authType` | Chaîne | Utilisez « OAUTH2 ». |
| `grant` | Chaîne | Utilisez « OAUTH2_CLIENT_CREDENTIALS ». |
| `accessTokenUrl` | Chaîne | URL du serveur d’autorisations, qui émet un jeton d’accès et un jeton d’actualisation facultatif. |
| `refreshTokenUrl` | Chaîne | *Facultatif.* URL de votre côté, qui émet des jetons d’actualisation. Souvent, l’URL de jeton d’actualisation `refreshTokenUrl` est identique à l’URL de jeton d’accès `accessTokenUrl`. |
| `clientId` | Chaîne | L’identifiant client que votre système attribue à Adobe Experience Platform. |
| `clientSecret` | Chaîne | Le secret client que votre système attribue à Adobe Experience Platform. |
| `scope` | Liste de chaînes | *Facultatif*. Définissez la portée de ce que le jeton d’accès permet à Experience Platform d’effectuer sur vos ressources. Exemple : « lire, écrire ». |

{style="table-layout:auto"}

## Personnalisation de votre configuration OAuth 2 {#customize-configuration}

Les configurations décrites dans les sections ci-dessus décrivent les octrois OAuth 2 standard. Cependant, le système conçu par Adobe offre une certaine flexibilité afin de vous permettre d’utiliser des paramètres personnalisés pour n’importe quelle variante de l’octroi OAuth 2. Pour personnaliser les paramètres OAuth 2 standard, utilisez les paramètres `authenticationDataFields`, comme illustrés dans les exemples ci-dessous.

### Exemple 1 : utilisation de `authenticationDataFields` pour capturer des informations provenant de la réponse d’autorisation {#example-1}

Dans cet exemple, une plateforme de destination dispose de jetons d’actualisation qui expirent après un certain temps. Dans ce cas, le partenaire configure le champ personnalisé `refreshTokenExpiration` pour obtenir l’expiration du jeton d’actualisation à partir du champ `refresh_token_expires_in` dans la réponse de l’API.

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

### Exemple 2 : utilisation de `authenticationDataFields` pour fournir un jeton d’actualisation spécial {#example-2}

Dans cet exemple, un partenaire configure sa destination pour fournir un jeton d’actualisation spécial. En outre, la date d’expiration des jetons d’accès n’est pas renvoyée dans la réponse de l’API. Une valeur par défaut, ici 3 600 secondes, peut donc être codée en dur.

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

### Exemple 3 : l’utilisateur saisit l’identifiant et le secret client au moment de la configuration de la destination {#example-3}

Dans cet exemple, au lieu de créer un identifiant client global et un secret client comme illustré dans la section [Conditions préalables dans votre système](#prerequisites), le client doit saisir l’identifiant du client, le secret client et l’identifiant de compte (l’identifiant que le client utilise pour se connecter à la destination)

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



Vous pouvez utiliser les paramètres suivants dans `authenticationDataFields` pour personnaliser votre configuration OAuth 2 :

| Paramètre | Type | Description |
|---------|----------|------|
| `authenticationDataFields.name` | Chaîne | Nom du champ personnalisé. |
| `authenticationDataFields.title` | Chaîne | Titre que vous pouvez donner au champ personnalisé. |
| `authenticationDataFields.description` | Chaîne | Description du champ de données personnalisé que vous configurez. |
| `authenticationDataFields.type` | Chaîne | Définit le type du champ de données personnalisé. <br> Valeurs acceptées : `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Booléen | Indique si le champ de données personnalisé est obligatoire dans le flux d’autorisation. |
| `authenticationDataFields.format` | Chaîne | Lorsque vous sélectionnez `"format":"password"`, Adobe chiffre la valeur du champ de données d’autorisation. Utilisé avec `"fieldType": "CUSTOMER"`, cela masque également l’entrée dans l’interface utilisateur quand l’utilisateur saisit le champ. |
| `authenticationDataFields.fieldType` | Chaîne | Indique si l’entrée provient du partenaire (vous) ou de l’utilisateur, quand il configure la destination dans Experience Platform. |
| `authenticationDataFields.value` | Chaîne. Booléen. Nombre entier | Valeur du champ de données personnalisé. La valeur correspond au type sélectionné parmi `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Chaîne | Indique le champ du chemin de réponse de l’API que vous référencez. |

{style="table-layout:auto"}

## Actualisation du jeton d’accès {#access-token-refresh}

Adobe a conçu un système qui actualise les jetons d’accès expirés sans demander à l’utilisateur de se reconnecter à la plateforme. Le système peut générer un nouveau jeton afin de faciliter l’activation vers la destination pour le client.

Pour configurer l’actualisation du jeton d’accès, vous devrez peut-être configurer une requête HTTP modélisée qui permet à Adobe d’obtenir un nouveau jeton d’accès à l’aide d’un jeton d’actualisation. Si le jeton d’accès a expiré, Adobe accepte votre requête modélisée, en ajoutant les paramètres que vous avez fournis. Utilisez le paramètre `accessTokenRequest` pour configurer un mécanisme d’actualisation du jeton d’accès.


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

Vous pouvez utiliser les paramètres suivants dans `accessTokenRequest` pour personnaliser votre processus d’actualisation du jeton d’accès :

| Paramètre | Type | Description |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Chaîne | Utilisez `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Chaîne | <ul><li>Utilisez `PEBBLE_V1` si vous utilisez des modèles pour la valeur dans `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Utilisez `NONE` si la valeur du champ `accessTokenRequest.urlBasedDestination.url.value` est une constante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Chaîne | URL dans laquelle Experience Platform demande le jeton d’accès. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Chaîne | <ul><li>Utilisez `PEBBLE_V1` si vous utilisez des modèles pour les valeurs dans `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Utilisez `NONE` si la valeur du champ `accessTokenRequest.httpTemplate.requestBody.value` est une constante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Chaîne | Utilisez le langage de modèle pour personnaliser les champs de la requête HTTP vers le point d’entrée du jeton d’accès. Pour plus d’informations sur l’utilisation du modèle pour personnaliser des champs, consultez la section [Conventions de création de modèles](#templating-conventions). |
| `accessTokenRequest.httpTemplate.httpMethod` | Chaîne | Indique la méthode HTTP utilisée pour appeler votre point d’entrée de jeton d’accès. Dans la plupart des cas, cette valeur est `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Chaîne | Indique le type de contenu de l’appel HTTP au point d’entrée du jeton d’accès. <br> Par exemple, `application/x-www-form-urlencoded` ou `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Chaîne | Indique si des en-têtes doivent être ajoutés à l’appel HTTP vers le point d’entrée du jeton d’accès. |
| `accessTokenRequest.responseFields.templatingStrategy` | Chaîne | <ul><li>Utilisez `PEBBLE_V1` si vous utilisez des modèles pour les valeurs dans `accessTokenRequest.responseFields.value`.</li><li> Utilisez `NONE` si la valeur du champ `accessTokenRequest.responseFields.value` est une constante. </li></li> |
| `accessTokenRequest.responseFields.value` | Chaîne | Utilisez le langage de modèle pour accéder aux champs d’accès de la réponse HTTP depuis votre point d’entrée du jeton d’accès. Pour plus d’informations sur l’utilisation du modèle pour personnaliser des champs, consultez la section [Conventions de création de modèles](#templating-conventions). |
| `accessTokenRequest.validations.name` | Chaîne | Indique le nom que vous avez fourni pour cette validation. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Chaîne | <ul><li>Utilisez `PEBBLE_V1` si vous utilisez des modèles pour les valeurs dans `accessTokenRequest.validations.actualValue.value`.</li><li> Utilisez `NONE` si la valeur du champ `accessTokenRequest.validations.actualValue.value` est une constante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Chaîne | Utilisez le langage de modèle pour accéder aux champs de la réponse HTTP. Pour plus d’informations sur l’utilisation du modèle pour personnaliser des champs, consultez la section [Conventions de création de modèles](#templating-conventions). |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Chaîne | <ul><li>Utilisez `PEBBLE_V1` si vous utilisez des modèles pour les valeurs dans `accessTokenRequest.validations.expectedValue.value`.</li><li> Utilisez `NONE` si la valeur du champ `accessTokenRequest.validations.expectedValue.value` est une constante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Chaîne | Utilisez le langage de modèle pour accéder aux champs de la réponse HTTP. Pour plus d’informations sur l’utilisation du modèle pour personnaliser des champs, consultez la section [Conventions de création de modèles](#templating-conventions). |

{style="table-layout:auto"}

## Conventions relatives aux modèles {#templating-conventions}

Selon la personnalisation de votre autorisation, vous devrez peut-être accéder aux champs de données dans la réponse d’autorisation, comme indiqué dans la section précédente. Pour ce faire, familiarisez-vous avec le [langage de modèle Pebble](https://pebbletemplates.io/) utilisé par Adobe et consultez les conventions de création de modèles ci-dessous pour personnaliser votre implémentation OAuth 2.


| Préfixe | Description | Exemple |
|---------|----------|---------|
| authData | Accédez à la valeur d’un champ de données de partenaire ou de client. | `{{ authData.accessToken }}` |
| response.body | Corps de réponse HTTP | `{{ response.body.access_token }}` |
| response.status | Statut de réponse HTTP | `{{ response.status }}` |
| response.headers | En-têtes de réponse HTTP | `{{ response.headers.server[0] }}` |
| userContext | Accéder aux informations sur la tentative d’autorisation actuelle | <ul><li>`{{ userContext.sandboxName }}`</li><li>`{{ userContext.sandboxId }}`</li><li>`{{ userContext.imsOrgId }}`</li><li>`{{ userContext.client }} // the client executing the authorization attempt`</li></ul> |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

En lisant cet article, vous avez maintenant une compréhension des modèles d’autorisation OAuth 2 pris en charge par Adobe Experience Platform et vous savez comment configurer la destination avec la prise en charge de l’autorisation OAuth 2. Vous pouvez désormais configurer la destination avec prise en charge d’OAuth 2 à l’aide de Destination SDK. Pour connaître les étapes suivantes, consultez la documentation [Utilisation de Destination SDK pour configurer la destination](../../guides/configure-destination-instructions.md).
