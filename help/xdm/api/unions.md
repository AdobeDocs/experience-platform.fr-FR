---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;union;union;unions;unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Point de terminaison de l’API Unions
description: Le point d’entrée /unions de l’API Schema Registry vous permet de gérer par programmation les schémas d’union XDM dans votre application d’expérience.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 50%

---

# Point d’entrée Unions

Les unions (ou vues d’union) sont des schémas en lecture seule générés par le système qui regroupent les champs de tous les schémas qui partagent la même classe ([!DNL XDM ExperienceEvent] ou [!DNL XDM Individual Profile]) et sont activés pour [[!DNL Real-Time Customer Profile]](../../profile/home.md).

Ce document couvre les concepts essentiels pour travailler avec les unions dans l’API Schema Registry, y compris des exemples d’appels pour diverses opérations. Pour plus d’informations générales sur les unions dans XDM, consultez la section sur les unions dans le [Principe de base de la composition des schémas](../schema/composition.md#union).

## Champs de schéma d’union

Le [!DNL Schema Registry] inclut automatiquement trois champs clés dans un schéma d’union : `identityMap`, `timeSeriesEvents`, et `segmentMembership`.

### Mappage d’identités

Un schéma d’union `identityMap` est une représentation des identités connues dans les schémas d’enregistrement associés de l’union. Le mappage d’identités sépare les identités en différents tableaux saisis par espace de noms. Chaque identité répertoriée est elle-même un objet contenant une valeur unique `id`. Pour plus d’informations, voir la [documentation d’Identity Service](../../identity-service/home.md).

### Événements de série temporelle

Le tableau `timeSeriesEvents` est une liste d’événements de série temporelle liés aux schémas d’enregistrement associés à l’union. Lorsque les données de profil sont exportées vers des jeux de données, ce tableau est inclus pour chaque enregistrement. Ceci est utile pour divers cas d’utilisation, tels que le machine learning où les modèles ont besoin de l’historique complet du comportement d’un profil en plus de ses attributs d’enregistrement.

### Mappage de l’adhésion aux segments

Le mappage `segmentMembership` stocke les résultats des évaluations de segments. Lorsque les tâches de segmentation sont exécutées avec succès à l’aide de l’[API Segmentation](https://www.adobe.io/experience-platform-apis/references/segmentation/), le mappage est mis à jour. `segmentMembership` stocke également tous les segments d’audience pré-évalués qui sont ingérés dans Platform, permettant l’intégration avec d’autres solutions comme Adobe Audience Manager. Pour plus d’informations, consultez le tutoriel sur la [création de segments à l’aide des API](../../segmentation/tutorials/create-a-segment.md).

## Récupération d’une liste d’unions {#list}

Lorsque vous définissez la variable `union` sur un schéma, la balise [!DNL Schema Registry] ajoute automatiquement le schéma à l’union pour la classe sur laquelle le schéma est basé. S’il n’existe aucune union pour la classe en question, une nouvelle union est automatiquement créée. Le `$id` pour l’union est similaire à la norme `$id` d’autres [!DNL Schema Registry] ressources, à la seule différence près que est ajouté deux traits de soulignement et le mot &quot;union&quot; (`__union`).

Vous pouvez afficher une liste des unions disponibles en adressant une demande de GET au `/tenant/unions` point de terminaison .

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

Le format de réponse dépend de la variable `Accept` en-tête envoyé dans la requête. Les éléments suivants `Accept` Des en-têtes sont disponibles pour répertorier les unions :

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un court résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour répertorier les ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie la classe JSON complète pour chaque ressource, avec l’élément d’origine `$ref` et `allOf` inclus. (Limite : 300) |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 (OK) et un tableau `results` dans le corps de la réponse. Si des unions ont été définies, les détails de chaque union sont fournis sous la forme d’objets dans le tableau. Si aucune union n’a été définie, un état HTTP 200 (OK) est toujours renvoyé, mais le tableau `results` est vide.

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

## Recherche d’une union {#lookup}

Vous pouvez voir une union spécifique en exécutant une requête GET qui inclut l’`$id` et, selon l’en-tête Accept, certains ou tous les détails de l’union.

>[!NOTE]
>
>Les recherches d’unions sont disponibles à l’aide des points d’entrée `/unions` et `/schemas`[!DNL Profile] afin de les activer pour les utiliser dans les exportations de dans un jeu de données.

**Format d’API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{UNION_ID}` | Codé URL `$id` URI de l’union que vous souhaitez rechercher. Les URI pour les schémas d’unions sont suivis de « __union ». |

{style="table-layout:auto"}

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Les requêtes de recherche d’unions requièrent que `version` soit inclus dans l’en-tête Accept.

Les en-têtes Accept suivants sont disponibles pour les recherches de schémas d’unions :

| Accept | Description |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw avec `$ref` et `allOf`. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version=1` | Attributs `$ref` et `allOf` résolus. Contient des titres et des descriptions. |

{style="table-layout:auto"}

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

Pour qu’un schéma soit inclus dans l’union pour sa classe, une `union` doit être ajoutée à la balise `meta:immutableTags` attribut. Pour ce faire, vous pouvez envoyer une requête de PATCH pour ajouter une `meta:immutableTags` tableau avec une seule valeur de chaîne de `union` au schéma en question. Voir [guide de point d’entrée des schémas](./schemas.md#union) pour un exemple détaillé.

## Liste des schémas dans une union {#list-schemas}

Pour identifier les schémas qui font partie d’une union spécifique, vous pouvez exécuter une requête de GET sur la variable `/tenant/schemas` point de terminaison . En utilisant le paramètre de requête `property`, vous pouvez configurer la réponse afin de renvoyer uniquement les schémas contenant un champ `meta:immutableTags` et un `meta:class` égal à la classe de l’union à laquelle vous accédez.

**Format d’API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | Le `$id` de la classe dont vous souhaitez répertorier les schémas activés pour l’union. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère une liste de tous les schémas qui font partie de l’union pour la variable [!DNL XDM Individual Profile] classe .

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de réponse dépend de la variable `Accept` en-tête envoyé dans la requête. Les éléments suivants `Accept` Les en-têtes sont disponibles pour répertorier les schémas :

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un court résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour répertorier les ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie la totalité du schéma JSON de chaque ressource, en incluant le `$ref` et l’`allOf` d’origine. (Limite : 300) |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie une liste filtrée de schémas, contenant uniquement ceux qui appartiennent à la classe spécifiée et qui ont été activés pour l’adhésion à l’union. N’oubliez pas que lorsque vous utilisez plusieurs paramètres de requête, une relation ET est présumée.

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
