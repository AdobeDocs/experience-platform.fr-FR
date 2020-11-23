---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;union;Union;unions;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Unions
description: Le point de terminaison /unions de l'API Schéma Registry vous permet de gérer par programmation les schémas d'union XDM dans votre application d'expérience.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 53%

---


# Point de terminaison des Unions

Unions (or union views) are system-generated, read-only schemas that aggregate the fields of all schemas which share the same class ([!DNL XDM ExperienceEvent] or [!DNL XDM Individual Profile]) and are enabled for [[!DNL Real-time Customer Profile]](../../profile/home.md).

Ce document couvre les concepts essentiels pour travailler avec les unions dans l’API Schema Registry, y compris des exemples d’appels pour diverses opérations. Pour plus d’informations générales sur les unions dans XDM, consultez la section sur les unions dans le [Principe de base de la composition des schémas](../schema/composition.md#union).

## Champs de schéma Union

Le [!DNL Schema Registry] schéma d’union comprend automatiquement trois champs clés : `identityMap`, `timeSeriesEvents`et `segmentMembership`.

### Mappage d’identités

Un schéma d’union `identityMap` est une représentation des identités connues dans les schémas d’enregistrement associés de l’union. Le mappage d’identités sépare les identités en différents tableaux saisis par espace de noms. Chaque identité répertoriée est elle-même un objet contenant une valeur unique `id`. Pour plus d’informations, voir la [documentation d’Identity Service](../../identity-service/home.md).

### Événements de série temporelle

Le tableau `timeSeriesEvents` est une liste d’événements de série temporelle liés aux schémas d’enregistrement associés à l’union. Lorsque les données de profil sont exportées vers des jeux de données, ce tableau est inclus pour chaque enregistrement. Ceci est utile pour divers cas d’utilisation, tels que l’apprentissage automatique où les modèles ont besoin de l’historique complet du comportement d’un profil en plus de ses attributs d’enregistrement.

### Mappage de l’adhésion aux segments

Le mappage `segmentMembership` stocke les résultats des évaluations de segments. Lorsque les tâches de segmentation sont exécutées avec succès à l’aide de l’[API Segmentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml), le mappage est mis à jour. `segmentMembership` stocke également tous les segments d’audience pré-évalués qui sont ingérés dans Platform, permettant l’intégration avec d’autres solutions comme Adobe Audience Manager. Pour plus d’informations, consultez le tutoriel sur la [création de segments à l’aide des API](../../segmentation/tutorials/create-a-segment.md).

## Retrieve a list of unions {#list}

Lorsque vous définissez la `union` balise sur un schéma, la [!DNL Schema Registry] balise ajoute automatiquement le schéma à l&#39;union de la classe sur laquelle le schéma est basé. S&#39;il n&#39;existe aucune union pour la classe en question, une nouvelle union est automatiquement créée. The `$id` for the union is similar to the standard `$id` of other [!DNL Schema Registry] resources, with the only difference being that is appended by two underscores and the word &quot;union&quot; (`__union`).

Vous pouvez vue une liste d’unions disponibles en adressant une demande de GET au point de `/tenant/unions` terminaison.

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

The response format depends on the `Accept` header sent in the request. The following `Accept` headers are available for listing unions:

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Returns full JSON class for each resource, with original `$ref` and `allOf` included. (Limite : 300) |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 (OK) et un tableau `results` dans le corps de la réponse. Si des unions ont été définies, les détails de chaque union sont fournis en tant qu&#39;objets dans le tableau. Si aucune union n’a été définie, un état HTTP 200 (OK) est toujours renvoyé, mais le tableau `results` est vide.

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

## Look up a union {#lookup}

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
| `{UNION_ID}` | The URL-encoded `$id` URI of the union you want to look up. Les URI pour les schémas d’unions sont suivis de « __union ». |

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

## Activation d’un segment pour un abonnement à l’union {#enable}

Pour qu’un schéma soit inclus dans l’union de sa classe, une `union` balise doit être ajoutée à l’attribut de schéma `meta:immutableTags` . Pour ce faire, vous pouvez lancer une demande de PATCH pour ajouter un `meta:immutableTags` tableau avec une seule valeur de chaîne de `union` au schéma en question. Consultez le guide [des points de terminaison](./schemas.md#union) des schémas pour obtenir un exemple détaillé.

## Liste des schémas dans une union {#list-schemas}

Pour déterminer les schémas qui font partie d’une union spécifique, vous pouvez exécuter une demande de GET sur le point de `/tenant/schemas` terminaison. En utilisant le paramètre de requête `property`, vous pouvez configurer la réponse afin de renvoyer uniquement les schémas contenant un champ `meta:immutableTags` et un `meta:class` égal à la classe de l’union à laquelle vous accédez.

**Format d’API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | La `$id` classe dont vous souhaitez liste les schémas activés pour les unions. |

**Requête**

La requête suivante récupère une liste de tous les schémas qui font partie de l&#39;union de la [!DNL XDM Individual Profile] classe.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. The following `Accept` headers are available for listing schemas:

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie la totalité du schéma JSON de chaque ressource, en incluant le `$ref` et l’`allOf` d’origine. (Limite : 300) |

**Réponse**

Une réponse réussie renvoie une liste filtrée de schémas, contenant uniquement ceux qui appartiennent à la classe spécifiée et qui ont été activés pour l&#39;adhésion à l&#39;union. N’oubliez pas que lorsque vous utilisez plusieurs paramètres de requête, une relation ET est présumée.

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
