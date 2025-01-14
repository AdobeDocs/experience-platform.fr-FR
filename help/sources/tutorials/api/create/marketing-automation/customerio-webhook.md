---
title: Créez une connexion source et un flux de données pour Customer.io à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Customer.io à l’aide de l’API Flow Service.
badge: Version bêta
exl-id: 1c84d818-428f-4097-9f6f-ef0cf1a04785
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 55%

---

# Créer une connexion source et un flux de données pour [!DNL Customer.io] à l’aide de l’API Flow Service

>[!NOTE]
>
>La source [!DNL Customer.io] est en version Beta. Voir la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Le tutoriel suivant vous guide tout au long des étapes de création d’une connexion source [!DNL Customer.io] et d’un flux de données pour importer des données d’événement [[!DNL Customer.io]](https://customer.io/) dans Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main {#getting-started}

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Connecter [!DNL Customer.io] à Platform à l’aide de l’API [!DNL Flow Service] {#connect-platform-to-flow-api}

La procédure ci-dessous décrit les étapes à suivre pour créer une connexion source et un flux de données afin d’apporter vos données d’événements [!DNL Customer.io] à l’Experience Platform.

### Créer une connexion source {#source-connection}

Créez une connexion source en adressant une requête de POST à l’API [!DNL Flow Service], tout en fournissant l’identifiant de spécification de connexion de votre source, des détails tels que le nom et la description, ainsi que le format de vos données.

**Format d’API**

```https
POST /sourceConnections
```

**Requête**

La requête suivante crée une connexion source pour [!DNL Customer.io] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Customer.io",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for customer.io",
      "connectionSpec": {
          "id": "96479064-7b8a-4d69-b9ed-21c5683837ea",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion source. |
| `connectionSpec.id` | Identifiant de spécification de connexion correspondant à votre source. |
| `data.format` | Format des données [!DNL Customer.io] que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
    "etag": "\"af00a717-0000-0200-0000-63ef2cbd0000\""
}
```

### Créer un schéma XDM cible {#target-schema}

Pour que les données sources soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Le schéma cible est ensuite utilisé pour créer un jeu de données Platform contenant les données sources.

Un schéma XDM cible peut être créé en adressant une requête POST à l’[API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, suivez le tutoriel sur la [création d’un schéma à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Créer un jeu de données cible {#target-dataset}

Un jeu de données cible peut être créé en adressant une requête POST à l’[API Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/) et en fournissant l’identifiant du schéma cible dans la payload.

Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, suivez le tutoriel sur la [création d’un jeu de données à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Créer une connexion cible {#target-connection}

Une connexion cible représente la connexion à la destination où les données ingérées doivent être stockées. Pour créer une connexion cible, vous devez fournir l’identifiant fixe de spécification de connexion qui correspond au lac de données. Cet identifiant est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma cible, d’un jeu de données cible et de l’identifiant de spécification de connexion au lac de données. À lʼaide de ces identifiants, vous pouvez créer une connexion cible à l’aide de l’API [!DNL Flow Service] pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

```https
POST /targetConnections
```

**Requête**

La requête suivante crée une connexion cible pour [!DNL Customer.io] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Customer.io",
      "description": "Streaming Target Connection for Customer.io",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63ec807d3f5ce91bd2d06c65"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom de la connexion cible. Assurez-vous que le nom de votre connexion cible est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion cible. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion cible. |
| `connectionSpec.id` | Identifiant de spécification de connexion qui correspond au lac de données. Cet ID fixe est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Format des données [!DNL Customer.io] à ingérer. |
| `params.dataSetId` | Identifiant du jeu de données cible récupéré lors d’une étape précédente. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique de la nouvelle connexion cible (`id`). Cet identifiant est requis aux étapes suivantes.

```json
{
    "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
    "etag": "\"70003dff-0000-0200-0000-63ef4a090000\""
}
```

### Créer un mappage {#mapping}

Pour que les données sources soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible se rattache. Pour ce faire, il suffit d’adresser une requête de POST à [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) avec des mappages de données définis dans la payload de la requête.

**Format d’API**

```http
POST /conversion/mappingSets
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.cio_id",
            "sourceAttribute": "data.identifiers.cio_id",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.email",
            "sourceAttribute": "data.identifiers.email",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.event_id0",
            "sourceAttribute": "event_id",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.metricx",
            "sourceAttribute": "metric",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.object_type1",
            "sourceAttribute": "object_type",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestampx",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| Propriété | Description |
| --- | --- |
| `outputSchema.schemaRef.id` | Identifiant du [schéma XDM cible](#target-schema) généré lors d’une étape précédente. |
| `mappings.sourceType` | Type d’attribut source en cours de mappage. |
| `mappings.source` | Attribut source qui doit être mappé à un chemin XDM de destination. |
| `mappings.destination` | Chemin XDM de destination vers lequel l’attribut source est mappé. |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Cette valeur est requise lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
    "version": 0,
    "createdDate": 1676627988129,
    "modifiedDate": 1676627988129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Créer un flux {#flow}

La dernière étape pour importer des données de [!DNL Customer.io] vers Platform consiste à créer un flux de données. Vous disposez à présent des valeurs requises suivantes :

* [ID de connexion source](#source-connection)
* [ID de connexion cible](#target-connection)
* [Identifiant de mappage](#mapping)

Un flux de données est chargé de planifier et de collecter les données provenant d’une source. Vous pouvez créer un flux de données en exécutant une requête POST et en fournissant les valeurs mentionnées précédemment dans la payload.

**Format d’API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for Customer.io",
      "description": "Streaming Dataflow for Customer.io",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "133bb51f-f310-4b4a-b8b2-731aef1e223c"
      ],
      "targetConnectionIds": [
          "da8b75ad-f6ee-4991-95df-291e62936e98"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du flux de données. Assurez-vous que le nom de votre flux de données est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre flux de données. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre flux de données. |
| `flowSpec.id` | Identifiant de spécification de flux requis pour créer un flux de données. Cet ID fixe est `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | Version correspondante de l’identifiant de spécification de flux. Cette valeur est définie par défaut sur `1.0`. |
| `sourceConnectionIds` | L’[identifiant de connexion source](#source-connection) généré lors d’une étape précédente. |
| `targetConnectionIds` | [Identifiant de connexion cible](#target-connection) généré lors d’une étape précédente. |
| `transformations` | Cette propriété contient les différentes transformations qui doivent être appliquées à vos données. Cette propriété est requise lors de l’importation de données non conformes à XDM dans Platform. |
| `transformations.name` | Nom attribué à la transformation. |
| `transformations.params.mappingId` | [Identifiant de mappage](#mapping) généré lors d’une étape précédente. |
| `transformations.params.mappingVersion` | Version correspondante de l’identifiant de mappage. Ce paramètre est défini par défaut sur `0`. |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du flux de données nouvellement créé. Vous pouvez utiliser cet identifiant pour surveiller, mettre à jour ou supprimer votre flux de données.

```json
{
    "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
    "etag": "\"4c012103-0000-0200-0000-63ef57db0000\""
}
```

### Obtention de l’URL du point d’entrée de diffusion en continu {#get-streaming-endpoint-url}

Une fois votre flux de données créé, vous pouvez récupérer votre URL de point d’entrée de diffusion en continu. Vous utiliserez cette URL de point d’entrée pour abonner votre source à un webhook, ce qui permettra à votre source de communiquer avec Experience Platform.

Pour récupérer l’URL de votre point d’entrée de diffusion en continu, envoyez une requête de GET au point d’entrée de `/flows` et indiquez l’identifiant de votre flux de données.

**Format d’API**

```http
GET /flows/{FLOW_ID}
```

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des informations sur votre flux de données, y compris votre URL de point d’entrée, marquée comme `inletUrl`. Reportez-vous à la page [Configurer le Webhook](../../../ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint-url) pour obtenir la valeur requise.

```json
{
    "items": [
        {
            "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
            "createdAt": 1676629979503,
            "updatedAt": 1676629985390,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Customer.io",
            "description": "Streaming Dataflow for Customer.io",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"4c01c003-0000-0200-0000-63ef57e10000\"",
            "etag": "\"4c01c003-0000-0200-0000-63ef57e10000\"",
            "sourceConnectionIds": [
                "133bb51f-f310-4b4a-b8b2-731aef1e223c"
            ],
            "targetConnectionIds": [
                "da8b75ad-f6ee-4991-95df-291e62936e98"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
                        "connectionSpec": {
                            "id": "96479064-7b8a-4d69-b9ed-21c5683837ea",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e75dcb5247eb65e7385df30270192e80b145566f52ed74d570505bd2e82463f3"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4982698b-e6b3-48c2-8dcf-040e20121fd2",
            "providerRefId": "c4726e6f-64b4-4b3b-97e3-f128ace0cc74",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            }
        }
    ]
}
```

## Annexe {#appendix}

La section suivante fournit des informations sur les étapes que vous pouvez suivre pour surveiller, mettre à jour et supprimer votre flux de données.

### Surveiller votre flux de données {#monitor-dataflow}

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les exécutions du flux, le statut d’achèvement et les erreurs. Pour obtenir des exemples d’API complets, consultez le guide sur la [surveillance des flux de données sources à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Mettre à jour votre flux de données {#update-dataflow}

Mettez à jour les détails de votre flux de données, tels que son nom et sa description, ainsi que son planning d’exécution et les jeux de mappages associés en envoyant une requête de PATCH au point d’entrée `/flows` de [!DNL Flow Service]’API , tout en fournissant l’identifiant de votre flux de données. Lors de l’exécution d’une requête de PATCH, vous devez fournir le `etag` unique de votre flux de données dans l’en-tête `If-Match`. Pour obtenir des exemples d’API complets, consultez le guide sur la [mise à jour des flux de données sources à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Mettre à jour votre compte {#update-account}

Mettez à jour le nom, la description et les informations d’identification de votre compte source en adressant une requête de PATCH à l’API [!DNL Flow Service] et en fournissant votre identifiant de connexion de base comme paramètre de requête. Lors de l’exécution d’une requête de PATCH, vous devez indiquer le `etag` unique de votre compte source dans l’en-tête `If-Match`. Pour obtenir des exemples d’API complets, consultez le guide sur la [mise à jour de votre compte source à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Supprimer le flux de données {#delete-dataflow}

Supprimez votre flux de données en adressant une requête de DELETE à l’API [!DNL Flow Service] et en fournissant l’identifiant du flux de données à supprimer dans le cadre du paramètre de requête. Pour obtenir des exemples d’API complets, consultez le guide sur la [suppression de vos flux de données à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Supprimer votre compte {#delete-account}

Supprimez votre compte en adressant une requête de DELETE à l’API [!DNL Flow Service] et en fournissant l’identifiant de connexion de base du compte que vous souhaitez supprimer. Pour obtenir des exemples d’API complets, consultez le guide sur la [suppression de votre compte source à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
