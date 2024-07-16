---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;ad hoc;ad hoc;ad hoc;ad hoc;ad hoc;ad hoc;tutoriel;créer;créer;schéma;schéma;schéma
solution: Experience Platform
title: Création d’un schéma ad hoc
description: Dans des cas spécifiques, il peut être nécessaire de créer un schéma de modèle de données d’expérience (XDM) avec des champs dont l’espace de noms n’est utilisé que par un seul jeu de données. On parle alors de schéma « ad hoc ». Les schémas ad hoc sont utilisés dans plusieurs workflows d’ingestion de données pour Experience Platform, notamment dans l’ingestion de fichiers CSV et dans la création de certains types de connexions sources.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 74%

---

# Création d’un schéma ad hoc

Dans des circonstances spécifiques, il peut être nécessaire de créer un schéma [!DNL Experience Data Model] (XDM) avec des champs dont l’espace de noms est utilisé uniquement par un seul jeu de données. On parle alors de schéma « ad hoc ». Les schémas ad hoc sont utilisés dans divers workflows d’ingestion de données pour [!DNL Experience Platform], y compris l’ingestion de fichiers CSV et la création de certains types de connexions source.

Ce document décrit les étapes générales de création d’un schéma ad hoc à l’aide de l’[API Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Il est destiné à être utilisé avec d’autres tutoriels [!DNL Experience Platform] qui nécessitent la création d’un schéma ad hoc dans le cadre de leur workflow. Chacun de ces documents fournit des informations détaillées sur la manière de configurer correctement un schéma ad hoc pour son cas d’utilisation spécifique.

## Prise en main

Ce tutoriel nécessite une compréhension pratique du système [!DNL Experience Data Model] (XDM). Avant de commencer ce tutoriel, consultez la documentation XDM suivante :

- [Présentation du système XDM](../home.md) : présentation de haut niveau de XDM et de sa mise en oeuvre dans [!DNL Experience Platform].
- [Principes de base de la composition des schémas](../schema/composition.md) : présentation des composants de base des schémas XDM.

Avant de commencer ce tutoriel, consultez le [guide de développement](../api/getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API [!DNL Schema Registry]. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).

## Création d’une classe ad hoc

Le comportement des données d’un schéma XDM est déterminé par sa classe sous-jacente. La première étape de la création d’un schéma ad hoc consiste à créer une classe basée sur le comportement `adhoc`. Pour ce faire, vous devez envoyer une requête POST au point d’entrée `/tenant/classes`.

**Format d’API**

```http
POST /tenant/classes
```

**Requête**

La requête suivante crée une nouvelle classe XDM configurée par les attributs fournis dans le payload. En fournissant une propriété `$ref` définie sur `https://ns.adobe.com/xdm/data/adhoc` dans le tableau `allOf`, cette classe hérite du comportement `adhoc`. La requête définit également un objet `_adhoc`, qui contient les champs personnalisés de la classe.

>[!NOTE]
>
>Les champs personnalisés définis sous `_adhoc` varient en fonction du cas d’utilisation du schéma ad hoc. Reportez-vous au workflow spécifique du tutoriel approprié pour les champs personnalisés requis en fonction du cas d’utilisation.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle classe, en remplaçant le nom de l’objet `properties._adhoc` par un GUID, qui est un identifiant unique généré par le système et en lecture seule pour la classe. L’attribut `meta:datasetNamespace` est également généré automatiquement et inclus dans la réponse.

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
    "imsOrg": "{ORG_ID}",
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
| `$id` | URI qui sert d’identifiant unique généré par le système et en lecture seule pour la nouvelle classe ad hoc. Cette valeur est utilisée à l’étape suivante de la création d’un schéma ad hoc. |

{style="table-layout:auto"}

## Création d’un schéma ad hoc

Une fois que vous avez créé une classe ad hoc, vous pouvez créer un nouveau schéma qui implémente celle-ci en envoyant une requête POST au point d’entrée `/tenant/schemas`.

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

La requête suivante crée un nouveau schéma, fournissant une référence (`$ref`) à la propriété `$id` de la classe ad hoc créée précédemment dans son payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie les détails du schéma créé, y compris sa propriété `$id` générée par le système et en lecture seule.

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
    "imsOrg": "{ORG_ID}",
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

## Affichage du schéma ad hoc complet

>[!NOTE]
>
>Cette étape est facultative. Si vous ne souhaitez pas examiner la structure des champs de votre schéma ad hoc, vous pouvez passer aux [étapes suivantes](#next-steps) de la section, à la fin de ce tutoriel.

Une fois le schéma ad hoc créé, vous pouvez effectuer une requête de recherche (GET) pour afficher la forme développée du schéma. Pour ce faire, utilisez l’en-tête Accept approprié dans la requête GET, comme illustré ci-dessous.

**Format d’API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` encodé URL ou `meta:altId` du schéma ad hoc auquel vous souhaitez accéder. |

{style="table-layout:auto"}

**Requête**

La requête suivante utilise l’en-tête Accept `application/vnd.adobe.xed-full+json; version=1`, qui renvoie la forme développée du schéma. Notez que lors de la récupération d’une ressource spécifique à partir de [!DNL Schema Registry], l’en-tête Accept de la requête doit inclure la version majeure de la ressource en question.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

En suivant ce tutoriel, vous avez créé un schéma ad hoc. Si un autre tutoriel vous a renvoyé à ce document, vous pouvez désormais utiliser la propriété `$id` de votre schéma ad hoc pour terminer le workflow comme indiqué.

Pour plus d&#39;informations sur l&#39;utilisation de l&#39;API [!DNL Schema Registry], consultez le [guide de développement](../api/getting-started.md).
