---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;behavior;behaviour;behaviors;behaviours;
solution: Experience Platform
title: Guide du point de terminaison des comportements
description: Le point de terminaison /comportements de l'API de registre de Schéma vous permet de récupérer tous les comportements disponibles dans le conteneur global.
topic: developer guide
translation-type: tm+mt
source-git-commit: 72c9147cefd00c9fe734ac64f8062c899b0588bc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 5%

---


# Point de terminaison des comportements

Dans le modèle de données d’expérience (XDM), les comportements définissent la nature des données qu’un schéma décrit. Chaque classe XDM doit faire référence à un comportement spécifique, dont tous les schémas qui utilisent cette classe hériteront. Pour presque tous les cas d’utilisation de la plate-forme, il existe deux comportements disponibles :

* **[!UICONTROL Enregistrer]**: Fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **[!UICONTROL Série]** chronologique : Fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet d&#39;enregistrement.

>[!NOTE]
>
>Il y a des cas d&#39;utilisation dans Plateforme qui nécessitent l&#39;utilisation de schéma qui n&#39;utilisent aucun des comportements ci-dessus. Pour ces cas, un troisième comportement &quot;ad hoc&quot; est disponible. Pour plus d’informations, consultez le didacticiel sur la [création d’un schéma](../tutorials/ad-hoc.md) ad hoc.
>
>Pour obtenir des informations plus générales sur les comportements des données en ce qui concerne leur incidence sur la composition des schémas, consultez le guide sur les [bases de la composition](../schema/composition.md)des schémas.

Le `/behaviors` point de terminaison de l’ [!DNL Schema Registry] API vous permet de vue des comportements disponibles dans le `global` conteneur.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’ [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Avant de continuer, consultez le guide [de](./getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Retrieve a list of behaviors {#list}

You can retrieve a list of all available behaviors by making a GET request to the `/behaviors` endpoint.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Vous pouvez rechercher un comportement spécifique en indiquant son identifiant dans le chemin d’une demande de GET vers le point de `/behaviors` terminaison.

**Format d’API**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{BEHAVIOR_ID}` | Code `meta:altId` ou URL `$id` du comportement à rechercher. |

**Requête**

La requête suivante récupère les détails du comportement de l&#39;enregistrement en les indiquant `meta:altId` dans le chemin de la requête.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Réponse**

Une réponse positive renvoie les détails du comportement, y compris sa version, sa description et les attributs que le comportement fournit aux classes qui l’utilisent.

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

Ce guide décrit l’utilisation du point de `/behaviors` terminaison dans l’ [!DNL Schema Registry] API. Pour savoir comment attribuer un comportement à une classe à l&#39;aide de l&#39;API, consultez le guide [des points de terminaison](./classes.md)de classes.