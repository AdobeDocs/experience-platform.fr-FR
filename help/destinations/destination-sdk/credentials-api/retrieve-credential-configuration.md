---
description: Cette page illustre l’appel API utilisé pour récupérer une configuration d’informations d’identification via Adobe Experience Platform Destination SDK.
title: Récupération d’une configuration d’informations d’identification
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 29%

---


# Récupération d’une configuration d’informations d’identification

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page illustre la requête d’API et la charge utile que vous pouvez utiliser pour récupérer une configuration d’informations d’identification à l’aide de la variable `/authoring/credentials` Point d’entrée de l’API.

## Quand utiliser le point d’entrée de l’API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous ***ne devez pas*** utiliser le point d’entrée de l’API `/credentials`. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`.
> 
>Lecture [Configuration de l’authentification du client](../functionality/destination-configuration/customer-authentication.md) pour plus d’informations sur les types d’authentification pris en charge.

Utilisez ce point de terminaison d’API pour créer une configuration d’informations d’identification uniquement s’il existe un système d’authentification global entre l’Adobe et votre plateforme de destination, et que la variable [!DNL Platform] Le client n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer une configuration d’informations d’identification à l’aide de la fonction `/credentials` Point d’entrée de l’API.

Lorsque vous utilisez un système d’authentification global, vous devez définir `"authenticationRule":"PLATFORM_AUTHENTICATION"` dans le [diffusion de destination](../functionality/destination-configuration/destination-delivery.md) lors de la configuration [création d’une configuration de destination](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API de des informations d’identification {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Récupération d’une configuration d’informations d’identification {#retrieve}

Vous pouvez récupérer une [existant](create-credential-configuration.md) configuration des informations d’identification en effectuant une `GET` à la fonction `/authoring/credentials` point de terminaison .

**Format d’API**

Utilisez le format d’API suivant pour récupérer toutes les configurations d’informations d’identification pour votre compte.

```http
GET /authoring/credentials
```

Utilisez le format d’API suivant pour récupérer une configuration d’informations d’identification spécifique, définie par la variable `{INSTANCE_ID}` .

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Les deux requêtes suivantes récupèrent toutes les configurations d’identification pour votre organisation IMS, ou une configuration d’identification spécifique, selon que vous transmettez ou non la variable `INSTANCE_ID` dans la requête.

Sélectionnez chaque onglet ci-dessous pour afficher la charge utile correspondante.

>[!BEGINTABS]

>[!TAB Récupération de toutes les configurations d’informations d’identification]

+++Requête

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec une liste des configurations d’informations d’identification auxquelles vous avez accès, en fonction de la variable [!DNL IMS Org ID] et le nom de l’environnement de test que vous avez utilisé. One `instanceId` correspond à une configuration d’informations d’identification.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB Récupération d’une configuration d’informations d’identification spécifique]

+++Requête

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | L’identifiant de la configuration des informations d’identification que vous souhaitez récupérer. |

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration des informations d’identification correspondant à la variable `instanceId` fourni sur la requête.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment récupérer des détails sur vos configurations d’informations d’identification à l’aide de la variable `/authoring/credentials` Point d’entrée de l’API. Poursuivez votre apprentissage dans la section [Comment utiliser Destination SDK pour configurer votre destination](../guides/configure-destination-instructions.md) et obtenez une vue dʼensemble du processus de configuration de votre destination.
