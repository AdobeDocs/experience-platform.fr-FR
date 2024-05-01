---
title: Création d’une connexion source Azure Event Hubs à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un compte Azure Event Hubs à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 33%

---

# Créez un [!DNL Azure Event Hubs] connexion source à l’aide de la fonction [!DNL Flow Service] API

>[!IMPORTANT]
>
>La variable [!DNL Azure Event Hubs] source est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Lisez ce tutoriel pour apprendre à vous connecter [!DNL Azure Event Hubs] (ci-après dénommés &quot;[!DNL Event Hubs]&quot;) à l’Experience Platform, à l’aide de la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
- [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à connecter [!DNL Event Hubs] à Platform à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Event Hubs] , vous devez fournir des valeurs pour les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB Authentification standard]

| Informations d’identification | Description |
| --- | --- |
| `sasKeyName` | Nom de la règle d’autorisation, également connu sous le nom de clé SAS. |
| `sasKey` | La clé primaire de la variable [!DNL Event Hubs] espace de noms. La variable `sasPolicy` que la variable `sasKey` correspond à doit avoir `manage` les droits configurés pour [!DNL Event Hubs] liste à renseigner. |
| `namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB Authentification SAS]

| Informations d’identification | Description |
| --- | --- |
| `sasKeyName` | Nom de la règle d’autorisation, également connu sous le nom de clé SAS. |
| `sasKey` | La clé primaire de la variable [!DNL Event Hubs] espace de noms. La variable `sasPolicy` que la variable `sasKey` correspond à doit avoir `manage` les droits configurés pour [!DNL Event Hubs] liste à renseigner. |
| `namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| `eventHubName` | Le nom de votre [!DNL Event Hubs] source. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Pour plus d’informations sur l’authentification SAS (Shared Access Signatures) pour [!DNL Event Hubs], lisez le [[!DNL Azure] guide sur l&#39;utilisation de SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Event Hub Azure Active Directory Auth]

| Informations d’identification | Description |
| --- | --- |
| `tenantId` | Identifiant du tenant auprès duquel vous souhaitez demander une autorisation. Votre ID de tenant peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque**: l’identifiant du client est appelé &quot;ID d’annuaire&quot; dans la variable [!DNL Microsoft Azure] . |
| `clientId` | ID d’application affecté à votre application. Vous pouvez récupérer cet ID à partir de la variable [!DNL Microsoft Entra ID] le portail sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| `clientSecretValue` | Le secret client utilisé avec l’ID client pour authentifier votre application. Vous pouvez récupérer votre secret client à partir de la fonction [!DNL Microsoft Entra ID] le portail sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| `namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |

Pour plus d’informations sur [!DNL Azure Active Directory], lisez le [Guide Azure sur l’utilisation de Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Event Hub Portée par Azure Active Directory Auth]

| Informations d’identification | Description |
| --- | --- |
| `tenantId` | Identifiant du tenant auprès duquel vous souhaitez demander une autorisation. Votre ID de tenant peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque**: l’identifiant du client est appelé &quot;ID d’annuaire&quot; dans la variable [!DNL Microsoft Azure] . |
| `clientId` | ID d’application affecté à votre application. Vous pouvez récupérer cet ID à partir de la variable [!DNL Microsoft Entra ID] le portail sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| `clientSecretValue` | Le secret client utilisé avec l’ID client pour authentifier votre application. Vous pouvez récupérer votre secret client à partir de la fonction [!DNL Microsoft Entra ID] le portail sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| `namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| `eventHubName` | Le nom de votre [!DNL Event Hubs] source. |

>[!ENDTABS]

Pour plus d’informations sur ces valeurs, voir [ce document Événements Hub](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d&#39;authentification d&#39;un [!DNL Event Hubs] connexion de base. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

La première étape de création d’une connexion source consiste à authentifier votre source [!DNL Event Hubs] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL Event Hubs] dans le cadre des paramètres de requête.

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Authentification standard]

Pour créer un compte à l’aide de l’authentification standard, envoyez une demande de POST à la fonction `/connections` point de terminaison tout en fournissant des valeurs pour votre `sasKeyName`, `sasKey`, et `namespace`.

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}"
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.sasKeyName` | Nom de la règle d’autorisation, également connu sous le nom de clé SAS. |
| `auth.params.sasKey` | Signature d’accès partagé générée. |
| `auth.params.namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. |
| `connectionSpec.id` | La variable [!DNL Event Hubs] l’identifiant de spécification de connexion est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant de connexion est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Authentification SAS]

Pour créer un compte à l’aide de l’authentification SAS, envoyez une demande de POST à l’ `/connections` point de terminaison tout en fournissant des valeurs pour votre `sasKeyName`, `sasKey`,`namespace`, et `eventHubName`.

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.sasKeyName` | Nom de la règle d’autorisation, également connu sous le nom de clé SAS. |
| `auth.params.sasKey` | Signature d’accès partagé générée. |
| `auth.params.namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. |
| `params.eventHubName` | Le nom de votre [!DNL Event Hubs] source. |
| `connectionSpec.id` | La variable [!DNL Event Hubs] l’identifiant de spécification de connexion est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant de connexion est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Event Hub Azure Active Directory Auth]

Pour créer un compte à l’aide de l’authentification Azure Active Directory, envoyez une demande de POST à la fonction `/connections` point de terminaison tout en fournissant des valeurs pour votre `tenantId`, `clientId`,`clientSecretValue`, et `namespace`.

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.tenantId` | Identifiant du tenant de votre application. **Remarque**: l’identifiant du client est appelé &quot;ID d’annuaire&quot; dans la variable [!DNL Microsoft Azure] . |
| `auth.params.clientId` | ID client de votre organisation. |
| `auth.params.clientSecretValue` | La valeur du secret client de votre organisation. |
| `auth.params.namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. |
| `connectionSpec.id` | La variable [!DNL Event Hubs] l’identifiant de spécification de connexion est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant de connexion est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Event Hub Portée par Azure Active Directory Auth]

Pour créer un compte à l’aide de l’authentification Azure Active Directory, envoyez une demande de POST à la fonction `/connections` point de terminaison tout en fournissant des valeurs pour votre `tenantId`, `clientId`,`clientSecretValue`, `namespace`, et `eventHubName`.

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.tenantId` | Identifiant du tenant de votre application. **Remarque**: l’identifiant du client est appelé &quot;ID d’annuaire&quot; dans la variable [!DNL Microsoft Azure] . |
| `auth.params.clientId` | ID client de votre organisation. |
| `auth.params.clientSecretValue` | La valeur du secret client de votre organisation. |
| `auth.params.namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. |
| `auth.params.eventHubName` | Le nom de votre [!DNL Event Hubs] source. |
| `connectionSpec.id` | La variable [!DNL Event Hubs] l’identifiant de spécification de connexion est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant de connexion est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## Créer une connexion source

>[!TIP]
>
>Un [!DNL Event Hubs] Le groupe de consommateurs ne peut être utilisé que pour un seul flux à la fois.

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et un identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation.

Pour créer une connexion source, envoyez une requête POST au point d’entrée `/sourceConnections` de l’API [!DNL Flow Service].

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Azure Event Hubs source connection",
      "description": "A source connection for Azure Event Hubs",
      "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "eventHubName": "{EVENT_HUB_NAME}",
          "dataType": "raw",
          "reset": "latest",
          "consumerGroup": "{CONSUMER_GROUP}"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez fournir pour inclure plus d’informations sur votre connexion source. |
| `baseConnectionId` | L’identifiant de connexion de votre [!DNL Event Hubs] source générée à l’étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion fixe pour [!DNL Event Hubs]. Cet identifiant est `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Format des données [!DNL Event Hubs] que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |
| `params.eventHubName` | Le nom de votre [!DNL Event Hubs] source. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |
| `params.reset` | Ce paramètre définit la manière dont les données seront lues. Utilisation `latest` pour commencer la lecture à partir des données les plus récentes et utiliser `earliest` pour commencer la lecture à partir des premières données disponibles dans le flux. Ce paramètre est facultatif et la valeur par défaut est `earliest` si non fourni. |
| `params.consumerGroup` | Le mécanisme de publication ou d’abonnement à utiliser pour [!DNL Event Hubs]. Ce paramètre est facultatif et la valeur par défaut est `$Default` si non fourni. Consultez cette section [[!DNL Event Hubs] guide sur les consommateurs d’événements](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) pour plus d’informations. **Remarque**: [!DNL Event Hubs] Le groupe de consommateurs ne peut être utilisé que pour un seul flux à la fois. |

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Event Hubs] connexion source à l’aide de la fonction [!DNL Flow Service] API. Vous pouvez utiliser cet ID de connexion source dans le tutoriel suivant pour [créer un flux de données en continu à l’aide de l’API  [!DNL Flow Service] ](../../collect/streaming.md).
