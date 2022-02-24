---
description: Cette page décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/credentials`.
title: Opérations de l’API du point d’entrée des informations d’identification
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: bc357e2e93b80edb5f7825bf2dee692f14bd7297
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 6%

---

# Opérations de l’API du point d’entrée des informations d’identification {#credentials}

>[!IMPORTANT]
>
>**Point de terminaison de l’API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du `/authoring/credentials` Point d’entrée de l’API.

Pour une description des fonctionnalités prises en charge par ce point de terminaison, lisez :

* [Configuration de destination de diffusion en continu](destination-configuration.md) pour la fonctionnalité que vous pouvez configurer pour les destinations de diffusion en continu.
* [Configuration des destinations basées sur des fichiers](file-based-destination-configuration.md) pour les fonctionnalités que vous pouvez configurer pour les destinations basées sur des fichiers.

## Quand utiliser la variable `/credentials` Point d’entrée API {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous *ne pas* Vous devez utiliser la variable `/credentials` Point d’entrée de l’API. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via le `customerAuthenticationConfigurations` des paramètres `/destinations` point de terminaison . Lecture [Configuration de l’authentification](./authentication-configuration.md#when-to-use) pour plus d’informations.

Utilisez ce point d’entrée API et sélectionnez `PLATFORM_AUTHENTICATION` dans le [configuration de destination](./destination-configuration.md#destination-delivery) s’il existe un système d’authentification global entre l’Adobe et votre destination et la variable [!DNL Platform] Le client n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide de la variable `/credentials` Point d’entrée de l’API.

## Prise en main des opérations de l’API de configuration des informations d’identification {#get-started}

Avant de poursuivre, veuillez consulter la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Création d’une configuration d’informations d’identification {#create}

Vous pouvez créer une configuration d’informations d’identification en adressant une requête de POST à la fonction `/authoring/credentials` point de terminaison .

**Format d’API**

```http
POST /authoring/credentials
```

**Requête**

La requête suivante crée une nouvelle configuration des informations d’identification, configurée par les paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par la fonction `/authoring/credentials` point de terminaison . Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

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
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `username` | Chaîne | Nom d’utilisateur de connexion de configuration des informations d’identification |
| `password` | Chaîne | Mot de passe de connexion de la configuration des informations d&#39;identification |
| `url` | Chaîne | URL du fournisseur d’autorisations |
| `clientId` | Chaîne | ID client des informations d’identification client/application |
| `clientSecret` | Chaîne | Secret client des informations d’identification client/application |
| `accessToken` | Chaîne | Jeton d’accès fourni par le fournisseur d’autorisations |
| `expiration` | Chaîne | Durée de vie du jeton d’accès |
| `refreshToken` | Chaîne | Jeton d’actualisation fourni par le fournisseur d’autorisations |
| `header` | Chaîne | Tout en-tête requis pour l’autorisation |
| `accessId` | Chaîne | Identifiant d’accès Amazon S3 |
| `secretKey` | Chaîne | Clé secrète Amazon S3 |
| `sshKey` | Chaîne | Clé SSH pour SFTP avec authentification SSH |
| `tenant` | Chaîne | Client de stockage Azure Data Lake |
| `servicePrincipalId` | Chaîne | Identifiant principal Azure Service pour Azure Data Lake Storage |
| `servicePrincipalKey` | Chaîne | Clé principale Azure Service pour Azure Data Lake Storage |
| `connectionString` | Chaîne | Chaîne de connexion de stockage Azure Blob |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration des informations d’identification que vous venez de créer.

## Répertorier les configurations des informations d’identification {#retrieve-list}

Vous pouvez récupérer une liste de toutes les configurations d’identification de votre organisation IMS en adressant une demande de GET à la fonction `/authoring/credentials` point de terminaison .

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

La réponse suivante renvoie un état HTTP 200 avec une liste des configurations d’informations d’identification auxquelles vous avez accès, en fonction de l’identifiant de l’organisation IMS et du nom de l’environnement de test que vous avez utilisés. One `instanceId` correspond au modèle pour une configuration des informations d’identification. La réponse est tronquée pour la concision.

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

Vous pouvez mettre à jour une configuration d’informations d’identification existante en adressant une requête de PUT à la fonction `/authoring/credentials` point de terminaison et en indiquant l’ID d’instance de la configuration des informations d’identification que vous souhaitez mettre à jour. Dans le corps de l’appel, indiquez la configuration des informations d’identification mises à jour.

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

Vous pouvez récupérer des informations détaillées sur une configuration d’informations d’identification spécifique en envoyant une demande de GET à la fonction `/authoring/credentials` point de terminaison et en indiquant l’ID d’instance de la configuration des informations d’identification que vous souhaitez mettre à jour.

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

Vous pouvez supprimer la configuration des informations d’identification spécifiées en adressant une requête de DELETE à la fonction `/authoring/credentials` point de terminaison et en indiquant l’identifiant de la configuration des informations d’identification que vous souhaitez supprimer dans le chemin d’accès de la requête.

**Format d’API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | Le `id` de la configuration des informations d’identification que vous souhaitez supprimer. |

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

Les points de terminaison de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Voir [Codes d’état d’API](../../landing/troubleshooting.md#api-status-codes) et [erreurs d’en-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant quand utiliser le point de terminaison des informations d’identification et comment configurer une configuration des informations d’identification à l’aide de la variable `/authoring/credentials` Point d’entrée de l’API ou `/authoring/destinations` point de terminaison . Lecture [comment utiliser la Destination SDK pour configurer votre destination](./configure-destination-instructions.md) pour comprendre où cette étape s’inscrit dans le processus de configuration de votre destination.
