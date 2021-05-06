---
keywords: Experience Platform ; accueil ; rubriques populaires ; assimilation en flux continu ; assimilation ; données d'enregistrement ; données d'enregistrement de flux ;
solution: Experience Platform
title: Diffusion en continu des données d'enregistrement à l'aide des API d'importation en flux continu
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel vous aidera à commencer à utiliser les API d’ingestion par flux, qui font partie des API d’Adobe Experience Platform Data Ingestion Service.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
translation-type: tm+mt
source-git-commit: 544eeb3a27d0b218885e3000deb214f21c8e9fcd
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 75%

---


# Diffusion en continu des données d&#39;enregistrement à l&#39;aide des API d&#39;importation en flux continu

Ce didacticiel vous aidera à commencer à utiliser les API d&#39;assimilation en flux continu, qui font partie des [!DNL Data Ingestion Service] API Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une connaissance pratique de différents services d’Adobe Experience Platform. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel  [!DNL Platform] organiser les données d’expérience.
   - [Guide de développement du registre des schémas](../../xdm/api/getting-started.md)[!DNL Schema Registry] : guide complet abordant chacun des points de terminaison disponibles de l’API et la manière d’effectuer des appels vers ceux-ci. Cela implique de connaître votre `{TENANT_ID}`, qui apparaît dans les appels de ce tutoriel, et de savoir comment créer des schémas utilisés pour la création d’un jeu de données destiné à être ingéré.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de sources multiples.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API d’ingestion par flux.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Composer un schéma basé sur la classe [!DNL XDM Individual Profile]

Pour créer un jeu de données, vous devez d&#39;abord créer un nouveau schéma qui implémente la classe [!DNL XDM Individual Profile]. Pour plus d’informations sur la façon de créer des schémas, consultez le [guide de développement de l’API Schema Registry](../../xdm/api/getting-started.md).

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
| `title` | Le nom que vous souhaitez utiliser pour votre schéma. Ce nom doit être unique. |
| `description` | Description significative du schéma que vous êtes en train de créer. |
| `meta:immutableTags` | Dans cet exemple, la balise `union` est utilisée pour conserver vos données dans [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails du schéma que vous venez de créer.

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
| `{TENANT_ID}` | Cet identifiant est utilisé pour assurer que les espaces de noms des ressources que vous créez sont corrects et contenus dans votre organisation IMS. Pour plus d’informations sur l’identifiant du client, consultez le [guide du registre des schémas](../../xdm/api/getting-started.md#know-your-tenant-id). |

Prenez note des `$id` ainsi que des attributs `version`, ces deux éléments étant utilisés lors de la création du jeu de données.

## Définition d’un descripteur d’identité principal du schéma

Ajoutez ensuite un [descripteur d’identité](../../xdm/api/descriptors.md) au schéma créé ci-dessus, en utilisant l’attribut d’adresse e-mail de travail comme identifiant principal. Cela entraînera deux modifications :

1. L’adresse e-mail de travail deviendra un champ obligatoire. Cela signifie que les messages envoyés sans ce champ ne seront ni validés ni ingérés.

2. [!DNL Real-time Customer Profile] utilisera l’adresse e-mail de travail comme identifiant pour rassembler plus d’informations sur cette personne.

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
| `{SCHEMA_REF_ID}` | Le `$id` précédemment reçu lorsque vous avez composé le schéma. La ligne devrait ressembler à ceci : `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Codes d’espaces de noms d’identité**
>
> Assurez-vous que les codes sont valides. L’exemple ci-dessus utilise « email », qui est un espace de noms d’identité standard. Vous trouverez d’autres espaces de noms d’identité standard couramment utilisés dans la [FAQ d’Identity Service](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Si vous souhaitez créer un espace de noms personnalisé, suivez les étapes décrites dans la [présentation de l’espace de noms d’identité](../../identity-service/home.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec des informations sur le descripteur d’identité principal créé pour le schéma.

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

Une fois que vous avez créé votre schéma, vous devez créer un jeu de données pour ingérer les données d’enregistrement.

>[!NOTE]
>
>Ce jeu de données sera activé pour **[!DNL Real-time Customer Profile]** et **[!DNL Identity Service]**.

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
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 et un tableau contenant l’identifiant du jeu de données que vous venez de créer au format `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Création d’une connexion en continu

Après avoir créé votre schéma et votre jeu de données, vous pouvez créer une connexion de flux continu.

Pour plus d’informations sur la création d’une connexion en continu, consultez le [tutoriel de création d’une connexion en continu](./create-streaming-connection.md).

## Ingestion de données d’enregistrement vers la connexion en continu {#ingest-data}

Une fois le jeu de données et la connexion en continu en place, vous pouvez ingérer des enregistrements JSON au format XDM pour ingérer des données d’enregistrement dans [!DNL Platform].

**Format d’API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | La valeur `inletId` de la connexion en continu que vous avez créée précédemment. |
| `synchronousValidation` | Un paramètre de requête facultatif destiné au développement. S’il est défini sur `true`, il peut être utilisé pour obtenir des commentaires immédiats afin de déterminer si la requête a bien été envoyée. Par défaut, cette valeur est définie sur `false`. |

**Requête**

L’insertion de données d’enregistrement dans une connexion de flux continu peut se faire avec ou sans le nom source.

L&#39;exemple de requête ci-dessous ingère un enregistrement dont le nom source est absent à la plate-forme. Si le nom source est absent d’un enregistrement, celui-ci ajoute l’ID source de la définition de connexion de flux continu.

>[!NOTE]
>
>L’appel API suivant ne nécessite **pas** d’en-têtes d’authentification.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
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

Si vous souhaitez inclure un nom source, l’exemple suivant montre comment l’inclure.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 200 avec les détails du [!DNL Profile] nouvellement diffusé.

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
| `{CONNECTION_ID}` | L’identifiant de la connexion en continu précédemment créée. |
| `xactionId` | Un identifiant unique généré côté serveur pour l’enregistrement que vous venez d’envoyer. Cet identifiant aide Adobe à suivre le cycle de vie de cet enregistrement sur différents systèmes et en cas de débogage. |
| `receivedTimeMs` | Un horodatage (en millisecondes) indiquant l’heure de réception de la requête. |
| `synchronousValidation.status` | Le paramètre de requête `synchronousValidation=true` ayant été ajouté, cette valeur s’affiche. Si la validation a réussi, l’état est `pass`. |

## Récupération des données d’enregistrement nouvellement ingérées

Pour valider les enregistrements précédemment assimilés, vous pouvez utiliser [[!DNL Profile Access API]](../../profile/api/entities.md) pour récupérer les données d&#39;enregistrement.

>[!NOTE]
>
>Si l&#39;ID de stratégie de fusion n&#39;est pas défini et que `schema.name` ou `relatedSchema.name` est `_xdm.context.profile`, [!DNL Profile Access] récupère **toutes** les identités associées.

**Format d’API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Paramètre | Description |
| --------- | ----------- |
| `schema.name` | **Obligatoire.** Le nom du schéma auquel vous accédez. |
| `entityId` | Identifiant de l’entité. Si cet identifiant est fourni, vous devez aussi fournir l’espace de noms de l’entité. |
| `entityIdNS` | L’espace de noms de l’identifiant que vous tentez de récupérer. |

**Requête**

Vous pouvez consulter les données d’enregistrement précédemment ingérées à l’aide de la requête GET suivante.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails des entités demandées. Comme vous pouvez le voir, il s’agit du même enregistrement qui a été ingéré avec succès plus tôt.

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

En lisant ce document, vous comprenez maintenant comment ingérer des données d&#39;enregistrement dans [!DNL Platform] à l&#39;aide de connexions en flux continu. Vous pouvez essayer d’effectuer plus d’appels avec des valeurs différentes et de récupérer les valeurs mises à jour. De plus, vous pouvez début à surveiller vos données imbriquées par le biais de l&#39;interface utilisateur [!DNL Platform]. Pour plus d’informations, consultez le guide de [surveillance de l’ingestion des données](../quality/monitor-data-ingestion.md).

Pour plus d’informations sur l’ingestion par flux en général, consultez la [présentation de l’ingestion par flux](../streaming-ingestion/overview.md).
