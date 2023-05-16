---
description: Cette page illustre l’appel API utilisé pour mettre à jour une configuration d’informations d’identification existante via Adobe Experience Platform Destination SDK.
title: Mise à jour d’une configuration d’informations d’identification
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 35%

---


# Mise à jour d’une configuration d’informations d’identification

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page illustre la requête d’API et la charge utile que vous pouvez utiliser pour mettre à jour une configuration d’informations d’identification existante, à l’aide de la variable `/authoring/credentials` Point d’entrée de l’API.

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

## Mise à jour d’une configuration d’informations d’identification {#update}

Vous pouvez mettre à jour une [existant](create-credential-configuration.md) configuration des informations d’identification en effectuant une `PUT` à la fonction `/authoring/credentials` point de terminaison avec la payload mise à jour.

Pour obtenir une configuration d’informations d’identification existante et les `{INSTANCE_ID}`, voir l’article sur [récupération d’une configuration des informations d’identification](retrieve-credential-configuration.md).

**Format d’API**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | L’identifiant de la configuration des informations d’identification que vous souhaitez mettre à jour. Pour obtenir une configuration d’informations d’identification existante et les `{INSTANCE_ID}`, voir [Récupération d’une configuration d’informations d’identification](retrieve-credential-configuration.md). |

Les requêtes suivantes mettent à jour les configurations d’informations d’identification existantes, définies par les paramètres fournis dans le payload.

Sélectionnez chaque onglet ci-dessous pour afficher la charge utile correspondante.

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

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration des informations d’identification mise à jour.

+++

>[!TAB Amazon S3]

**Mettre à jour une [!DNL Amazon S3] configuration des informations d’identification**

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
| `accessId` | Chaîne | [!DNL Amazon S3] ID d’accès |
| `secretKey` | Chaîne | [!DNL Amazon S3] clé secrète |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration des informations d’identification mise à jour.

+++

>[!TAB SSH]

**Mettre à jour une [!DNL SSH] configuration des informations d’identification**

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
| `sshKey` | Chaîne | [!DNL SSH] clé pour [!DNL SFTP] avec [!DNL SSH] authentication |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration des informations d’identification mise à jour.

+++

>[!TAB Stockage du lac de données Azure]

**Mettre à jour une [!DNL Azure Data Lake Storage] configuration des informations d’identification**

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
| `servicePrincipalId` | Chaîne | [!DNL Azure Service Principal] ID pour [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | Chaîne | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration des informations d’identification mise à jour.

+++

>[!TAB Stockage Azure Blob]

**Mettre à jour une [!DNL Azure Blob] configuration des informations d’identification**

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
| `connectionString` | Chaîne | [!DNL Azure Blob Storage] chaîne de connexion |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration des informations d’identification mise à jour.

+++

>[!ENDTABS]

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment mettre à jour une configuration d’informations d’identification à l’aide de la variable `/authoring/credentials` Point d’entrée de l’API. Poursuivez votre apprentissage dans la section [Comment utiliser Destination SDK pour configurer votre destination](../guides/configure-destination-instructions.md) et obtenez une vue dʼensemble du processus de configuration de votre destination.
