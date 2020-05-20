---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Diffusion en continu des données d’enregistrement
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 2%

---


# Diffusion en continu des données d’enregistrement vers Adobe Experience Platform

Ce didacticiel vous aidera à commencer à utiliser les API d’assimilation en flux continu, qui font partie des API Adobe Experience Platform Data Ingestion Service.

## Prise en main

Ce didacticiel nécessite une connaissance pratique de divers services Adobe Experience Platform. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la Plateforme organise les données d&#39;expérience.
- [Profil](../../profile/home.md)client en temps réel : Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de plusieurs sources.
- [Guide](../../xdm/api/getting-started.md)du développeur du registre des Schémas : Un guide complet qui couvre chacun des points de terminaison disponibles de l&#39;API de registre de Schéma et comment leur envoyer des appels. Ce didacticiel vous explique comment connaître votre `{TENANT_ID}`identité, qui apparaît dans les appels, et comment créer des schémas, qui est utilisé pour créer un jeu de données à assimiler.

De plus, ce didacticiel nécessite que vous ayez déjà créé une connexion de diffusion en continu. Pour plus d&#39;informations sur la création d&#39;une connexion en flux continu, consultez le didacticiel [](./create-streaming-connection.md)Créer une connexion en flux continu.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API d’assimilation en flux continu.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Composer un schéma basé sur la classe de Profil XDM individuel

Pour créer un jeu de données, vous devez d&#39;abord créer un nouveau schéma qui implémente la classe de Profil XDM Individuel. Pour plus d&#39;informations sur la création de schémas, consultez le guide [du développeur de l&#39;API](../../xdm/api/getting-started.md)Schéma Registry.

**Format d’API**

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
| `title` | Nom à utiliser pour votre schéma. Ce nom doit être unique. |
| `description` | Description significative du schéma que vous créez. |
| `meta:immutableTags` | Dans cet exemple, la `union` balise est utilisée pour conserver vos données dans le Profil [client](../../profile/home.md)en temps réel. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 avec les détails de votre schéma nouvellement créé.

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
| `{TENANT_ID}` | Cet identifiant permet de s’assurer que les ressources que vous créez sont correctement espacées dans l’espace de noms et contenues dans votre organisation IMS. Pour plus d&#39;informations sur l&#39;ID du locataire, veuillez lire le guide [du registre des](../../xdm/api/getting-started.md#know-your-tenant-id)schémas. |

Veuillez prendre note des attributs `$id` et des `version` attributs, car ceux-ci seront utilisés lors de la création de votre jeu de données.

## Définir un descripteur d&#39;identité principal pour le schéma

Ensuite, ajoutez un descripteur [d&#39;](../../xdm/api/descriptors.md) identité au schéma créé ci-dessus, en utilisant l&#39;attribut d&#39;adresse électronique de travail comme identifiant principal. Cela entraînera deux modifications :

1. L&#39;adresse électronique de travail devient un champ obligatoire. Cela signifie que les messages envoyés sans ce champ ne seront pas validés et ne seront pas ingérés.

2. Le Profil du client en temps réel utilisera l’adresse électronique de travail comme identifiant pour rassembler plus d’informations sur cette personne.

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
| `{SCHEMA_REF_ID}` | Le `$id` que vous avez précédemment reçu lorsque vous avez composé le schéma. Il devrait ressembler à ceci : `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE] &#x200B; &#x200B; codes d&#39;Espace de nommage **d&#39;identité**
>
> Assurez-vous que les codes sont valides - l&#39;exemple ci-dessus utilise &quot;courriel&quot;, qui est un espace de nommage d&#39;identité standard. Vous trouverez d&#39;autres espaces de nommage d&#39;identité standard couramment utilisés dans la FAQ [du service](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)d&#39;identité.
>
> Si vous souhaitez créer un espace de nommage personnalisé, suivez les étapes décrites dans la présentation [de l&#39;espace de nommage](../../identity-service/home.md)d&#39;identité.

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 avec des informations sur le nouveau descripteur d’identité principal du schéma.

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

Une fois votre schéma créé, vous devez créer un jeu de données pour assimiler les données d&#39;enregistrement.

>[!NOTE] Ce jeu de données sera activé pour le Profil **client en temps** réel et le service **** d&#39;identité.

**Format d’API**

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

Une réponse réussie renvoie l&#39;état HTTP 201 et un tableau contenant l&#39;ID du jeu de données nouvellement créé au format `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Envoi de données d’enregistrement à la connexion de flux continu

Une fois le jeu de données et la connexion en flux continu en place, vous pouvez ingérer des enregistrements JSON au format XDM pour intégrer des données d’enregistrement dans la plate-forme.

**Format d’API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de la connexion de flux continu précédemment créée. |
| `synchronousValidation` | Paramètre de requête facultatif destiné au développement. S’il est défini sur `true`, il peut être utilisé pour des commentaires immédiats afin de déterminer si la demande a bien été envoyée. Par défaut, cette valeur est définie sur `false`. |

**Requête**

>[!NOTE] L’appel d’API suivant **ne nécessite aucun** en-tête d’authentification.

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

Une réponse réussie renvoie l’état HTTP 200 avec les détails du Profil nouvellement diffusé.

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
| `xactionId` | Un identifiant unique a généré côté serveur pour l&#39;enregistrement que vous venez d&#39;envoyer. Cet identifiant permet à Adobe de suivre le cycle de vie de cet enregistrement sur divers systèmes et avec le débogage. |
| `receivedTimeMs` | Horodatage (en millisecondes) qui indique l’heure de réception de la demande. |
| `synchronousValidation.status` | Comme le paramètre de requête `synchronousValidation=true` a été ajouté, cette valeur s’affiche. Si la validation a réussi, l’état est `pass`le suivant. |

## Récupérer les données d&#39;enregistrement nouvellement assimilées

Pour valider les enregistrements précédemment ingérés, vous pouvez utiliser l&#39;API [d&#39;accès au](../../profile/api/entities.md) Profil pour récupérer les données d&#39;enregistrement.

>[!NOTE] Si l’ID de stratégie de fusion n’est pas défini et le schéma.</span>name ou relatedSchema</span>.name est défini `_xdm.context.profile`, Profil Access récupère **toutes les** identités associées.

**Format d’API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Paramètre | Description |
| --------- | ----------- |
| `schema.name` | **Obligatoire.** Nom du schéma auquel vous accédez. |
| `entityId` | ID de l&#39;entité. Si cela est fourni, vous devez également fournir l’espace de nommage d’entité. |
| `entityIdNS` | espace de nommage de l’identifiant que vous tentez de récupérer. |

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

Une réponse réussie renvoie l&#39;état HTTP 200 avec les détails des entités demandées. Comme vous pouvez le voir, il s&#39;agit du même enregistrement qui a été correctement assimilé précédemment.

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

En lisant ce document, vous comprenez maintenant comment importer des données d’enregistrement dans la plate-forme à l’aide de connexions de flux continu. Vous pouvez essayer d’effectuer plus d’appels avec des valeurs différentes et de récupérer les valeurs mises à jour. De plus, vous pouvez début à surveiller vos données imbriquées via l’interface utilisateur de la plate-forme. Pour plus d&#39;informations, veuillez lire le guide d&#39;assimilation [des données de](../quality/monitor-data-flows.md) surveillance.

Pour plus d&#39;informations sur l&#39;assimilation en flux continu en général, veuillez lire l&#39;aperçu [de l&#39;assimilation en](../streaming-ingestion/overview.md)flux continu.


