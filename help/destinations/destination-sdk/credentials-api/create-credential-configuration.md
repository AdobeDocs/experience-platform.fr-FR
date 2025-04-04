---
description: Cette page illustre comment l’appel API est utilisé pour créer une configuration d’informations d’identification avec Adobe Experience Platform Destination SDK.
title: Création d’une configuration d’informations d’identification
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 97%

---

# Création d’une configuration d’informations d’identification

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour créer une configuration d’informations d’identification à l’aide du point d’entrée de l’API `/authoring/credentials`.

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

## Créer la configuration des informations d’identification {#create}

Vous pouvez créer une configuration d’informations d’identification en effectuant une requête `POST` vers le point d’entrée `/authoring/credentials`.

**Format d’API**

```http
POST /authoring/credentials
```

Les requêtes suivantes créent des configurations d’informations d’identification, définies par les paramètres fournis dans la payload.

Sélectionnez chaque onglet ci-dessous pour afficher la payload correspondante.

>[!BEGINTABS]

>[!TAB De base]

**Création d’une configuration d’informations d’identification de base**

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!TAB Amazon S3]

**Création d’une configuration d’informations d’identification [!DNL Amazon S3]**

+++**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!TAB SSH]

**Création d’une configuration d’informations d’identification SSH**

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
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
| `sshKey` | Chaîne | Clé SSH pour SFTP avec authentification SSH |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!TAB Azure Data Lake Storage]

**Création d’une configuration d’informations d’identification [!DNL Azure Data Lake Storage]**

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
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
| `servicePrincipalId` | Chaîne | Identifiant principal du service Azure pour Azure Data Lake Storage |
| `servicePrincipalKey` | Chaîne | Clé principale du service Azure pour Azure Data Lake Storage |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!TAB Stockage Azure Blob]

**Création d’une configuration d’informations d’identification [!DNL Azure Blob Storage]**

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!ENDTABS]

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez quand utiliser le point d’entrée des informations d’identification et comment configurer les informations d’identification à l’aide du point d’entrée `/authoring/credentials` de l’API. Découvrez [comment utiliser Destination SDK pour configurer la destination](../guides/configure-destination-instructions.md) afin de comprendre la place de cette étape dans le processus de configuration de la destination.
