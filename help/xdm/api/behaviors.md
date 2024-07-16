---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;comportement;comportement;comportements;comportements;comportements;comportements;comportements;comportements;
solution: Experience Platform
title: Point de terminaison de l’API de comportement
description: Le point de terminaison /comportements de l’API Schema Registry vous permet de récupérer tous les comportements disponibles dans le conteneur global.
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 23%

---

# Point d’entrée des comportements

Dans le modèle de données d’expérience (XDM), les comportements définissent la nature des données décrites par un schéma. Chaque classe XDM doit faire référence à un comportement spécifique, dont tous les schémas qui utilisent cette classe hériteront. Pour la plupart des cas d’utilisation de Platform, il existe deux comportements disponibles :

* **[!UICONTROL Enregistrement]** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **[!UICONTROL Série temporelle]** : fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un objet d’enregistrement.

>[!NOTE]
>
>Dans Platform, certains cas d’utilisation nécessitent l’utilisation d’un schéma qui n’emploie aucun des comportements ci-dessus. Pour ces cas, un troisième comportement &quot;ad hoc&quot; est disponible. Pour plus d’informations, consultez le tutoriel sur la [création d’un schéma ad hoc](../tutorials/ad-hoc.md) .
>
>Pour des informations plus générales sur les comportements de données en termes d’impact sur la composition des schémas, consultez le guide sur les [ principes de base de la composition des schémas](../schema/composition.md).

Le point d’entrée `/behaviors` de l’API [!DNL Schema Registry] vous permet d’afficher les comportements disponibles dans le conteneur `global`.

## Commencer

Le point de terminaison utilisé dans ce guide fait partie de l’ [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de comportements {#list}

Vous pouvez récupérer une liste de tous les comportements disponibles en envoyant une requête de GET au point de terminaison `/behaviors`.

**Format d’API**

```http
GET /global/behaviors
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Réponse**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## Rechercher un comportement {#lookup}

Vous pouvez rechercher un comportement spécifique en fournissant son identifiant dans le chemin d’accès d’une requête de GET au point de terminaison `/behaviors`.

**Format d’API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{BEHAVIOR_ID}` | `meta:altId` ou encodé URL `$id` du comportement que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère les détails du comportement de l’enregistrement en fournissant son `meta:altId` dans le chemin de la requête.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Réponse**

Une réponse réussie renvoie les détails du comportement, y compris sa version, sa description et les attributs que le comportement fournit aux classes qui l’utilisent.

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## Étapes suivantes

Ce guide décrit l’utilisation du point d’entrée `/behaviors` dans l’API [!DNL Schema Registry]. Pour savoir comment attribuer un comportement à une classe à l’aide de l’API, consultez le [guide de point de terminaison de classes](./classes.md).
