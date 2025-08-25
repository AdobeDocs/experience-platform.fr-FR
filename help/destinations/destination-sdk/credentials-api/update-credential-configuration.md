---
description: Cette page illustre l’appel API utilisé pour mettre à jour une configuration d’informations d’identification existante avec Adobe Experience Platform Destination SDK.
title: Mise à jour d’une configuration d’informations d’identification
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 90%

---

# Mise à jour d’une configuration d’informations d’identification

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour mettre à jour une configuration d’informations d’identification existante à l’aide du point d’entrée `/authoring/credentials` de l’API.

## Quand utiliser le point d’entrée de l’API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous ***ne devez pas*** utiliser le point d’entrée de l’API `/credentials`. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`.
> 
>Pour en savoir plus sur les types d’authentification pris en charge, consultez la documentation [Configuration de l’authentification du client](../functionality/destination-configuration/customer-authentication.md).

Utilisez ce point d’entrée de l’API pour créer une configuration d’informations d’identification uniquement s’il existe un système d’authentification global entre Adobe et votre plateforme de destination et si le client [!DNL Experience Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à la destination. Dans ce cas, vous devez créer une configuration d’informations d’identification à l’aide du point d’entrée `/credentials` de l’API.

Lors de l’utilisation d’un système d’authentification global, vous devez définir les `"authenticationRule":"PLATFORM_AUTHENTICATION"` dans la configuration [diffusion de destination](../functionality/destination-configuration/destination-delivery.md) lors de la [création d’une configuration de destination](../authoring-api/destination-configuration/create-destination-configuration.md). Ensuite, vous devez créer une [configuration des informations d’identification](../credentials-api/create-credential-configuration.md) et transmettre l’identifiant de l’objet d’identification dans le paramètre `authenticationId` de la configuration [diffusion de destination](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication).

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API des informations d’identification {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Mise à jour d’une configuration d’informations d’identification {#update}

Vous pouvez mettre à jour une configuration d’informations d’identification [existante](create-credential-configuration.md) en effectuant une requête `PUT` au point d’entrée `/authoring/credentials` avec la payload mise à jour.

Pour obtenir une configuration d’informations d’identification existante et son `{INSTANCE_ID}` correspondant, consultez l’article sur la [récupération d’une configuration d’informations d’identification](retrieve-credential-configuration.md).

**Format d’API**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration dʼinformations dʼidentification que vous souhaitez mettre à jour. Pour obtenir une configuration d’informations d’identification existante et son `{INSTANCE_ID}` correspondant, consultez la section [Récupération d’une configuration d’informations d’identification](retrieve-credential-configuration.md). |

Les requêtes suivantes mettent à jour des configurations d’informations d’identification, définies par les paramètres fournis dans la payload.

Sélectionnez chaque onglet ci-dessous pour afficher la payload correspondante.

>[!BEGINTABS]

>[!TAB De base]

**Mise à jour d’une configuration d’informations d’identification de base**

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `url` | Chaîne | URL du fournisseur d’autorisations |
| `username` | Chaîne | Nom d’utilisateur pour la configuration des informations d’identification |
| `password` | Chaîne | Mot de passe pour la configuration des informations d’identification |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration de vos informations d’identification mise à jour.

+++

>[!TAB Amazon S3]

**Mise à jour d’une configuration d’informations d’identification [!DNL Amazon S3]**

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `accessId` | Chaîne | Identifiant d’accès [!DNL Amazon S3] |
| `secretKey` | Chaîne | Clé secrète [!DNL Amazon S3] |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration de vos informations d’identification mise à jour.

+++

>[!TAB SSH]

**Mise à jour d’une configuration d’informations d’identification [!DNL SSH]**

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `username` | Chaîne | Nom d’utilisateur pour la configuration des informations d’identification |
| `sshKey` | Chaîne | Clé [!DNL SSH] pour [!DNL SFTP] avec l’authentication [!DNL SSH] |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration de vos informations d’identification mise à jour.

+++

>[!TAB Azure Data Lake Storage]

**Mise à jour d’une configuration d’informations d’identification [!DNL Azure Data Lake Storage]**

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `url` | Chaîne | URL du fournisseur d’autorisations |
| `tenant` | Chaîne | Client Azure Data Lake Storage |
| `servicePrincipalId` | Chaîne | Identifiant [!DNL Azure Service Principal] pour [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | Chaîne | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration de vos informations d’identification mise à jour.

+++

>[!TAB Stockage Azure Blob]

**Mise à jour d’une configuration d’informations d’identification [!DNL Azure Blob]**

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `connectionString` | Chaîne | chaîne de connexion [!DNL Azure Blob Storage] |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration de vos informations d’identification mise à jour.

+++

>[!ENDTABS]

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment mettre à jour une configuration d’informations d’identification à l’aide du point d’entrée `/authoring/credentials` de l’API. Consultez la documentation [Comment utiliser Destination SDK pour configurer la destination](../guides/configure-destination-instructions.md) afin de comprendre la place de cette étape dans le processus de configuration de la destination.
