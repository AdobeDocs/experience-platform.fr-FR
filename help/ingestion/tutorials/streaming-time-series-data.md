---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Diffusion en continu des données de séries chronologiques
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 3%

---


# Diffusion en continu des données de série chronologique vers l’Adobe Experience Platform

Ce didacticiel vous aidera à commencer à utiliser les API d&#39;assimilation en flux continu, qui font partie des API Adobe Experience Platform Data Ingestion Service.

## Prise en main

Ce didacticiel nécessite une connaissance pratique de divers services d&#39;Adobe Experience Platform. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d&#39;expérience.
- [Profil](../../profile/home.md)client en temps réel : Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de plusieurs sources.
- [Guide](../../xdm/api/getting-started.md)du développeur du registre des Schémas : Un guide complet qui couvre chacun des points de terminaison disponibles de l&#39;API de registre de Schéma et comment leur envoyer des appels. Ce didacticiel vous explique comment connaître votre `{TENANT_ID}`identité, qui apparaît dans les appels, et comment créer des schémas, qui est utilisé pour créer un jeu de données à assimiler.

De plus, ce didacticiel nécessite que vous ayez déjà créé une connexion de diffusion en continu. Pour plus d&#39;informations sur la création d&#39;une connexion en flux continu, consultez le didacticiel [](./create-streaming-connection.md)Créer une connexion en flux continu.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API d’assimilation en flux continu.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de l’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour passer des appels aux API Platform, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de l&#39;Experience Platform sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Composer un schéma basé sur la classe XDM ExperienceEvent

Pour créer un jeu de données, vous devez d&#39;abord créer un nouveau schéma qui implémente la classe XDM ExperienceEvent. Pour plus d&#39;informations sur la création de schémas, consultez le guide [du développeur de l&#39;API](../../xdm/api/getting-started.md)Schéma Registry.

**Format d’API**

```http
POST /schemaregistry/tenant/schemas
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
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
    "version": "{SCHEMA_VERSION}",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
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
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
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

>[!NOTE]
>
>&#x200B; &#x200B; codes d&#39;Espace de nommage **d&#39;identité**
>
> Assurez-vous que les codes sont valides - l&#39;exemple ci-dessus utilise &quot;courriel&quot;, qui est un espace de nommage d&#39;identité standard. Vous trouverez d&#39;autres espaces de nommage d&#39;identité standard couramment utilisés dans la FAQ [du service](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)d&#39;identité.
>
> Si vous souhaitez créer un espace de nommage personnalisé, suivez les étapes décrites dans la présentation [de l&#39;espace de nommage](../../identity-service/home.md)d&#39;identité.
**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 201 avec des informations sur l&#39;espace de nommage d&#39;identité principal nouvellement créé pour le schéma.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Création d’un jeu de données pour les données de série chronologique

Une fois votre schéma créé, vous devez créer un jeu de données pour assimiler les données d&#39;enregistrement.

>[!NOTE]
>
>Ce jeu de données sera activé pour le Profil **client et** l&#39;identité **en temps** réel en définissant les balises appropriées.

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
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
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
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## Envoi de données de série chronologique à la connexion en flux continu

Une fois le jeu de données et la connexion en flux continu en place, vous pouvez ingérer des enregistrements JSON au format XDM pour ingérer des données de série chronologique dans Platform.

**Format d’API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de votre nouvelle connexion de diffusion en continu. |
| `synchronousValidation` | Paramètre de requête facultatif destiné au développement. S’il est défini sur `true`, il peut être utilisé pour des commentaires immédiats afin de déterminer si la demande a bien été envoyée. Par défaut, cette valeur est définie sur `false`. |

**Requête**

>[!NOTE]
>
>Vous devrez générer vos propres `xdmEntity._id` et `xdmEntity.timestamp`. Un bon moyen de générer un identifiant est d’utiliser un UUID. De plus, l&#39;appel d&#39;API suivant **ne nécessite aucun** en-tête d&#39;authentification.


```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
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
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
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
| `receivedTimeMs`: Horodatage (en millisecondes) qui indique l’heure de réception de la demande. |
| `synchronousValidation.status` | Comme le paramètre de requête `synchronousValidation=true` a été ajouté, cette valeur s’affiche. Si la validation a réussi, l’état est `pass`le suivant. |

## Récupérer les données de série chronologique nouvellement assimilées

Pour valider les enregistrements précédemment assimilés, vous pouvez utiliser l&#39;API [d&#39;accès au](../../profile/api/entities.md) Profil pour récupérer les données de la série chronologique. Pour ce faire, vous pouvez utiliser une requête GET sur le point de `/access/entities` terminaison et des paramètres de requête facultatifs. Plusieurs paramètres peuvent être utilisés, séparés par des esperluettes (&amp;).&quot;

>[!NOTE]
>
>Si l’ID de stratégie de fusion n’est pas défini et le schéma.</span>name ou relatedSchema</span>.name est défini `_xdm.context.profile`, Profil Access récupère **toutes les** identités associées.

**Format d’API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Paramètre | Description |
| --------- | ----------- |
| `schema.name` | **Obligatoire.** Nom du schéma auquel vous accédez. |
| `relatedSchema.name` | **Obligatoire.** Puisque vous accédez à une `_xdm.context.experienceevent`variable, cette valeur spécifie le schéma de l&#39;entité de profil à laquelle les événements de séries chronologiques sont liés. |
| `relatedEntityId` | ID de l&#39;entité associée. Si cela est fourni, vous devez également fournir l’espace de nommage d’entité. |
| `relatedEntityIdNS` | espace de nommage de l’identifiant que vous tentez de récupérer. |

**Requête**

```shell
curl -X GET \
  https://platform-stage.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 200 avec les détails des entités demandées. Comme vous pouvez le voir, il s’agit des mêmes données de série chronologique qui ont été précédemment ingérées.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Étapes suivantes

En lisant ce document, vous comprenez maintenant comment ingérer des données d&#39;enregistrement dans Platform à l&#39;aide de connexions en flux continu. Vous pouvez essayer d’effectuer plus d’appels avec des valeurs différentes et de récupérer les valeurs mises à jour. De plus, vous pouvez début à surveiller vos données assimilées via l’interface utilisateur de Platform. Pour plus d&#39;informations, veuillez lire le guide d&#39;assimilation [des données de](../quality/monitor-data-flows.md) surveillance.

Pour plus d&#39;informations sur l&#39;assimilation en flux continu en général, veuillez lire l&#39;aperçu [de l&#39;assimilation en](../streaming-ingestion/overview.md)flux continu.
