---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un schéma ad hoc
topic: tutorials
translation-type: tm+mt
source-git-commit: 956d1e5b4a994c9ea52d818f3dd6d3ff88cb16b6
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 2%

---


# Création d’un schéma ad hoc

Dans des circonstances spécifiques, il peut être nécessaire de créer un schéma de modèle de données d’expérience (XDM) avec des champs dont l’espacement des noms n’est utilisé que par un seul jeu de données. On parle alors de schéma &quot;ad hoc&quot;. Les schémas ad hoc sont utilisés dans divers workflows d’assimilation de données pour la plate-forme d’expérience, y compris l’assimilation de fichiers CSV et la création de certains types de connexions source.

Ce document fournit des étapes générales pour la création d&#39;un schéma ad hoc à l&#39;aide de l&#39;API [de registre de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schéma. Il est destiné à être utilisé conjointement avec d’autres didacticiels de la plateforme d’expérience qui nécessitent la création d’un schéma ad hoc dans le cadre de leur processus. Chacun de ces documents fournit des informations détaillées sur la manière de configurer correctement un schéma ad hoc en fonction de son cas d’utilisation spécifique.

## Prise en main

Ce didacticiel nécessite une bonne compréhension du système de modèle de données d’expérience (XDM). Avant de commencer ce didacticiel, consultez la documentation XDM suivante :

- [Présentation](../home.md)du système XDM : Présentation générale de XDM et de son implémentation dans la plateforme d’expérience.
- [Principes de base de la composition](../schema/composition.md)des schémas : Présentation des composants de base des schémas XDM.

Avant de commencer ce didacticiel, veuillez consulter le guide [du](../api/getting-started.md) développeur pour obtenir des informations importantes que vous devez connaître pour pouvoir invoquer l&#39;API de registre de Schéma. Cela inclut votre `{TENANT_ID}`nom, le concept de &quot;conteneurs&quot; et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accepter et à ses valeurs possibles).

## Création d’une classe ad hoc

Le comportement des données d&#39;un schéma XDM est déterminé par sa classe sous-jacente. La première étape de la création d’un schéma ad hoc consiste à créer une classe basée sur le `adhoc` comportement. Pour ce faire, vous devez envoyer une requête POST au point de `/tenant/classes` terminaison.

**Format d’API**

```http
POST /tenant/classes
```

**Requête**

La requête suivante crée une nouvelle classe XDM, configurée par les attributs fournis dans la charge utile. En fournissant une `$ref` propriété définie sur `https://ns.adobe.com/xdm/data/adhoc` dans le `allOf` tableau, cette classe hérite du `adhoc` comportement. La requête définit également un `_adhoc` objet, qui contient les champs personnalisés de la classe.

>[!NOTE] Les champs personnalisés définis sous `_adhoc` varient selon le cas d’utilisation du schéma ad hoc. Reportez-vous au processus spécifique du didacticiel approprié pour les champs personnalisés requis en fonction du cas d&#39;utilisation.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `$ref` | Comportement des données pour la nouvelle classe. Pour les classes ad hoc, cette valeur doit être définie sur `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Objet contenant les champs personnalisés de la classe, exprimés en paires clé-valeur des noms de champ et des types de données. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle classe, en remplaçant le nom de l&#39; `properties._adhoc` objet par un GUID qui est un identifiant unique généré par le système et en lecture seule pour la classe. L’ `meta:datasetNamespace` attribut est également généré automatiquement et inclus dans la réponse.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| Propriété | Description |
| --- | --- |
| `$id` | URI qui sert d’identificateur unique généré par le système en lecture seule pour la nouvelle classe ad hoc. Cette valeur est utilisée à l’étape suivante de la création d’un schéma ad hoc. |

## Création d’un schéma ad hoc

Une fois que vous avez créé une classe ad hoc, vous pouvez créer un nouveau schéma qui implémente cette classe en envoyant une demande POST au point de `/tenant/schemas` terminaison.

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

La requête suivante crée un nouveau schéma, fournissant une référence (`$ref`) à la classe ad hoc précédemment créée dans sa charge `$id` de charge utile.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**Réponse**

Une réponse positive renvoie les détails du schéma nouvellement créé, y compris son  généré par le système et en lecture seule `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## Vue du schéma ad hoc complet

>[!NOTE] Cette étape est facultative. Si vous ne souhaitez pas examiner la structure des champs de votre schéma ad hoc, vous pouvez passer à la section [étapes](#next-steps) suivantes à la fin de ce didacticiel.

Une fois le schéma ad hoc créé, vous pouvez effectuer une demande de recherche (GET) pour vue du schéma sous sa forme étendue. Pour ce faire, vous devez utiliser l’en-tête Accepter approprié dans la demande GET, comme indiqué ci-dessous.

**Format d’API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI codé en URL `$id` ou `meta:altId` du schéma ad hoc auquel vous souhaitez accéder. |

**Requête**

La requête suivante utilise l’en-tête Accepter `application/vnd.adobe.xed-full+json; version=1`, qui renvoie la forme développée du schéma. Notez que lors de la récupération d&#39;une ressource spécifique du Registre du Schéma, l&#39;en-tête Accepter de la demande doit inclure la version majeure de la ressource en question.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie les détails du schéma, y compris tous les champs imbriqués sous `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## Étapes suivantes {#next-steps}

En suivant ce didacticiel, vous avez créé un nouveau schéma ad hoc. Si vous avez été amené à ce document dans le cadre d’un autre didacticiel, vous pouvez désormais utiliser le schéma ad hoc `$id` pour terminer le processus comme indiqué.

Pour plus d&#39;informations sur l&#39;utilisation de l&#39;API Schéma Registry, consultez le guide [du](../api/getting-started.md)développeur.