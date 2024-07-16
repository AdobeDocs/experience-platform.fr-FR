---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Configuration des spécifications d’authentification pour les sources en libre-service (SDK par lots)
description: Ce document présente les configurations que vous devez préparer pour utiliser les sources en libre-service (SDK par lots).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 4%

---

# Configuration des spécifications d’authentification pour les sources en libre-service (SDK par lots)

Les spécifications d’authentification définissent la manière dont les utilisateurs de Adobe Experience Platform peuvent se connecter à votre source.

Le tableau `authSpec` contient des informations sur les paramètres d’authentification requis pour connecter une source à Platform. Toute source donnée peut prendre en charge plusieurs types d’authentification différents.

## Spécifications d’authentification

Les sources en libre-service (SDK par lots) prennent en charge les codes d’actualisation OAuth 2 et l’authentification de base. Consultez les tableaux ci-dessous pour obtenir des conseils sur l’utilisation d’un code d’actualisation OAuth 2 et l’authentification de base.

### Code d’actualisation OAuth 2

Un code d’actualisation OAuth 2 permet un accès sécurisé à une application en générant un jeton d’accès temporaire et un jeton d’actualisation. Le jeton d’accès vous permet d’accéder en toute sécurité à vos ressources sans avoir à fournir d’autres informations d’identification, tandis que le jeton d’actualisation vous permet de générer un nouveau jeton d’accès, une fois le jeton d’accès expiré.

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| Propriété | Description | Exemple |
| --- | --- | --- |
| `authSpec.name` | Affiche le nom du type d’authentification pris en charge. | `oAuth2-refresh-code` |
| `authSpec.type` | Définit le type d’authentification pris en charge par la source. | `oAuth2-refresh-code` |
| `authSpec.spec` | Contient des informations sur le schéma, le type de données et les propriétés de l’authentification. |
| `authSpec.spec.$schema` | Définit le schéma utilisé pour l’authentification. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Définit le type de données du schéma. | `object` |
| `authSpec.spec.properties` | Contient des informations sur les informations d’identification utilisées pour l’authentification. |
| `authSpec.spec.properties.description` | Affiche une brève description des informations d’identification. |
| `authSpec.spec.properties.type` | Définit le type de données des informations d’identification. | `string` |
| `authSpec.spec.properties.clientId` | ID client associé à votre application. L’ID client est utilisé conjointement avec votre secret client pour récupérer votre jeton d’accès. |
| `authSpec.spec.properties.clientSecret` | Le secret client associé à votre application. Le secret client est utilisé conjointement avec votre ID client pour récupérer votre jeton d’accès. |
| `authSpec.spec.properties.accessToken` | Le jeton d’accès autorise votre accès sécurisé à votre application. |
| `authSpec.spec.properties.refreshToken` | Le jeton d’actualisation est utilisé pour générer un nouveau jeton d’accès, à l’expiration du jeton d’accès. |
| `authSpec.spec.properties.expirationDate` | Définit la date d’expiration du jeton d’accès. |
| `authSpec.spec.properties.refreshTokenUrl` | URL utilisée pour récupérer votre jeton d’actualisation. |
| `authSpec.spec.properties.accessTokenUrl` | URL utilisée pour récupérer votre jeton d’actualisation. |
| `authSpec.spec.properties.requestParameterOverride` | Permet de spécifier les paramètres d’identification à remplacer lors de l’authentification. |
| `authSpec.spec.required` | Affiche les informations d’identification requises pour l’authentification. | `accessToken` |

{style="table-layout:auto"}


### Authentification de base

L’authentification de base est un type d’authentification qui vous permet d’accéder à votre application à l’aide d’une combinaison de votre nom d’utilisateur de compte et de votre mot de passe de compte.

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| Propriété | Description | Exemple |
| --- | --- | --- |
| `authSpec.name` | Affiche le nom du type d’authentification pris en charge. | `Basic Authentication` |
| `authSpec.type` | Définit le type d’authentification pris en charge par la source. | `BasicAuthentication` |
| `authSpec.spec` | Contient des informations sur le schéma, le type de données et les propriétés de l’authentification. |
| `authSpec.spec.$schema` | Définit le schéma utilisé pour l’authentification. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Définit le type de données du schéma. | `object` |
| `authSpec.spec.description` | Affiche des informations supplémentaires spécifiques à votre type d’authentification. |
| `authSpec.spec.properties` | Contient des informations sur les informations d’identification utilisées pour l’authentification. |
| `authSpec.spec.properties.username` | Nom d’utilisateur du compte associé à votre application. |
| `authSpec.spec.properties.password` | Mot de passe du compte associé à votre application. |
| `authSpec.spec.required` | Spécifie les champs requis en tant que valeurs obligatoires à saisir dans Platform. | `username` |

{style="table-layout:auto"}

## Exemple de spécification d’authentification

Voici un exemple de spécification d’authentification terminée utilisant une source [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md).

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

## Étapes suivantes

Une fois vos spécifications d’authentification renseignées, vous pouvez procéder à la configuration des spécifications source pour la source que vous souhaitez intégrer à Platform. Pour plus d’informations, consultez le document sur la [configuration des spécifications source](./sourcespec.md) .
