---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Unions
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 88%

---


# Unions

Unions (or union views) are system-generated, read-only schemas that aggregate the fields of all schemas which share the same class ([!DNL XDM ExperienceEvent] or [!DNL XDM Individual Profile]) and are enabled for [[!DNL Real-time Customer Profile]](../../profile/home.md).

Ce document couvre les concepts essentiels pour travailler avec les unions dans l’API Schema Registry, y compris des exemples d’appels pour diverses opérations. Pour plus d’informations générales sur les unions dans XDM, consultez la section sur les unions dans le [Principe de base de la composition des schémas](../schema/composition.md#union).

## Mixins d’union

The [!DNL Schema Registry] automatically includes three mixins within the union schema: `identityMap`, `timeSeriesEvents`, and `segmentMembership`.

### Mappage d’identités

Un schéma d’union `identityMap` est une représentation des identités connues dans les schémas d’enregistrement associés de l’union. Le mappage d’identités sépare les identités en différents tableaux saisis par espace de noms. Chaque identité répertoriée est elle-même un objet contenant une valeur unique `id`.

Pour plus d’informations, voir la [documentation d’Identity Service](../../identity-service/home.md).

### Événements de série temporelle

Le tableau `timeSeriesEvents` est une liste d’événements de série temporelle liés aux schémas d’enregistrement associés à l’union. When [!DNL Profile] data is exported to datasets, this array is included for each record. Ceci est utile pour divers cas d’utilisation, tels que l’apprentissage automatique où les modèles ont besoin de l’historique complet du comportement d’un profil en plus de ses attributs d’enregistrement.

### Mappage de l’adhésion aux segments

Le mappage `segmentMembership` stocke les résultats des évaluations de segments. Lorsque les tâches de segmentation sont exécutées avec succès à l’aide de l’[API Segmentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml), le mappage est mis à jour. `segmentMembership` stocke également tous les segments d’audience pré-évalués qui sont ingérés dans Platform, permettant l’intégration avec d’autres solutions comme Adobe Audience Manager.

Pour plus d’informations, consultez le tutoriel sur la [création de segments à l’aide des API](../../segmentation/tutorials/create-a-segment.md).

## Activation d’un segment pour un abonnement à l’union

Pour qu’un schéma soit inclus dans l’union fusionnée, la balise « union » doit être ajoutée à l’attribut `meta:immutableTags` du schéma. Pour ce faire, vous devez effectuer une requête PATCH pour mettre à jour le schéma et ajouter le tableau `meta:immutableTags` avec une valeur « union ».

>[!NOTE]
>
>Les balises immuables sont des balises destinées à être configurées, mais jamais supprimées.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI encodé URL `$id` ou `meta:altId` du schéma que vous souhaitez activer pour une utilisation dans [!DNL Profile]. |

**Requête**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour, qui inclut désormais un tableau `meta:immutableTags` contenant la valeur de chaîne « union ».

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Liste d’unions

When you set the &quot;union&quot; tag on a schema, the [!DNL Schema Registry] automatically creates and maintains a union for the class upon which the schema is based. La valeur `$id` pour l’union est similaire à la norme `$id` d’une classe, la seule différence étant l’ajout de deux tirets bas et du mot « union » (`"__union"`).

Pour afficher une liste des unions disponibles, vous pouvez effectuer une requête GET auprès du point de terminaison `/unions`.

**Format d’API**

```http
GET /tenant/unions
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 (OK) et un tableau `results` dans le corps de la réponse. Si des unions ont été définies, les valeurs `title`, `$id`, `meta:altId` et `version` pour chaque union sont fournies comme des objets dans le tableau. Si aucune union n’a été définie, un état HTTP 200 (OK) est toujours renvoyé, mais le tableau `results` est vide.

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## Recherche d’une union spécifique

Vous pouvez voir une union spécifique en exécutant une requête GET qui inclut l’`$id` et, selon l’en-tête Accept, certains ou tous les détails de l’union.

>[!NOTE]
>
>Les recherches d’unions sont disponibles à l’aide des points de terminaison `/unions` et `/schemas`[!DNL Profile] afin de les activer pour les utiliser dans les exportations de dans un jeu de données.

**Format d’API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{UNION_ID}` | URI encodé URL `$id` de l’union que vous souhaitez rechercher. Les URI pour les schémas d’unions sont suivis de « __union ». |

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Les requêtes de recherche d’unions requièrent que `version` soit inclus dans l’en-tête Accept.

Les en-têtes Accept suivants sont disponibles pour les recherches de schémas d’unions :

| Accept | Description |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Raw avec `$ref` et `allOf`. Contient des titres et des descriptions. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | Attributs `$ref` et `allOf` résolus. Contient des titres et des descriptions. |

**Réponse**

Une réponse réussie renvoie la vue d’union de tous les schémas qui implémentent la classe dont le `$id` a été fourni dans le chemin de la requête.

Le format de la réponse dépend de l’en-tête Accept envoyé dans la requête. Testez différents en-têtes Accept pour comparer les réponses et déterminer l’en-tête qui convient le mieux à votre cas d’utilisation.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## Liste des schémas dans une union

Afin de voir quels schémas font partie d’une union spécifique, vous pouvez effectuer une requête GET en utilisant des paramètres de requête afin de filtrer les schémas dans le conteneur client.

En utilisant le paramètre de requête `property`, vous pouvez configurer la réponse afin de renvoyer uniquement les schémas contenant un champ `meta:immutableTags` et un `meta:class` égal à la classe de l’union à laquelle vous accédez.

**Format d’API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | Le `$id` de classe de l’union à laquelle vous souhaitez accéder. |

**Requête**

The following request looks up all schemas that are part of the [!DNL XDM Individual Profile] class union.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste filtrée de schémas, contenant uniquement ceux qui répondent aux deux exigences. N’oubliez pas que lorsque vous utilisez plusieurs paramètres de requête, une relation ET est présumée. Le format de la réponse dépend de l’en-tête Accept envoyé dans la requête.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
