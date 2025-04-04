---
description: Cette page illustre comment l’appel API est utilisé pour récupérer une configuration d’informations d’identification avec Adobe Experience Platform Destination SDK.
title: Récupération d’une configuration d’informations d’identification
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 96%

---

# Récupération d’une configuration d’informations d’identification

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour récupérer une configuration d’informations d’identification à l’aide du point d’entrée `/authoring/credentials` de l’API.

## Quand utiliser le point d’entrée de l’API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous ***ne devez pas*** utiliser le point d’entrée de l’API `/credentials`. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`.
> 
>Pour en savoir plus sur les types d’authentification pris en charge, consultez la documentation [Configuration de l’authentification du client](../functionality/destination-configuration/customer-authentication.md).

Utilisez ce point d’entrée de l’API pour créer une configuration d’informations d’identification uniquement s’il existe un système d’authentification global entre Adobe et votre plateforme de destination et si le client [!DNL Experience Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à la destination. Dans ce cas, vous devez créer une configuration d’informations d’identification à l’aide du point d’entrée `/credentials` de l’API.

Quand vous utilisez un système d’authentification global, vous devez définir `"authenticationRule":"PLATFORM_AUTHENTICATION"` dans la configuration de [diffusion de destination](../functionality/destination-configuration/destination-delivery.md) au moment de la [création d’une configuration de destination](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API des informations d’identification {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Récupération d’une configuration d’informations d’identification {#retrieve}

Vous pouvez récupérer une configuration d’informations d’identification [existante](create-credential-configuration.md) en effectuant une requête `GET` au point dʼentrée `/authoring/credentials`.

**Format d’API**

Utilisez le format d’API suivant pour récupérer toutes les configurations d’informations d’identification pour votre compte.

```http
GET /authoring/credentials
```

Utilisez le format d’API suivant pour récupérer une configuration d’informations d’identification spécifique, définie par le paramètre `{INSTANCE_ID}`.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Les deux requêtes suivantes récupèrent toutes les configurations d’informations d’identification pour votre organisation IMS ou une configuration d’informations d’identification spécifique, selon que vous transmettez ou non le paramètre `INSTANCE_ID` dans la requête.

Sélectionnez chaque onglet ci-dessous pour afficher la payload correspondante.

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

Une réponse réussie renvoie le statut HTTP 200 avec une liste de configurations d’informations d’identification auxquels vous avez accès en fonction de [!DNL IMS Org ID] et du nom du sandbox que vous avez utilisé. Un `instanceId` correspond à une configuration d’informations d’identification.

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

>[!TAB Récupération d’une configuration dʼinformations d’identification spécifique]

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
| `{INSTANCE_ID}` | Identifiant de la configuration dʼinformations d’identification à récupérer. |

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration d’informations d’identification correspondant à l’identifiant `instanceId` fourni pendant l’appel.

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

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment récupérer des détails sur la configuration de vos informations d’identification à l’aide du point d’entrée `/authoring/credentials` de l’API. Consultez la documentation [Comment utiliser Destination SDK pour configurer la destination](../guides/configure-destination-instructions.md) afin de comprendre la place de cette étape dans le processus de configuration de la destination.
