---
title: Utiliser Azure Private Link pour les sources dans l’API
description: Découvrez comment créer et utiliser des liens privés pour les sources Adobe Experience Platform
badge: Beta
exl-id: 9b7fc1be-5f42-4e29-b552-0b0423a40aa1
source-git-commit: 52365851aef0e0e0ad532ca19a8e0ddccacf7af7
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 8%

---

# Utilisation de [!DNL Azure Private Link] pour les sources dans l’API

>[!AVAILABILITY]
>
>Cette fonctionnalité est en disponibilité limitée et n’est actuellement prise en charge que par les sources suivantes :
>
>* [[!DNL Azure Blob]](../../connectors/cloud-storage/blob.md)
>* [[!DNL Azure Data Lake Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

Vous pouvez utiliser la fonction [!DNL Azure Private Link] pour créer des points d’entrée privés auxquels vos sources Adobe Experience Platform peuvent se connecter. Connectez vos sources en toute sécurité à un réseau virtuel à l&#39;aide d&#39;adresses IP privées, éliminez le besoin d&#39;adresses IP publiques et réduisez votre surface d&#39;attaque.Simplifiez votre configuration réseau en supprimant la nécessité de configurations complexes de pare-feu ou de traduction d&#39;adresses réseau, tout en veillant à ce que le trafic de données atteigne uniquement les services approuvés.

Lisez ce guide pour savoir comment utiliser des API pour créer et utiliser un point d’entrée privé.

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Créer un point d’entrée privé {#create-private-endpoint}

Pour créer un point d’entrée privé, envoyez une requête POST à `/privateEndpoints`.

**Format d’API**

```http
POST /privateEndpoints
```

**Requête**

La requête suivante crée un point d’entrée privé :

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [],
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre point d’entrée privé. |
| `subscriptionId` | ID associé à votre abonnement [!DNL Azure]. Pour plus d’informations, consultez le guide de [!DNL Azure] sur la [récupération des ID d’abonnement et de client de l’ [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Nom de votre groupe de ressources sur [!DNL Azure]. Un groupe de ressources contient les ressources associées à une solution [!DNL Azure]. Pour plus d’informations, consultez le guide [!DNL Azure] sur [la gestion des groupes de ressources](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | Nom de la ressource. Dans [!DNL Azure], une ressource fait référence à des instances telles que des machines virtuelles, des applications web et des bases de données. Pour plus d’informations, consultez le guide [!DNL Azure] sur [présentation du gestionnaire  [!DNL Azure]  ressources](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | Noms de domaine complets pour votre source. Cette propriété est requise uniquement lors de l’utilisation de la source [!DNL Snowflake]. |
| `connectionSpec.id` | Identifiant de spécification de connexion de la source que vous utilisez. |
| `connectionSpec.version` | Version de l’identifiant de spécification de connexion que vous utilisez. |

+++

**Réponse**

Une réponse réussie renvoie les éléments suivants :

+++Sélectionner pour afficher l’exemple de réponse

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "fqdns": [],
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant du point d’entrée privé que vous venez de créer. |
| `name` | Nom de votre point d’entrée privé. |
| `subscriptionId` | ID associé à votre abonnement [!DNL Azure]. Pour plus d’informations, consultez le guide de [!DNL Azure] sur la [récupération des ID d’abonnement et de client de l’ [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Nom de votre groupe de ressources sur [!DNL Azure]. Un groupe de ressources contient les ressources associées à une solution [!DNL Azure]. Pour plus d’informations, consultez le guide [!DNL Azure] sur [la gestion des groupes de ressources](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | Nom de la ressource. Dans [!DNL Azure], une ressource fait référence à des instances telles que des machines virtuelles, des applications web et des bases de données. Pour plus d’informations, consultez le guide [!DNL Azure] sur [présentation du gestionnaire  [!DNL Azure]  ressources](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | Noms de domaine complets pour votre source. Cette propriété est requise uniquement lors de l’utilisation de la source [!DNL Snowflake]. |
| `connectionSpec.id` | Identifiant de spécification de connexion de la source que vous utilisez. |
| `connectionSpec.version` | Version de l’identifiant de spécification de connexion que vous utilisez. |
| `state` | État actuel de votre point d’entrée privé. Les états valides sont les suivants : <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## Récupération d’une liste de points d’entrée privés {#retrieve-private-endpoints}

Pour récupérer une liste de points d’entrée privés d’un sandbox donné de votre organisation, envoyez une requête GET à `/privateEndpoints`.

**Format d’API**

```http
GET /privateEndpoints
```

**Requête**

La requête suivante récupère une liste de tous les points d’entrée privés qui existent dans votre organisation.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie une liste de points d’entrée privés de votre organisation.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Récupération d’une liste de points d’entrée privés pour une source donnée {#retrieve-private-endpoints-by-source}

Pour récupérer une liste de points d’entrée privés qui correspondent à une source spécifique, envoyez une requête GET au point d’entrée `/privateEndpoints` et indiquez le `connectionSpec.id` de la source.

**Format d’API**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| Paramètre de requête | Description |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | Identifiant de spécification de connexion de la source que vous souhaitez rechercher dans les points d’entrée privés. |

**Requête**

La requête suivante récupère une liste de tous les points d’entrée privés qui correspondent à la source avec l’identifiant de spécification de connexion : `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie une liste de tous les points d’entrée privés qui correspondent à la source avec l’identifiant de spécification de connexion : `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Récupérer un point d’entrée privé {#retrieve-specific-private-endpoint}

Pour récupérer un point d’entrée privé spécifique, envoyez une requête GET à `/privateEndpoints` et indiquez l’identifiant du point d’entrée privé que vous souhaitez récupérer.

**Format d’API**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Paramètre de requête | Description |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | L’identifiant du point d’entrée privé que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère le point d’entrée privé avec l’ID :`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie le point d’entrée privé avec l’identifiant : `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`

+++Sélectionner pour afficher l’exemple de réponse

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## Résoudre un point d’entrée privé {#resolve-private-endpoint}

**Format d’API**

```http
GET /privateEndpoints?op=autoResolve
```

**Requête**

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**Réponse**

+++Sélectionner pour afficher l’exemple de réponse

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## Activation de la création interactive {#enable-interactive-authoring}

La création interactive est utilisée pour des fonctionnalités telles que l’exploration d’une connexion ou d’un compte et la prévisualisation des données. Pour activer la création interactive, envoyez une requête POST à `/privateEndpoints/interactiveAuthoring` et spécifiez `enable` en tant qu’opérateur dans vos paramètres de requête.

**Format d’API**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| Paramètre de requête | Description |
| --- | --- |
| `op` | Opération que vous souhaitez effectuer. Pour activer la création interactive, définissez la valeur `op` sur `enable`. |

**Requête**

La requête suivante active la création interactive pour votre point d’entrée privé et définit la TTL sur 60 minutes.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| Propriété | Description |
| --- | --- |
| `autoTerminationMinutes` | Durée de vie (TTL) de création interactive en minutes. La création interactive est utilisée pour des fonctionnalités telles que l’exploration d’une connexion ou d’un compte et la prévisualisation des données. Vous pouvez définir une durée de vie maximale de 120 minutes. La durée de vie par défaut est de 60 minutes. |

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 202 (Accepté).

## Récupération de l’état de création interactive {#retrieve-interactive-authoring-status}

Pour afficher le statut actuel de la création interactive pour votre point d’entrée privé, envoyez une requête GET à `/privateEndpoints/interactiveAuthoring`.

**Format d’API**

```http
GET /privateEndpoints/interactiveAuthoring
```

**Requête**

La requête suivante récupère le statut de la création interactive :

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

+++Sélectionner pour afficher l’exemple de réponse

```json
{
    "status": "Disabled"
}
```

| Propriété | Description |
| --- | --- |
| `status` | Statut de la création interactive. Les valeurs valides sont les suivantes : `disabled`, `enabling`, `enabled`. |

+++

## Supprimer le point de terminaison privé {#delete-private-endpoint}

Pour supprimer votre point d’entrée privé, envoyez une requête DELETE à `/privateEndpoints` et indiquez l’identifiant du point d’entrée que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Paramètre de requête | Description |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | L’identifiant du point d’entrée privé que vous souhaitez supprimer. |

**Requête**

La requête suivante supprime le point d’entrée privé avec l’ID : `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 (Succès). Vous pouvez vérifier la suppression en effectuant une requête GET et en `/privateEndpoints` et en fournissant l’identifiant supprimé comme paramètre de requête.

## Service de flux {#flow-service}

Lisez les sections suivantes pour savoir comment utiliser des points d’entrée privés conjointement avec l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

### Créer une connexion avec un point d’entrée privé {#create-base-connection}

Pour créer une connexion avec un point d’entrée privé dans Experience Platform, envoyez une requête POST au point d’entrée `/connections` de l’API [!DNL Flow Service].

**Format d’API**

```http
POST /connections/
```

**Requête**

La requête suivante crée une connexion de base authentifiée pour [!DNL Snowflake], tout en utilisant un point d’entrée privé.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "A base connection for a Snowflake source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre connexion de base. |
| `description` | (Facultatif) Description qui fournit des informations supplémentaires sur votre connexion. |
| `auth.specName` | Authentification utilisée pour connecter votre source à Experience Platform. |
| `auth.params.connectionString` | Chaîne de connexion [!DNL Snowflake]. Pour plus d’informations, consultez le [[!DNL Snowflake] guide d’authentification des API](../api/create/databases/snowflake.md). |
| `auth.params.usePrivateLink` | Valeur booléenne qui détermine si vous utilisez ou non un point d’entrée privé. Définissez cette valeur sur `true` si vous utilisez un point d’entrée privé. |
| `connectionSpec.id` | Identifiant de spécification de connexion de [!DNL Snowflake]. |
| `connectionSpec.version` | Version de l’identifiant de spécification de connexion [!DNL Snowflake]. |

+++

**Réponse**

Une réponse réussie renvoie l’identifiant de connexion de base et l’etag que vous venez de générer.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### Récupérer les connexions liées à un point d’entrée privé donné {#retrieve-connections-by-endpoint}

Pour récupérer des connexions liées à un point d’entrée privé spécifique, envoyez une requête GET au point d’entrée `/connections` et indiquez l’identifiant du point d’entrée privé comme paramètre de requête.

**Format d’API**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| Paramètre de requête | Description |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | L’identifiant du point d’entrée privé lié aux connexions que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère les connexions existantes liées à un point d’entrée privé avec l’ID : `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie une liste de connexions liées au point d’entrée privé interrogé.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### Récupérer les connexions associées à un point d’entrée privé {#retrieve-connections}

Pour récupérer les connexions associées à un point d’entrée privé, envoyez une requête GET au point d’entrée `/connections` et indiquez le `property=auth.params.usePrivateLink==true` comme paramètre de requête.

**Format d’API**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**Requête**

La requête suivante récupère toutes les connexions de votre organisation qui utilisent des points d’entrée privés.

+++Sélectionner pour afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie toutes les connexions liées à des points d’entrée privés.

+++Sélectionner pour afficher l’exemple de réponse

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++
