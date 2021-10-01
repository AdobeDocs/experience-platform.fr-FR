---
description: Cette page décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/credentials`.
title: Opérations de l’API du point d’entrée des informations d’identification
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 6ff5fd0e80f7ca1015969e91cc23c88251509b61
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 6%

---

# Opérations de l’API du point d’entrée des informations d’identification {#credentials}

>[!IMPORTANT]
>
>**Point de terminaison de l’API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/credentials`.

## Quand utiliser le point d’entrée de l’API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous *ne devez pas* utiliser le point d’entrée de l’API `/credentials`. Vous pouvez plutôt configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point de terminaison `/destinations`. Pour plus d’informations, consultez [Configuration des informations d’identification](./credentials-configuration.md) .

Utilisez ce point de terminaison d’API et sélectionnez `PLATFORM_AUTHENTICATION` dans la [configuration de destination](./destination-configuration.md#destination-delivery) s’il existe un système d’authentification global entre l’Adobe et votre destination et que le client [!DNL Platform] n’a pas besoin de fournir d’informations d’identification d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide du point de terminaison de l’API `/credentials`.

<!--

Commenting out the example configurations

## Example configurations

**Example configuration for a Basic authentication credential configuration with username and password**

```json
{
  "type": "BASIC",
  "name": "YOUR_DESTINATION_NAME",
  "basicAuthentication": {
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "password": "YOUR_DESTINATION_SERVER_PASSWORD"
  }
}

```

**Example configuration for an OAuth2 credential configuration**

```json

{
  "oauth2AccessTokenAuthentication": {
    "accessToken": "YOUR_DESTINATION_SERVER_ACCESS_TOKEN",
    "expiration": "YOUR_TOKEN_TIME_TO_LIVE",
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "userId": "YOUR_DESTINATION_USER_ID",
    "url": "AUTHORIZATION_PROVIDER_URL",
    "header": "YOUR_AUTHORIZATION_HEADER"
  }
}

```

The sections below list out the necessary parameters for each authentication type. Let us know which authentication type your server uses and provide us with the relevant information for your server type.

## Basic authentication

|Parameter | Type | Description|
|---------|----------|------|
|`username` | String | credentials configuration login username |
|`password` | String | credentials configuration login password |



// commenting out this part as these types of authentication methods are not supported in phase one

### S3 authentication

|Parameter | Type | Description|
|---------|----------|------|
|accessId | String | credentials configuration S3 credential Access key ID |
|secretKey | String | credentials configuration S3 credential Secret key |

### SSH 

|Parameter | Type | Description|
|---------|----------|------|
|username | String | credentials configuration SSH username |
|SSHKey | String | credentials configuration SSH key |



## OAuth1

|Parameter | Type | Description|
|---------|----------|------|
|`apiKey` | String | A value used by the Destinations Service to identify itself to the Service Provider. |
|`apiSecret` | String | Secret used by the Destinations Service to establish ownership of the API key to the Service Provider. |
|`acccessToken` | String | A value used by the Destinations Service to gain access to the Protected Resources on behalf of the User |
|`tokenSecret` | String | A secret used by the Destinations Service to establish ownership of an access token. |

## OAuth2 user credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username` | String | The user's username to log on to your platform. |
|`password` | String | The user's password to log on to your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 client credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username`| String | URL of authorization provider |
|`password` | String | Any header required for authorization |

## OAuth2 access token

|Parameter | Type | Description|
|---------|----------|------|
|`accessToken` | String | Access token provided by the authorization provider |
|`expiration` | String | The time-to-live for the access token |
|`username` | String | The user's username to log on to your platform. |
|`userId` | String | The user's ID with your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 refresh token

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`refreshToken` | String | Refresh token provided by the authorization provider |
|`url` | String | URL of authorization provider |
|`expiration` | String | The time-to-live for the refresh token |
|`header` | String | Any header required for authorization |

-->

## Prise en main des opérations de l’API de configuration des informations d’identification {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Création d’une configuration d’informations d’identification {#create}

Vous pouvez créer une configuration d’informations d’identification en envoyant une requête de POST au point de terminaison `/authoring/credentials`.

**Format d’API**


```http
POST /authoring/credentials
```

**Requête**

La requête suivante crée une nouvelle configuration des informations d’identification, configurée par les paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point de terminaison `/authoring/credentials`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   }
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `username` | Chaîne | identification configuration nom d’utilisateur de connexion |
| `password` | Chaîne | identifiant de connexion |
| `url` | Chaîne | URL du fournisseur d’autorisations |
| `clientId` | Chaîne | ID client des informations d’identification client/application |
| `clientSecret` | Chaîne | Secret client des informations d’identification client/application |
| `accessToken` | Chaîne | Jeton d’accès fourni par le fournisseur d’autorisations |
| `expiration` | Chaîne | Durée de vie du jeton d’accès |
| `refreshToken` | Chaîne | Jeton d’actualisation fourni par le fournisseur d’autorisations |
| `header` | Chaîne | Tout en-tête requis pour l’autorisation |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration des informations d’identification que vous venez de créer.

## Répertorier les configurations des informations d’identification {#retrieve-list}

Vous pouvez récupérer une liste de toutes les configurations d’identification de votre organisation IMS en envoyant une requête GET au point de terminaison `/authoring/credentials` .

**Format d’API**


```http
GET /authoring/credentials
```

**Requête**

La requête suivante récupère la liste des configurations d’informations d’identification auxquelles vous avez accès, en fonction de la configuration de l’organisation IMS et de l’environnement de test.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse suivante renvoie un état HTTP 200 avec une liste des configurations d’informations d’identification auxquelles vous avez accès, en fonction de l’identifiant de l’organisation IMS et du nom de l’environnement de test que vous avez utilisés. Un `instanceId` correspond au modèle pour la configuration des informations d’identification. La réponse est tronquée pour la concision.

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## Mise à jour d’une configuration d’informations d’identification existante {#update}

Vous pouvez mettre à jour une configuration d’informations d’identification existante en envoyant une requête de PUT au point de terminaison `/authoring/credentials` et en fournissant l’ID d’instance de la configuration des informations d’identification que vous souhaitez mettre à jour. Dans le corps de l’appel, indiquez la configuration des informations d’identification mises à jour.

**Format d’API**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | L’identifiant de la configuration des informations d’identification que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour une configuration d’informations d’identification existante, configurée par les paramètres fournis dans la payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```





## Récupération d’une configuration d’informations d’identification spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une configuration d’informations d’identification spécifique en envoyant une demande de GET au point de terminaison `/authoring/credentials` et en fournissant l’ID d’instance de la configuration d’informations d’identification que vous souhaitez mettre à jour.

**Format d’API**


```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | L’identifiant de la configuration des informations d’identification que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la configuration des informations d’identification spécifiées.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```


## Suppression d’une configuration d’informations d’identification spécifique {#delete}

Vous pouvez supprimer la configuration des informations d’identification spécifiées en envoyant une requête de DELETE au point de terminaison `/authoring/credentials` et en fournissant l’identifiant de la configuration des informations d’identification que vous souhaitez supprimer dans le chemin d’accès de la requête.

**Format d’API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | `id` de la configuration des informations d’identification que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.

## Gestion des erreurs d’API

Les points d’entrée de l’API du SDK de destination suivent les principes généraux des messages d’erreur de l’API Experience Platform. Reportez-vous aux sections [Codes d’état d’API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) et [erreurs d’en-tête de requête](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant quand utiliser le point de terminaison des informations d’identification et comment configurer une configuration des informations d’identification à l’aide du point de terminaison de l’API `/authoring/credentials` ou du point de terminaison `/authoring/destinations`. Lisez la section [Comment utiliser le SDK de destination pour configurer votre destination](./configure-destination-instructions.md) afin de comprendre où cette étape correspond au processus de configuration de votre destination.
