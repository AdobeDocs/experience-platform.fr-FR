---
title: Créer une connexion Source Azure Event Hubs à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un compte Azure Event Hubs à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 29%

---

# Créer une connexion source [!DNL Azure Event Hubs] à l’aide de l’API [!DNL Flow Service]

>[!IMPORTANT]
>
>La source [!DNL Azure Event Hubs] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce tutoriel pour savoir comment connecter [!DNL Azure Event Hubs] (ci-après dénommé « [!DNL Event Hubs] ») à Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
- [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à connecter [!DNL Event Hubs] à Experience Platform à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puissiez vous connecter à votre compte [!DNL Event Hubs], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB  Authentification standard ]

| Informations d’identification | Description |
| --- | --- |
| `sasKeyName` | Nom de la règle d’autorisation, également appelé nom de la clé SAS. |
| `sasKey` | Clé primaire de l’espace de noms [!DNL Event Hubs]. La `sasPolicy` à laquelle correspond le `sasKey` doit disposer de droits `manage` configurés pour que la liste [!DNL Event Hubs] soit renseignée. |
| `namespace` | Espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur de définition de portée unique dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB authentification SAS]

| Informations d’identification | Description |
| --- | --- |
| `sasKeyName` | Nom de la règle d’autorisation, également appelé nom de la clé SAS. |
| `sasKey` | Clé primaire de l’espace de noms [!DNL Event Hubs]. La `sasPolicy` à laquelle correspond le `sasKey` doit disposer de droits `manage` configurés pour que la liste [!DNL Event Hubs] soit renseignée. |
| `namespace` | Espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur de définition de portée unique dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| `eventHubName` | Renseignez votre nom de [!DNL Azure Event Hub]. Lisez la documentation de [Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) pour plus d&#39;informations sur les noms de [!DNL Event Hub]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Pour plus d’informations sur l’authentification des signatures d’accès partagé (SAS) pour [!DNL Event Hubs], consultez le guide [[!DNL Azure]  sur l’utilisation de SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Authentification Azure Active Directory Event Hub]

| Informations d’identification | Description |
| --- | --- |
| `tenantId` | L’identifiant du client auprès duquel vous souhaitez demander une autorisation. Votre identifiant client peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque** : l’ID client est appelé « ID de répertoire » dans l’interface [!DNL Microsoft Azure]. |
| `clientId` | Identifiant d’application attribué à votre application. Vous pouvez récupérer cet identifiant à partir du portail [!DNL Microsoft Entra ID] où vous avez enregistré votre [!DNL Azure Active Directory]. |
| `clientSecretValue` | Secret client utilisé avec l’identifiant client pour authentifier votre application . Vous pouvez récupérer votre secret client à partir du portail [!DNL Microsoft Entra ID] où vous avez enregistré votre [!DNL Azure Active Directory]. |
| `namespace` | Espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur de définition de portée unique dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |

Pour plus d’informations sur [!DNL Azure Active Directory], consultez le guide [Azure sur l’utilisation de l’Entra ID de Microsoft](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Authentification Azure Active Directory étendue Event Hub]

| Informations d’identification | Description |
| --- | --- |
| `tenantId` | L’identifiant du client auprès duquel vous souhaitez demander une autorisation. Votre identifiant client peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque** : l’ID client est appelé « ID de répertoire » dans l’interface [!DNL Microsoft Azure]. |
| `clientId` | Identifiant d’application attribué à votre application. Vous pouvez récupérer cet identifiant à partir du portail [!DNL Microsoft Entra ID] où vous avez enregistré votre [!DNL Azure Active Directory]. |
| `clientSecretValue` | Secret client utilisé avec l’identifiant client pour authentifier votre application . Vous pouvez récupérer votre secret client à partir du portail [!DNL Microsoft Entra ID] où vous avez enregistré votre [!DNL Azure Active Directory]. |
| `namespace` | Espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur de définition de portée unique dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| `eventHubName` | Renseignez votre nom de [!DNL Azure Event Hub]. Lisez la documentation de [Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) pour plus d&#39;informations sur les noms de [!DNL Event Hub]. |

>[!ENDTABS]

Pour plus d’informations sur ces valeurs, consultez [ce document Concentrateur d’événements](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d’authentification d’une connexion de base [!DNL Event Hubs]. Pour modifier le type d’authentification, vous devez créer une connexion de base.

La première étape de création d’une connexion source consiste à authentifier votre source [!DNL Event Hubs] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL Event Hubs] dans le cadre des paramètres de requête.

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Authentification standard ]

Pour créer un compte à l’aide de l’authentification standard, envoyez une requête POST au point d’entrée `/connections` tout en fournissant des valeurs pour vos `sasKeyName`, `sasKey` et `namespace`.

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
| `auth.params.sasKeyName` | Nom de la règle d’autorisation, également appelé nom de la clé SAS. |
| `auth.params.sasKey` | Signature d’accès partagé générée. |
| `auth.params.namespace` | Espace de noms du [!DNL Event Hubs] auquel vous accédez. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

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

>[!TAB authentification SAS]

Pour créer un compte à l’aide de l’authentification SAS, envoyez une requête POST au point d’entrée `/connections` tout en fournissant des valeurs pour vos `sasKeyName`, `sasKey`, `namespace` et `eventHubName`.

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
| `auth.params.sasKeyName` | Nom de la règle d’autorisation, également appelé nom de la clé SAS. |
| `auth.params.sasKey` | Signature d’accès partagé générée. |
| `auth.params.namespace` | Espace de noms du [!DNL Event Hubs] auquel vous accédez. |
| `params.eventHubName` | Nom de votre source de [!DNL Event Hubs]. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

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

>[!TAB Authentification Azure Active Directory Event Hub]

Pour créer un compte à l’aide de l’authentification Azure Active Directory, envoyez une requête POST au point d’entrée `/connections` et indiquez les valeurs de vos `tenantId`, `clientId`, `clientSecretValue` et `namespace`.

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
| `auth.params.tenantId` | Identifiant client de votre application . **Remarque** : l’ID client est appelé « ID de répertoire » dans l’interface [!DNL Microsoft Azure]. |
| `auth.params.clientId` | Identifiant client de votre organisation. |
| `auth.params.clientSecretValue` | Valeur du secret client de votre organisation. |
| `auth.params.namespace` | Espace de noms du [!DNL Event Hubs] auquel vous accédez. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

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

>[!TAB Authentification Azure Active Directory étendue Event Hub]

Pour créer un compte à l’aide de l’authentification Azure Active Directory, envoyez une requête POST au point d’entrée `/connections` et indiquez les valeurs de vos `tenantId`, `clientId`, `clientSecretValue`, `namespace` et `eventHubName`.

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
| `auth.params.tenantId` | Identifiant client de votre application . **Remarque** : l’ID client est appelé « ID de répertoire » dans l’interface [!DNL Microsoft Azure]. |
| `auth.params.clientId` | Identifiant client de votre organisation. |
| `auth.params.clientSecretValue` | Valeur du secret client de votre organisation. |
| `auth.params.namespace` | Espace de noms du [!DNL Event Hubs] auquel vous accédez. |
| `auth.params.eventHubName` | Nom de votre source de [!DNL Event Hubs]. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL Event Hubs] est : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

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
>Un groupe de consommateurs [!DNL Event Hubs] ne peut être utilisé que pour un seul flux à la fois.

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
| `baseConnectionId` | Identifiant de connexion de votre source de [!DNL Event Hubs] générée à l’étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion fixe pour [!DNL Event Hubs]. Cet identifiant est `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Format des données [!DNL Event Hubs] que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |
| `params.eventHubName` | Nom de votre source de [!DNL Event Hubs]. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |
| `params.reset` | Ce paramètre définit la manière dont les données seront lues. Utilisez `latest` pour commencer la lecture à partir des données les plus récentes et `earliest` pour commencer la lecture à partir des premières données disponibles dans le flux. Ce paramètre est facultatif et défini par défaut sur `earliest` s’il n’est pas fourni. |
| `params.consumerGroup` | Mécanisme de publication ou d’abonnement à utiliser pour les [!DNL Event Hubs]. Ce paramètre est facultatif et défini par défaut sur `$Default` s’il n’est pas fourni. Pour plus d’informations, consultez ce [[!DNL Event Hubs] guide sur les consommateurs d’événements](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers). **Remarque** : un groupe de consommateurs [!DNL Event Hubs] ne peut être utilisé que pour un seul flux à la fois. |

>[!NOTE]
>
>Après avoir créé ou mis à jour un flux de données en continu, une brève pause de 5 minutes dans l’ingestion des données est nécessaire pour éviter toute instance potentielle de perte de données ou d’abandon de données.

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion source [!DNL Event Hubs] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet ID de connexion source dans le tutoriel suivant pour [créer un flux de données en continu à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../collect/streaming.md).
