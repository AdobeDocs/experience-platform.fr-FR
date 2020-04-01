---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Diffusion en flux continu des données de séries chronologiques
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Diffusion en continu des données de série chronologique vers Adobe Experience Platform

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

## Composer un  basé sur la classe XDM ExperienceEvent

Pour créer un jeu de données, vous devez d’abord créer un nouveau  qui implémente la classe XDM ExperienceEvent. Pour plus d&#39;informations sur la création de  de, veuillez lire le guide [du développeur de l&#39;API de registre de](../../xdm/api/getting-started.md).

**Format API**

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
| `{SCHEMA_REF_ID}` | Le `$id` que vous avez reçu précédemment lorsque vous avez composé le . Voici à quoi ça ressemble : `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE] &#x200B; &#x200B; codes de  d&#39; d&#39;identité&#x200B;****
>
> Assurez-vous que les codes sont valides - l&#39;exemple ci-dessus utilise &quot;email&quot;, qui est une identité  standard. Vous trouverez d&#39;autres  d&#39;identité standard couramment utilisés  dans la FAQ [du service](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)d&#39;identité.
>
> Si vous souhaitez créer un  de  personnalisé, suivez les étapes décrites dans la présentation [du de l&#39;](../../identity-service/home.md)identité  .
**Réponse**

Une réponse réussie renvoie l’état HTTP 201 avec des informations sur le nouveau d’identité principale  créé pour l’.

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

Une fois que vous avez créé votre  de, vous devez créer un jeu de données pour assimiler des données d’enregistrement.

>[!NOTE] Ce jeu de données sera activé pour les **en temps** réel des clients et de l’ **identité** en définissant les balises appropriées.

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

Une réponse réussie renvoie l’état HTTP 201 et un tableau contenant l’ID du jeu de données nouvellement créé au format `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## Envoi de données de série chronologique à la connexion en flux continu

Une fois le jeu de données et la connexion en flux continu en place, vous pouvez assimiler des enregistrements JSON au format XDM pour assimiler des données de série chronologique dans la plateforme.

**Format API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de votre nouvelle connexion de diffusion en continu. |
| `synchronousValidation` | Paramètre facultatif  destiné au développement. S’il est défini sur `true`, il peut être utilisé pour obtenir des commentaires immédiats afin de déterminer si la demande a bien été envoyée. Par défaut, cette valeur est définie sur `false`. |

**Requête**

>[!NOTE] Vous devrez générer les vôtres `xdmEntity._id` et `xdmEntity.timestamp`. Un bon moyen de générer un ID est d’utiliser un UUID. De plus, l’appel d’API suivant **ne nécessite pas** d’en-tête d’authentification.


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

Une réponse réussie renvoie l’état HTTP 200 avec les détails de la nouvelle  en flux continu.

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
| `receivedTimeMs`: Horodatage (en millisecondes) qui indique l’heure de réception de la demande. |
| `synchronousValidation.status` | Comme le paramètre  `synchronousValidation=true` a été ajouté, cette valeur s’affiche. Si la validation a réussi, l’état est `pass`. |

## Récupérer les données de série chronologique nouvellement assimilées

Pour valider les enregistrements précédemment assimilés, vous pouvez utiliser l’API [d’accès](../../profile/api/entities.md) aux  pour récupérer les données de la série chronologique. Cela peut être fait à l’aide d’une requête GET au `/access/entities` point de fin et à l’aide de paramètres de  facultatifs. Plusieurs paramètres peuvent être utilisés, séparés par des esperluettes (&amp;).&quot;

>[!NOTE] Si l’ID de stratégie de fusion n’est pas défini et que le n’est pas .</span>name ou relatedSchema</span>.name est `_xdm.context.profile`, Accès  récupérera **toutes les** identités associées.

**Format API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Paramètre | Description |
| --------- | ----------- |
| `schema.name` | **Obligatoire.** Nom du auquel vous accédez. |
| `relatedSchema.name` | **Obligatoire.** Puisque vous accédez à une `_xdm.context.experienceevent`, cette valeur spécifie le  de l&#39;entité  à laquelle les  de séries chronologiques sont liées. |
| `relatedEntityId` | ID de l’entité associée. Si cela est fourni, vous devez également fournir l&#39;entité  . |
| `relatedEntityIdNS` |  de l’ID que vous tentez de récupérer. |

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

Une réponse réussie renvoie l’état HTTP 200 avec les détails des entités demandées. Comme vous pouvez le voir, il s’agit des mêmes données de série chronologique qui ont été précédemment ingérées.

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

En lisant ce , vous comprenez maintenant comment assimiler des données d’enregistrement dans la plateforme à l’aide de connexions en flux continu. Vous pouvez essayer d’effectuer plus d’appels avec des valeurs différentes et de récupérer les valeurs mises à jour. De plus, vous pouvez  surveiller vos données assimilées via l’interface utilisateur de la plateforme. Pour plus d&#39;informations, veuillez lire le guide d&#39;assimilation [des données de](../quality/monitor-data-flows.md) surveillance.

Pour plus d&#39;informations sur l&#39;ingestion en flux continu en général, veuillez lire l&#39;aperçu [de l&#39;ingestion en](../streaming-ingestion/overview.md)flux continu.
