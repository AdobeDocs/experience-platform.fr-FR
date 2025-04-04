---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion par flux;ingestion;données de série temporelle;diffusion de données de série temporelle;
solution: Experience Platform
title: Diffusion de données de série temporelle à l’aide des API d’ingestion en flux continu
type: Tutorial
description: Ce tutoriel vous aidera à commencer à utiliser les API d’ingestion par flux, qui font partie des API d’Adobe Experience Platform Data Ingestion Service.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 57%

---

# Diffusion de données de série temporelle à l’aide des API d’ingestion en flux continu

Ce tutoriel vous aidera à commencer à utiliser les API d’ingestion en flux continu, qui font partie des API [!DNL Data Ingestion Service] de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une connaissance pratique de différents services d’Adobe Experience Platform. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données d’expérience.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Guide de développement sur le registre des schémas](../../xdm/api/getting-started.md) : guide complet qui couvre chacun des points d’entrée disponibles de l’API [!DNL Schema Registry] et la manière d’effectuer des appels vers ceux-ci. Cela implique de connaître votre `{TENANT_ID}`, qui apparaît dans les appels de ce tutoriel, et de savoir comment créer des schémas utilisés pour la création d’un jeu de données destiné à être ingéré.

De plus, pour suivre ce tutoriel, vous devez avoir déjà créé une connexion en continu. Pour plus d’informations sur la création d’une connexion en continu, consultez le [tutoriel de création d’une connexion en continu](./create-streaming-connection.md).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../landing/api-guide.md).

## Composition d’un schéma basé sur la classe XDM ExperienceEvent

Pour créer un jeu de données, vous devez d’abord créer un schéma qui implémente la classe [!DNL XDM ExperienceEvent]. Pour plus d’informations sur la façon de créer des schémas, consultez le [guide de développement de l’API Schema Registry](../../xdm/api/getting-started.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `title` | Le nom que vous souhaitez utiliser pour votre schéma. Ce nom doit être unique. |
| `description` | Description significative du schéma que vous êtes en train de créer. |
| `meta:immutableTags` | Dans cet exemple, la balise `union` est utilisée pour conserver vos données dans [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails du schéma que vous venez de créer.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1",
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
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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
| `{TENANT_ID}` | Cet identifiant permet de s’assurer que les ressources que vous créez ont un espace de noms correct et sont contenues dans votre organisation. Pour plus d’informations sur l’identifiant du client, consultez le [guide du registre des schémas](../../xdm/api/getting-started.md#know-your-tenant-id). |

Prenez note des `$id` ainsi que des attributs `version`, ces deux éléments étant utilisés lors de la création du jeu de données.

## Définition d’un descripteur d’identité principal du schéma

Ajoutez ensuite un [descripteur d’identité](../../xdm/api/descriptors.md) au schéma créé ci-dessus, en utilisant l’attribut d’adresse e-mail de travail comme identifiant principal. Cela entraînera deux modifications :

1. L’adresse e-mail de travail deviendra un champ obligatoire. Cela signifie que les messages envoyés sans ce champ ne seront ni validés ni ingérés.

2. [!DNL Real-Time Customer Profile] utilisera l’adresse e-mail professionnelle comme identifiant pour rassembler plus d’informations sur cet individu.

### Requête

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{SCHEMA_REF_ID}` | Le `$id` précédemment reçu lorsque vous avez composé le schéma. La ligne devrait ressembler à ceci : `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;Codes **’Espace De Noms D’Identité**
>
> Assurez-vous que les codes sont valides. L’exemple ci-dessus utilise « email », qui est un espace de noms d’identité standard. Vous trouverez d’autres espaces de noms d’identité standard couramment utilisés dans la [FAQ du service d’identités](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Si vous souhaitez créer un espace de noms personnalisé, suivez les étapes décrites dans la [présentation de l’espace de noms d’identité](../../identity-service/home.md).

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 avec des informations sur l’espace de noms d’identité principal créé pour le schéma.

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
    "imsOrg": "{ORG_ID}"
}
```

## Création d’un jeu de données pour les données de série temporelle

Une fois que vous avez créé votre schéma, vous devez créer un jeu de données pour ingérer les données d’enregistrement.

>[!NOTE]
>
>Ce jeu de données sera activé pour **[!DNL Real-Time Customer Profile]** et **[!DNL Identity]** en définissant les balises appropriées.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
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
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```


## Création d’une connexion en continu

Après avoir créé votre schéma et votre jeu de données, vous devrez créer une connexion en continu pour ingérer vos données.

Pour plus d’informations sur la création d’une connexion en continu, consultez le [tutoriel de création d’une connexion en continu](./create-streaming-connection.md).

## Ingestion de données de série temporelle vers la connexion en continu

Une fois le jeu de données, la connexion en continu et le flux de données créés, vous pouvez ingérer des enregistrements JSON au format XDM pour ingérer des données de série temporelle dans [!DNL Experience Platform].

**Format d’API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | La valeur `id` de la connexion en continu que vous venez de créer. |
| `syncValidation` | Paramètre de requête facultatif destiné au développement. S’il est défini sur `true`, il peut être utilisé pour obtenir des commentaires immédiats afin de déterminer si la requête a bien été envoyée. Par défaut, cette valeur est définie sur `false`. Veuillez noter que si vous définissez ce paramètre de requête sur `true` que le débit de la requête sera limité à 60 fois par minute par `CONNECTION_ID`. |

**Requête**

L’ingestion de données de série temporelle vers une connexion en continu peut être effectuée avec ou sans le nom de la source.

L’exemple de requête ci-dessous ingère dans Experience Platform des données de série temporelle dont le nom de source est manquant. Si le nom de la source est manquant dans les données, l’identifiant de la source sera ajouté à partir de la définition de la connexion en continu.

Les champs `xdmEntity._id` et `xdmEntity.timestamp` sont obligatoires pour les données de série temporelle. L’attribut `xdmEntity._id` représente un identifiant unique pour l’enregistrement lui-même, **pas** un identifiant unique de la personne ou de l’appareil dont il s’agit dans l’enregistrement.

Vous devez générer vos propres `xdmEntity._id` et `xdmEntity.timestamp` pour l’enregistrement d’une manière qui reste cohérente si l’enregistrement doit être réingéré. Idéalement, votre système source contiendra ces valeurs. Si aucun ID n’est disponible, envisagez de concaténer les valeurs d’autres champs de l’enregistrement pour créer une valeur unique qui peut être régénérée de manière cohérente à partir de l’enregistrement lors de la réingestion.

>[!NOTE]
>
>L’appel API suivant ne nécessite **pas** d’en-têtes d’authentification.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
    "datasetId": "{DATASET_ID}",
    "flowId": "{FLOW_ID}",
    "imsOrgID": "{ORG_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            },
        "identityMap": {
                "Email": [
                  {
                    "id": "acme_user@gmail.com",
                    "primary": true
                  }
                ]
              },
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

Si vous souhaitez inclure un nom de source, l’exemple suivant montre comment l’inclure.

```json
    "header": {
    "datasetId": "{DATASET_ID}",
    "flowId": "{FLOW_ID}",
    "imsOrgID": "{ORG_ID}",
      "source": {
        "name": "ACME source"
      }
    }
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails du [!DNL Profile] nouvellement diffusé en continu.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `{CONNECTION_ID}` | `inletId` de la connexion en continu créée précédemment. |
| `xactionId` | Un identifiant unique généré côté serveur pour l’enregistrement que vous venez d’envoyer. Cet identifiant aide Adobe à suivre le cycle de vie de cet enregistrement sur différents systèmes et en cas de débogage. |
| `receivedTimeMs` : un horodatage (en millisecondes) indiquant l’heure de réception de la requête. |
| `syncValidation.status` | Le paramètre de requête `syncValidation=true` ayant été ajouté, cette valeur s’affiche. Si la validation a réussi, l’état est `pass`. |

## Récupération des données de série temporelle que vous venez d’ingérer

Pour valider les enregistrements précédemment ingérés, vous pouvez utiliser l’[[!DNL Profile Access API]](../../profile/api/entities.md) pour récupérer les données de série temporelle. Vous pouvez le faire en envoyant une requête GET au point d’entrée `/access/entities` et en utilisant des paramètres de requête facultatifs. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (&amp;).

>[!NOTE]
>
>Si l’ID de la politique de fusion n’est pas défini et que le `schema.name` ou le `relatedSchema.name` est `_xdm.context.profile`, [!DNL Profile Access] récupérera **toutes** les identités associées.

**Format d’API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Paramètre | Description |
| --------- | ----------- |
| `schema.name` | **Obligatoire.** Le nom du schéma auquel vous accédez. |
| `relatedSchema.name` | **Obligatoire.** Puisque vous accédez à un `_xdm.context.experienceevent`, cette valeur indique le schéma d’entité de profil auquel les événements de série temporelle sont associés. |
| `relatedEntityId` | L’identifiant de l’entité associée. Si cet identifiant est fourni, vous devez aussi fournir l’espace de noms de l’entité. |
| `relatedEntityIdNS` | L’espace de noms de l’identifiant que vous tentez de récupérer. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails des entités demandées. Comme vous pouvez le voir, il s’agit des données de série temporelle ingérées précédemment.

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

En lisant ce document, vous comprenez désormais comment ingérer des données d’enregistrement dans des [!DNL Experience Platform] à l’aide de connexions en continu. Vous pouvez essayer d’effectuer plus d’appels avec des valeurs différentes et de récupérer les valeurs mises à jour. De plus, vous pouvez commencer à surveiller vos données ingérées via [!DNL Experience Platform]’interface utilisateur. Pour plus d’informations, consultez le guide de [surveillance de l’ingestion des données](../quality/monitor-data-ingestion.md).

Pour plus d’informations sur l’ingestion par flux en général, consultez la [présentation de l’ingestion par flux](../streaming-ingestion/overview.md).
