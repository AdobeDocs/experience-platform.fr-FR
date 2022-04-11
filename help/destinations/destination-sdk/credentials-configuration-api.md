---
description: Cette page décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point d’entrée de l’API « /authoring/credentials ».
title: Opérations des paramètres d’identification de l’API
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: bc357e2e93b80edb5f7825bf2dee692f14bd7297
workflow-type: ht
source-wordcount: '797'
ht-degree: 100%

---

# Opérations des paramètres d’identification de l’API {#credentials}

>[!IMPORTANT]
>
>**Point dʼentrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page répertorie et décrit toutes les opérations de l’API que vous pouvez effectuer à l’aide du point d’entrée de l’API `/authoring/credentials`.

Pour une description des fonctionnalités prises en charge par ce point d’entrée, lisez :

* [Configuration de destination de diffusion](destination-configuration.md) pour la fonctionnalité que vous pouvez configurer pour les destinations de diffusion.
* [Configuration des destinations basées sur des fichiers](file-based-destination-configuration.md) pour les fonctionnalités que vous pouvez configurer pour les destinations basées sur des fichiers.

## Quand utiliser le point d’entrée de l’API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous ne devez *pas* utiliser le point d’entrée de l’API `/credentials`. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`. Lisez [Configuration de l’authentification](./authentication-configuration.md#when-to-use) pour plus d’informations.

Utilisez ce point d’entrée d’API et sélectionnez `PLATFORM_AUTHENTICATION` dans [configuration d’une destination](./destination-configuration.md#destination-delivery) s’il existe un système d’authentification global entre Adobe et votre destination et si le client [!DNL Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide du point d’entrée de l’API `/credentials`.

## Prise en main des opérations de l’API de configuration des informations d’identification {#get-started}

Avant de poursuivre, veuillez consulter la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Créer la configuration des informations d’identification {#create}

Vous pouvez créer une nouvelle configuration d’information d’identification en effectuant une requête POST vers le point d’entrée `/authoring/credentials`.

**Format d’API**

```http
POST /authoring/credentials
```

**Requête**

La requête suivante crée une nouvelle configuration d’information d’identification, configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point d’entrée `/authoring/credentials`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

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
| `username` | Chaîne | Nom d’utilisateur pour la configuration des informations d’identification |
| `password` | Chaîne | Mot de passe pour la configuration des informations d’identification |
| `url` | Chaîne | URL du fournisseur d’autorisations |
| `clientId` | Chaîne | Identifiant client des informations d’identification client/application |
| `clientSecret` | Chaîne | Secret client des informations d’identification client/application |
| `accessToken` | Chaîne | Jeton d’accès fourni par le fournisseur d’autorisations |
| `expiration` | Chaîne | Durée de vie du jeton d’accès |
| `refreshToken` | Chaîne | Actualiser le jeton fourni par le fournisseur d’autorisations |
| `header` | Chaîne | Tout en-tête requis pour l’autorisation |
| `accessId` | Chaîne | Identifiant d’accès Amazon S3 |
| `secretKey` | Chaîne | Clé secrète Amazon S3 |
| `sshKey` | Chaîne | Clé SSH pour SFTP avec authentification SSH |
| `tenant` | Chaîne | Client Azure Data Lake Storage |
| `servicePrincipalId` | Chaîne | Identifiant principal du service Azure pour Azure Data Lake Storage |
| `servicePrincipalKey` | Chaîne | Clé principale du service Azure pour Azure Data Lake Storage |
| `connectionString` | Chaîne | Chaîne de connexion de stockage dʼobjets Azure Blob |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

## Répertorier les configurations dʼinformations d’identification {#retrieve-list}

Vous pouvez obtenir une liste de toutes les configurations dʼinformations dʼidentification de votre organisation IMS en effectuant une requête GET vers le point de terminaison `/authoring/credentials`.

**Format d’API**


```http
GET /authoring/credentials
```

**Requête**

La requête suivante récupère la liste des configurations dʼinformations d’identification auxquelles vous avez accès, en fonction de lʼorganisation IMS et de la configuration de la sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse suivante renvoie un état HTTP 200 avec une liste des configurations dʼinformations d’identification auxquelles vous avez accès, en fonction de l’identifiant de l’organisation IMS et du nom de sandbox utilisés. Un champ `instanceId` correspond au modèle dʼune configuration dʼinformations d’identification. La réponse est tronquée à des fins de brièveté.

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

## Mettre à jour une configuration dʼinformations d’identification existante {#update}

Vous pouvez mettre à jour une configuration dʼinformations d’identification existante en effectuant une requête PUT au point de terminaison `/authoring/credentials` et en fournissant lʼidentifiant de lʼinstance de la configuration dʼinformations d’identification à mettre à jour. Dans le corps de l’appel, indiquez la configuration dʼinformations d’identification mise à jour.

**Format d’API**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration dʼinformations dʼidentification que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour une configuration dʼinformations d’identification existante, configurée par les paramètres fournis dans la payload.

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

## Récupérer une configuration dʼinformations d’identification spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une configuration dʼinformations d’identification spécifique en effectuant une requête GET au point de terminaison `/authoring/credentials` et en indiquant l’identifiant de l’instance de la configuration dʼinformations d’identification à mettre à jour.

**Format d’API**

```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration dʼinformations d’identification à récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la configuration dʼinformations dʼidentification spécifiée.

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

## Supprimer une configuration d’informations d’identification spécifique {#delete}

Vous pouvez supprimer une configuration dʼinformations dʼidentification spécifiée en effectuant une requête DELETE vers le point de terminaison `/authoring/credentials` et en fournissant l’identifiant de la configuration dʼinformations dʼidentification à supprimer dans le chemin d’accès de la requête.

**Format d’API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | Champ `id` de la configuration dʼinformations dʼidentification que vous souhaitez supprimer. |

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

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dans l’en-tête de la requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez quand utiliser le point de terminaison des informations d’identification et comment créer une configuration dʼinformations d’identification à l’aide du point de terminaison `/authoring/credentials` de l’API ou du point de terminaison `/authoring/destinations`. Poursuivez votre apprentissage dans la section [Comment utiliser Destination SDK pour configurer votre destination](./configure-destination-instructions.md) et obtenez une vue dʼensemble du processus de configuration de votre destination.
