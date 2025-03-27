---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Configurer les spécifications d’authentification pour les sources en libre-service (SDK par lots)
description: Ce document présente un aperçu des configurations que vous devez préparer pour utiliser des sources en libre-service (SDK par lots).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 984de21c134d2fc94ef7dc5f5e449f7a39732bc6
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 4%

---

# Configurer les spécifications d’authentification pour les sources en libre-service (SDK par lots)

Les spécifications d’authentification définissent la manière dont les utilisateurs de Adobe Experience Platform peuvent se connecter à votre source.

Le tableau `authSpec` contient des informations sur les paramètres d’authentification requis pour connecter une source à Platform. Toute source donnée peut prendre en charge plusieurs types d’authentification différents.

## Spécifications d’authentification

Les sources en libre-service (SDK par lots) prennent en charge les codes d’actualisation OAuth 2 et l’authentification de base. Consultez les tableaux ci-dessous pour obtenir des conseils sur l’utilisation d’un code d’actualisation OAuth 2 et de l’authentification de base

### Code d’actualisation OAuth 2

Un code d’actualisation OAuth 2 permet un accès sécurisé à une application en générant un jeton d’accès temporaire et un jeton d’actualisation. Le jeton d’accès vous permet d’accéder à vos ressources en toute sécurité sans avoir à fournir d’autres informations d’identification, tandis que le jeton d’actualisation vous permet de générer un nouveau jeton d’accès, une fois que le jeton d’accès expire.

+++Afficher un exemple de code d’actualisation OAuth 2

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
| `authSpec.spec.properties.clientId` | Identifiant client associé à votre application. L’identifiant client est utilisé conjointement avec votre secret client pour récupérer votre jeton d’accès. |
| `authSpec.spec.properties.clientSecret` | Secret client associé à votre application . Le secret client est utilisé conjointement avec votre identifiant client pour récupérer votre jeton d’accès. |
| `authSpec.spec.properties.accessToken` | Le jeton d’accès autorise l’accès sécurisé à votre application . |
| `authSpec.spec.properties.refreshToken` | Le jeton d’actualisation est utilisé pour générer un nouveau jeton d’accès, lorsque le jeton d’accès expire. |
| `authSpec.spec.properties.expirationDate` | Définit la date d’expiration du jeton d’accès. |
| `authSpec.spec.properties.refreshTokenUrl` | URL utilisée pour récupérer votre jeton d’actualisation. |
| `authSpec.spec.properties.accessTokenUrl` | URL utilisée pour récupérer votre jeton d’actualisation. |
| `authSpec.spec.properties.requestParameterOverride` | Permet de spécifier les paramètres d’identification à remplacer lors de l’authentification. |
| `authSpec.spec.required` | Affiche les informations d’identification requises pour l’authentification. | `accessToken` |

{style="table-layout:auto"}

+++

### Authentification de base

L’authentification de base est un type d’authentification qui vous permet d’accéder à votre application en utilisant une combinaison de votre nom d’utilisateur de compte et de votre mot de passe de compte.

+++ Afficher un exemple d’authentification de base

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
| `authSpec.spec.required` | Spécifie les champs requis en tant que valeurs obligatoires à saisir dans Experience Platform. | `username` |

{style="table-layout:auto"}

+++

### Authentification de la clé API {#api-key-authentication}

L’authentification par clé API est une méthode sécurisée pour accéder aux API en fournissant une clé API et d’autres paramètres d’authentification pertinents dans les requêtes. Selon vos informations d’API spécifiques, vous pouvez envoyer la clé API dans le cadre de l’en-tête, des paramètres de requête ou du corps de la requête.

Les paramètres suivants sont généralement requis lors de l’utilisation de l’authentification par clé API :

| Paramètre | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `host` | chaîne | Non | URL de la ressource. |
| `authKey1` | Chaîne | Oui | Première clé d’authentification requise pour l’accès à l’API. Elle est généralement envoyée dans l’en-tête de requête ou les paramètres de requête. |
| `authKey2` | Chaîne | Facultatif | Une deuxième clé d’authentification. Si nécessaire, cette clé est souvent utilisée pour valider davantage les requêtes. |
| `authKeyN` | Chaîne | Facultatif | Variable d’authentification supplémentaire qui peut être utilisée si nécessaire, à l’exception de l’API . |

{style="table-layout:auto"}

+++Afficher l’authentification de la clé API

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### Comportement d’authentification

Vous pouvez utiliser le paramètre `restAttributes` pour définir comment la clé API doit être incluse dans la requête. Par exemple, dans l’exemple ci-dessous, l’attribut `headerParamName` indique que le `X-Auth-Key1` doit être envoyé en tant qu’en-tête.

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

Chaque clé d’authentification (telle que `authKey1`, `authKey2`, etc.) peut être associée à `restAttributes` pour dicter la manière dont elles sont envoyées sous forme de requêtes.

Si `authKey1` a `"headerParamName": "X-Auth-Key1"`. Cela signifie que l’en-tête de la requête doit inclure `X-Auth-Key:{YOUR_AUTH_KEY1}`. De plus, le nom de la clé et le `headerParamName` ne doivent pas nécessairement être identiques. Par exemple :

* Le `authKey1` peut avoir des `headerParamName: X-Custom-Auth-Key`. Cela signifie que l’en-tête de la requête utilisera `X-Custom-Auth-Key` au lieu de `authKey1`.
* Inversement, `authKey1` peut avoir des `headerParamName: authKey1`. Cela signifie que le nom de l’en-tête de la requête reste inchangé.

**Exemple de format API**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## Exemple de spécification d’authentification

Voici un exemple de spécification d’authentification terminée à l’aide d’une source [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md).

+++Afficher un exemple de spécification d’authentification

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

+++

## Étapes suivantes

Une fois vos spécifications d’authentification renseignées, vous pouvez procéder à la configuration des spécifications de source pour la source que vous souhaitez intégrer à Platform. Pour plus d’informations, consultez le document sur la [configuration des spécifications de source](./sourcespec.md).
