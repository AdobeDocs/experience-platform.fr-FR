---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Unions
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 2%

---


# Unions

Les Unions (ou vues d’union) sont des schémas générés par le système et en lecture seule qui agrégat les champs de tous les schémas qui partagent la même classe (XDM ExperienceEvent ou XDM Individuel Profil) et sont activés pour le Profil [client en temps](../../profile/home.md)réel.

Ce document aborde les concepts essentiels pour travailler avec des unions dans l&#39;API de registre de Schéma, y compris les exemples d&#39;appels à diverses opérations. Pour des informations plus générales sur les unions dans XDM, voir la section sur les unions dans les [bases de la composition](../schema/composition.md#union)des schémas.

## Mélanges Union

Le registre des Schémas comprend automatiquement trois mixins dans le schéma des unions : `identityMap`, `timeSeriesEvents`et `segmentMembership`.

### Carte d’identité

Un schéma d’union `identityMap` est une représentation des identités connues au sein des schémas d’enregistrement associés à l’union. La carte d&#39;identité sépare les identités en différentes matrices de clés par espace de nommage. Chaque identité répertoriée est elle-même un objet contenant une `id` valeur unique.

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### événements de séries chronologiques

Le `timeSeriesEvents` tableau est une liste de événements de séries chronologiques qui se rapportent aux schémas d&#39;enregistrement associés à l&#39;union. Lorsque les données de Profil sont exportées vers des jeux de données, ce tableau est inclus pour chaque enregistrement. Cela s’avère utile pour divers cas d’utilisation, tels que l’apprentissage automatique, où les modèles ont besoin d’un historique de comportement complet du profil en plus de ses attributs d’enregistrement.

### Mappage d’appartenance aux segments

Le `segmentMembership` mappage stocke les résultats des évaluations de segments. Lorsque les tâches de segmentation sont exécutées avec succès à l’aide de l’API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentation, le mappage est mis à jour. `segmentMembership` stocke également tous les segments d’audience préévalués qui sont ingérés dans Platform, ce qui permet l’intégration à d’autres solutions telles que l’Adobe Audience Manager.

Pour plus d’informations, consultez le didacticiel sur la [création de segments à l’aide d’API](../../segmentation/tutorials/create-a-segment.md) .

## Activation d’un schéma pour l’adhésion à l’union

Pour qu’un schéma soit inclus dans la vue d’union fusionnée, la balise &quot;union&quot; doit être ajoutée à l’ `meta:immutableTags` attribut du schéma. Pour ce faire, PATCH demande de mettre à jour le schéma et d&#39;ajouter le `meta:immutableTags` tableau avec la valeur &quot;union&quot;.

>[!NOTE]
>
>Les balises immuables sont des balises destinées à être définies, mais jamais supprimées.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` codé URL ou `meta:altId` du schéma que vous souhaitez activer pour une utilisation dans le Profil. |

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

Une réponse réussie renvoie les détails du schéma mis à jour, qui inclut désormais un `meta:immutableTags` tableau contenant la valeur de chaîne &quot;union&quot;.

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

## unions Listes

Lorsque vous définissez la balise &quot;union&quot; sur un schéma, le registre des Schémas crée et conserve automatiquement une union pour la classe sur laquelle le schéma est basé. Le nom `$id` de l&#39;union est similaire à celui `$id` d&#39;une classe, la seule différence étant que deux traits de soulignement et le mot &quot;union&quot; (`"__union"`) sont ajoutés.

Pour vue d’une liste d’unions disponibles, vous pouvez exécuter une requête GET sur le `/unions` point de terminaison.

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

Une réponse réussie renvoie l’état HTTP 200 (OK) et un `results` tableau dans le corps de la réponse. Si des unions ont été définies, les `title`, `$id`, `meta:altId``version` et pour chaque union sont fournis en tant qu&#39;objets dans le tableau. Si aucune union n&#39;a été définie, l&#39;état HTTP 200 (OK) est toujours renvoyé, mais la `results` baie sera vide.

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

## Rechercher une union spécifique

Vous pouvez vue à une union spécifique en exécutant une requête GET qui inclut le `$id` et, selon l’en-tête Accepter, certains ou tous les détails de l’union.

>[!NOTE]
>
>Les recherches d’Unions sont disponibles à l’aide du point de terminaison `/unions` et `/schemas` afin de les activer pour une utilisation dans les exportations de Profil dans un jeu de données.

**Format d’API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{UNION_ID}` | URI codée `$id` URL de l’union à rechercher. Les URI des schémas d’union sont ajoutés avec &quot;__union&quot;. |

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

Les demandes de recherche d’Union doivent `version` être incluses dans l’en-tête Accepter.

Les en-têtes Accepter suivants sont disponibles pour les recherches de schéma d’union :

| Accepter | Description |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Raw avec `$ref` et `allOf`. Inclut des titres et des descriptions. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` attributs et `allOf` résolus. Inclut des titres et des descriptions. |

**Réponse**

Une réponse réussie renvoie la vue d&#39;union de tous les schémas qui implémentent la classe dont `$id` le chemin d&#39;accès à la requête contient la classe.

Le format de réponse dépend de l’en-tête Accepter envoyé dans la requête. Testez différents en-têtes Accepter pour comparer les réponses et déterminer l’en-tête qui convient le mieux à votre cas d’utilisation.

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

## schémas de Liste dans une union

Pour déterminer quels schémas font partie d&#39;une union spécifique, vous pouvez exécuter une requête GET à l&#39;aide des paramètres de requête pour filtrer les schémas dans le conteneur locataire.

En utilisant le paramètre `property` requête, vous pouvez configurer la réponse pour qu&#39;elle renvoie uniquement des schémas contenant un `meta:immutableTags` champ et un `meta:class` égal à la classe dont vous accédez à l&#39;union.

**Format d’API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | La `$id` classe dont vous souhaitez accéder à l&#39;union. |

**Requête**

La requête suivante recherche tous les schémas qui font partie de l&#39;union de classe de Profil XDM.

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

Une réponse réussie renvoie une liste filtrée de schémas, contenant uniquement ceux qui satisfont aux deux exigences. N’oubliez pas que lorsque vous utilisez plusieurs paramètres de requête, une relation ET est supposée. Le format de la réponse dépend de l’en-tête Accepter envoyé dans la requête.

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
