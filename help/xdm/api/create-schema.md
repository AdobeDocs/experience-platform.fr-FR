---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un schéma
topic: developer guide
translation-type: tm+mt
source-git-commit: 162316c3b908ffa87d8df4dff72e26ba237993db
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 1%

---


# Création d’un schéma

Un schéma peut être considéré comme le modèle des données que vous souhaitez intégrer dans la plateforme d’expérience. Chaque schéma est composé d&#39;une classe et de zéro ou plusieurs mixins. En d&#39;autres termes, vous n&#39;avez pas à ajouter un mixin pour définir un schéma, mais dans la plupart des cas, au moins un mixin sera utilisé.

Le processus de composition du schéma commence par affecter une classe. La classe définit les principaux aspects comportementaux des données (enregistrements ou séries temporelles), ainsi que les champs minimaux requis pour décrire les données qui seront ingérées.

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

La requête doit inclure un `allOf` attribut qui fait référence à `$id` une classe. Cet attribut définit la &quot;classe de base&quot; que le schéma mettra en oeuvre. Dans cet exemple, la classe de base est une classe &quot;Informations sur la propriété&quot; qui a été créée précédemment.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `allOf > $ref` | La `$id` valeur de la classe que le nouveau schéma implémentera. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et une charge utile contenant les détails du schéma nouvellement créé, y compris le `$id`, `meta:altId`et `version`. Ces valeurs sont en lecture seule et sont affectées par le Registre du Schéma.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

L’exécution d’une requête GET pour liste à tous les schémas du conteneur locataire inclut désormais le schéma d’informations sur les propriétés, ou vous pouvez exécuter une requête GET (lookup) à l’aide de l’ `$id` URI codé en URL pour vue directement le nouveau schéma. N’oubliez pas d’inclure le dans l’en-tête Accepter `version` pour toutes les requêtes de recherche.
