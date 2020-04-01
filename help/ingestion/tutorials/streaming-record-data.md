---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Diffusion en flux continu des données d’enregistrement
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Diffusion en continu des données d’enregistrement vers Adobe Experience Platform

Ce didacticiel vous aidera à commencer à utiliser les API d’assimilation en flux continu, qui font partie des API du service d’administration des données de la plate-forme Adobe Experience Platform.

## Prise en main

Ce didacticiel nécessite une connaissance pratique de divers services Adobe Experience Platform. Avant de commencer ce didacticiel, veuillez consulter la documentation des services suivants :

- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la Plateforme organise les données d’expérience.
- [](../../profile/home.md)du client en temps réel : Fournit un unifié et en temps réel, basé sur des données agrégées provenant de sources multiples.
- [Guide](../../xdm/api/getting-started.md)du développeur du Registre des  : Un guide complet qui couvre chacun des points de fin disponibles de l&#39;API de Registre du  et comment y faire des appels. Ce didacticiel explique comment connaître votre `{TENANT_ID}`identité, qui apparaît dans les appels, et comment créer des , qui est utilisé pour créer un jeu de données à des fins d&#39;assimilation.

De plus, ce didacticiel nécessite que vous ayez déjà créé une connexion en flux continu. Pour plus d&#39;informations sur la création d&#39;une connexion en flux continu, consultez le didacticiel [Création d&#39;une connexion en flux continu](./create-streaming-connection.md).

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API d’assimilation en flux continu.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Composer un  basé sur la classe de XDM Individuel 

Pour créer un jeu de données, vous devez tout d’abord créer un nouveau  qui implémente la classe XDM Individuelle . Pour plus d&#39;informations sur la création de  de, veuillez lire le guide [du développeur de l&#39;API de registre de](../../xdm/api/getting-started.md).

**Format API**

```http
POST /schemaregistry/tenant/schemas
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `title` | Nom que vous souhaitez utiliser pour votre  de. Ce nom doit être unique. |
| `description` | Description significative du que vous êtes en train de créer. |
| `meta:immutableTags` | Dans cet exemple, la `union` balise est utilisée pour conserver vos données dans le [client en temps](../../profile/home.md)réel. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 avec les détails de votre  nouvellement créé.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `{TENANT_ID}` | Cet identifiant permet de s’assurer que les ressources que vous créez sont correctement nommées et contenues dans votre organisation IMS. Pour plus d&#39;informations sur l&#39;ID du client, veuillez lire le guide [du registre des](../../xdm/api/getting-started.md#know-your-tenant-id). |

Veuillez prendre note des attributs `$id` et des `version` attributs, car ceux-ci seront utilisés lors de la création de votre jeu de données.

## Définition d’un descripteur d’identité principal pour le  de

Ensuite, ajoutez un descripteur [d’](../../xdm/api/descriptors.md) identité au créé ci-dessus, en utilisant l’attribut d’adresse électronique de travail comme identifiant principal. Cela entraînera deux modifications :

1. L’adresse électronique du travail devient un champ obligatoire. Cela signifie que les messages envoyés sans ce champ ne seront pas validés et ne seront pas assimilés.

2. Le du client en temps réel utilisera l’adresse électronique de travail comme identifiant pour rassembler plus d’informations sur cette personne.

### Requête

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | Le `$id` que vous avez reçu précédemment lorsque vous avez composé le . Voici à quoi ça ressemble : `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE] &#x200B; &#x200B; codes de  d&#39; d&#39;identité&#x200B;****
>
> Assurez-vous que les codes sont valides - l&#39;exemple ci-dessus utilise &quot;email&quot;, qui est une identité  standard. Vous trouverez d&#39;autres  d&#39;identité standard couramment utilisés  dans la FAQ [du service](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)d&#39;identité.
>
> Si vous souhaitez créer un  de  personnalisé, suivez les étapes décrites dans la présentation [du de l&#39;](../../identity-service/home.md)identité  .

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 avec des informations sur le nouveau descripteur d’identité principal du.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Création d’un jeu de données pour les données d’enregistrement

Une fois que vous avez créé votre  de, vous devez créer un jeu de données pour assimiler des données d’enregistrement.

>[!NOTE] Ce jeu de données sera activé pour les **clients en temps** réel et le service **** d’identité.

**Format API**

```http
POST /catalog/dataSets
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 et un tableau contenant l’ID du jeu de données nouvellement créé au format `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Envoi de données d’enregistrement à la connexion de flux continu

Une fois le jeu de données et la connexion en flux continu en place, vous pouvez assimiler des enregistrements JSON au format XDM pour intégrer des données d’enregistrement dans la plateforme.

**Format API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de la connexion de flux continu précédemment créée. |
| `synchronousValidation` | Paramètre facultatif  destiné au développement. S’il est défini sur `true`, il peut être utilisé pour obtenir des commentaires immédiats afin de déterminer si la demande a bien été envoyée. Par défaut, cette valeur est définie sur `false`. |

**Requête**

>[!NOTE] L’appel d’API suivant **ne nécessite pas** d’en-tête d’authentification.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
            "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails du nouveau  en flux continu.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID de la connexion de flux continu précédemment créée. |
| `xactionId` | Un identifiant unique a généré côté serveur pour l&#39;enregistrement que vous venez d&#39;envoyer. Cet ID permet à Adobe de suivre le cycle de vie de cet enregistrement sur divers systèmes et avec le débogage. |
| `receivedTimeMs` | Horodatage (en millisecondes) qui indique l’heure de réception de la demande. |
| `synchronousValidation.status` | Comme le paramètre  `synchronousValidation=true` a été ajouté, cette valeur s’affiche. Si la validation a réussi, l’état est `pass`. |

## Récupérer les données d’enregistrement nouvellement assimilées

Pour valider les enregistrements précédemment assimilés, vous pouvez utiliser l’API [d’accès aux](../../profile/api/entities.md) pour récupérer les données d’enregistrement.

>[!NOTE] Si l’ID de stratégie de fusion n’est pas défini et que le n’est pas .</span>name ou relatedSchema</span>.name est `_xdm.context.profile`, Accès  récupérera **toutes les** identités associées.

**Format API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Paramètre | Description |
| --------- | ----------- |
| `schema.name` | **Obligatoire.** Nom du auquel vous accédez. |
| `entityId` | ID de l’entité. Si cela est fourni, vous devez également fournir l&#39;entité  . |
| `entityIdNS` |  de l’ID que vous tentez de récupérer. |

**Requête**

Vous pouvez consulter les données d’enregistrement précédemment assimilées avec la requête GET suivante.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails des entités demandées. Comme vous pouvez le voir, c&#39;est le même enregistrement qui a été assimilé avec succès plus tôt.

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## Étapes suivantes

En lisant ce , vous comprenez maintenant comment assimiler des données d’enregistrement dans la plateforme à l’aide de connexions en flux continu. Vous pouvez essayer d’effectuer plus d’appels avec des valeurs différentes et de récupérer les valeurs mises à jour. De plus, vous pouvez  surveiller vos données assimilées via l’interface utilisateur de la plateforme. Pour plus d&#39;informations, veuillez lire le guide d&#39;assimilation [des données de](../quality/monitor-data-flows.md) surveillance.

Pour plus d&#39;informations sur l&#39;ingestion en flux continu en général, veuillez lire l&#39;aperçu [de l&#39;ingestion en](../streaming-ingestion/overview.md)flux continu.


