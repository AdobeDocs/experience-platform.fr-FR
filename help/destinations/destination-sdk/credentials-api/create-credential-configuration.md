---
description: Cette page illustre l’appel API utilisé pour créer un Adobe Experience Platform Destination SDK de configuration des informations d’identification.
title: Création d’une configuration d’informations d’identification
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 50%

---


# Création d’une configuration d’informations d’identification

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page illustre la requête d’API et la charge utile que vous pouvez utiliser pour créer une configuration d’informations d’identification à l’aide de la variable `/authoring/credentials` Point d’entrée de l’API.

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

Avant de poursuivre, veuillez consulter la section [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Créer la configuration des informations d’identification {#create}

Vous pouvez créer une configuration d’informations d’identification en effectuant une `POST` à la fonction `/authoring/credentials` point de terminaison .

**Format d’API**

```http
POST /authoring/credentials
```

Les requêtes suivantes créent de nouvelles configurations d’informations d’identification, définies par les paramètres fournis dans le payload.

Sélectionnez chaque onglet ci-dessous pour afficher la charge utile correspondante.

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

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!TAB Amazon S3]

**Créez un [!DNL Amazon S3] configuration des informations d’identification**

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
| `accessId` | Chaîne | [!DNL Amazon S3] ID d’accès |
| `secretKey` | Chaîne | [!DNL Amazon S3] clé secrète |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

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

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!TAB Stockage du lac de données Azure]

**Créez un [!DNL Azure Data Lake Storage] configuration des informations d’identification**

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

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!TAB Stockage Azure Blob]

**Créez un [!DNL Azure Blob Storage] configuration des informations d’identification**

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
| `connectionString` | Chaîne | [!DNL Azure Blob Storage] chaîne de connexion |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration dʼinformations dʼidentification que vous venez de créer.

+++

>[!ENDTABS]

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant quand utiliser le point de terminaison des informations d’identification et comment configurer une configuration des informations d’identification à l’aide de la variable `/authoring/credentials` Lecture du point d’entrée API [comment utiliser la Destination SDK pour configurer votre destination](../guides/configure-destination-instructions.md) pour comprendre où cette étape s’inscrit dans le processus de configuration de votre destination.
