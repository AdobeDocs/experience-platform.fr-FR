---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' '
topic: developer guide
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


#  

  de (ou  de de) sont des générés par le système, en lecture seule, qui permettent de [les champs de tous les](../../profile/home.md)segments de la même classe (XDM ExperienceEvent ou XDM Individuel) et qui sont activés pour lescénario d’événement client en temps réel.

Ce décrit les concepts essentiels pour travailler avec  dans l&#39;API de registre des, y compris les exemples d&#39;appels pour diverses opérations. Pour plus d&#39;informations sur   de XDM, consultez la section sur les  de de  dans les [bases de la composition](../schema/composition.md#union)de l&#39;.

##  mixins 

Le registre des  de comprend automatiquement trois mixins dans lede  de : `identityMap`, `timeSeriesEvents`et `segmentMembership`.

### Carte d’identité

Un   est une représentation des identités connues au sein de l’d’enregistrements associé au `identityMap` . La carte d’identité sépare les identités en différents tableaux clés par  . Chaque identité répertoriée est elle-même un objet contenant une `id` valeur unique.

See the [Identity Service documentation](../../identity-service/home.md) for more information.

###  de la série chronologique

Le `timeSeriesEvents` tableau est un de  de séries chronologiques  qui se rapportent aux  d&#39;enregistrement qui sont associés au de la série de rapports. Lorsque  données sont exportées vers des jeux de données, ce tableau est inclus pour chaque enregistrement. Cela s’avère utile pour divers cas d’utilisation, tels que l’apprentissage automatique, où les modèles nécessitent un  l’historique complet du comportement en plus de ses attributs d’enregistrement.

### Mappage d’appartenance à un segment

Le `segmentMembership` mappage stocke les résultats des évaluations de segments. Lorsque les tâches de segmentation sont exécutées avec succès à l’aide de l’API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentation, le mappage est mis à jour. `segmentMembership` stocke également tous les segments   préévalués qui sont assimilés dans Platform, ce qui permet l’intégration à d’autres solutions telles qu’Adobe  Manager.

Pour plus d’informations, consultez le didacticiel sur la [création de segments à l’aide d’API](../../segmentation/tutorials/create-a-segment.md) .

## Activer un  pour  abonnement

Pour qu’un soit inclus dans le `meta:immutableTags` de l’ fusionné, la balise &quot;&quot; doit être ajoutée à l’attribut de l’. Pour ce faire, vous devez effectuer une demande PATCH pour mettre à jour le  de et ajouter le `meta:immutableTags` tableau avec la valeur &quot; &quot;.

>[!NOTE] Les balises immuables sont des balises destinées à être définies, mais jamais supprimées.

**Format API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI codé en URL `$id` ou `meta:altId` du que vous souhaitez activer pour une utilisation dans les . |

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

Une réponse réussie renvoie les détails de la  de mise à jour, qui inclut désormais un `meta:immutableTags` tableau contenant la valeur de chaîne &quot; &quot;.

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

##   

Lorsque vous définissez la balise &quot; &quot; sur un, le registre descrée et conserve automatiquement un de la classe sur laquelle leest basé. La valeur `$id` pour le   est similaire à la norme `$id` d’une classe, la seule différence étant qu’elle est annexée par deux traits de soulignement et le mot &quot; &quot; (`"__union"`).

Pour  un d’un  de  de  disponible, vous pouvez exécuter une requête GET sur le `/unions` point de terminaison.

**Format API**

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

Une réponse réussie renvoie l’état HTTP 200 (OK) et un `results` tableau dans le corps de la réponse. Si   de ont été définis, le `title`, `$id`, `meta:altId``version` et pour chaque  de sont fournis comme des objets dans le tableau. Si aucun   n&#39;a été défini, l&#39;état HTTP 200 (OK) est toujours renvoyé, mais le `results` tableau est vide.

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

## Recherchez un  spécifique 

Vous pouvez un  spécifique en exécutant une requête GET qui inclut la partie `$id` et, selon l’en-tête Accepter, certains ou tous les détails du.

>[!NOTE]   recherches de sont disponibles à l’aide du `/unions` `/schemas` point de terminaison et du point de terminaison afin de les activer pour les utiliser dans les exportations de dans un jeu de données.

**Format API**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{UNION_ID}` | URI codée `$id` URL du   que vous souhaitez rechercher. Les URI pour    sont ajoutés avec &quot;__&quot;. |

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

 demandes de recherche  doivent être `version` incluses dans l’en-tête Accepter.

Les en-têtes Accepter suivants sont disponibles pour   recherches de  :

| Accepter | Description |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Raw avec `$ref` et `allOf`. Inclut des titres et des descriptions. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` et `allOf` résolus. Inclut des titres et des descriptions. |

**Réponse**

Une réponse réussie renvoie l’ de tous les `$id` qui implémentent la classe dont le chemin d’accès à la requêtea été fourni.

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

##    dans un 

Pour savoir quel fait partie d&#39;un  de spécifique, vous pouvez exécuter une requête GET à l&#39;aide des paramètres depour filtrer le du client dans ledu client.

En utilisant le paramètre `property` , vous pouvez configurer la réponse afin de renvoyer uniquement les  de contenant un `meta:immutableTags` champ et un `meta:class` égal à la classe dont vous accédez au.

**Format API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | La `$id` classe à laquelle vous  accéder. |

**Requête**

La requête suivante recherche tous les qui font partie de la classe de  de XDM Individuel  le.

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

Une réponse réussie renvoie un filtré de  de, contenant uniquement ceux qui répondent aux deux exigences. N’oubliez pas que lors de l’utilisation de plusieurs paramètres de , une relation ET est supposée. Le format de la réponse dépend de l’en-tête Accepter envoyé dans la requête.

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
