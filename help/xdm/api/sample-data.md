---
keywords: Experience Platform ; accueil ; rubriques populaires ; api ; API ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; données d’exemple ; rpc ;
solution: Experience Platform
title: Exemple de point de terminaison de l’API de données
description: Le point de terminaison /sampledata de l'API de registre de Schéma vous permet de générer des données d'exemple mappées à la structure de tout schéma XDM existant.
topic: guide du développeur
translation-type: tm+mt
source-git-commit: 0727ffa0c72bcb6a85de1a13215b691b97889b70
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 5%

---


# Exemple de point de terminaison de données

Pour importer des données dans Adobe Experience Platform, le format et la structure des données doivent respecter un schéma de modèle de données d’expérience (XDM) existant. En fonction de la complexité du schéma d&#39;un jeu de données particulier, il peut s&#39;avérer difficile de déterminer la forme exacte des données attendues par le jeu lors de l&#39;assimilation.

A l’aide du point de terminaison `/sampledata` de l’API [!DNL Schema Registry], vous pouvez générer un exemple d’objet d’assimilation pour tout schéma précédemment créé.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l&#39;[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

Le point de terminaison des données d&#39;exemple fait partie des appels de procédure distante (RPC) pris en charge par [!DNL Schema Registry]. Contrairement aux autres points de terminaison de l&#39;API [!DNL Schema Registry], les points de terminaison RPC ne nécessitent pas d&#39;en-têtes supplémentaires tels que `Accept` ou `Content-Type` et n&#39;utilisent pas de `CONTAINER_ID`. Ils doivent plutôt utiliser l&#39;espace de nommage `/rpc`, comme indiqué dans l&#39;appel d&#39;API ci-dessous.

## Récupération des données d’exemple pour un schéma

Vous pouvez récupérer des données d’exemple pour n’importe quel schéma de la bibliothèque de Schémas en spécifiant l’identifiant de schéma dans le chemin d’accès d’une requête de GET au point de terminaison.

**Format d’API**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` ou codé URL `$id` du schéma pour lequel vous souhaitez générer des données d’exemple. |

**Requête**

La requête suivante génère des données d&#39;exemple pour un schéma Membres de fidélité.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un exemple d’objet de données pour le schéma spécifié.

```json
{
    "@id": "/uri-reference",
    "_{TENANT_ID}": {
        "favoriteHotel": "string",
        "loyalty": {
            "loyaltyId": "string",
            "loyaltyLevel": "string",
            "loyaltyPoints": 4862,
            "memberSince": "2018-11-12T20:20:39+00:00"
        }
    },
    "repo:createDate": "2004-10-23T12:00:00-06:00",
    "repo:modifyDate": "2004-10-23T12:00:00-06:00",
    "xdm:createdByBatchID": "/uri-reference",
    "xdm:faxPhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:homeAddress": {
        "@id": "/uri-reference",
        "repo:createDate": "2004-10-23T12:00:00-06:00",
        "repo:modifyDate": "2004-10-23T12:00:00-06:00",
        "schema:description": "string",
        "schema:elevation": 31148.05,
        "schema:latitude": 29.25,
        "schema:longitude": -145.42,
        "xdm:city": "string",
        "xdm:country": "string",
        "xdm:countryCode": "US",
        "xdm:createdByBatchID": "/uri-reference",
        "xdm:dmaID": 1612,
        "xdm:label": "string",
        "xdm:lastVerifiedDate": "2018-01-12",
        "xdm:modifiedByBatchID": "/uri-reference",
        "xdm:msaID": 26375,
        "xdm:postOfficeBox": "string",
        "xdm:postalCode": "string",
        "xdm:primary": false,
        "xdm:region": "string",
        "xdm:repositoryCreatedBy": "string",
        "xdm:repositoryLastModifiedBy": "string",
        "xdm:state": "string",
        "xdm:stateProvince": "US-CA",
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:street1": "string",
        "xdm:street2": "string",
        "xdm:street3": "string",
        "xdm:street4": "string"
    },
    "xdm:homePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:identityMap": {
        "key": [
            {
                "xdm:authenticatedState": "ambiguous",
                "xdm:id": "string",
                "xdm:primary": false
            }
        ]
    },
    "xdm:mobilePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:modifiedByBatchID": "/uri-reference",
    "xdm:person": {
        "xdm:birthDate": "2018-01-12",
        "xdm:birthDayAndMonth": "01-23",
        "xdm:birthYear": 6427,
        "xdm:gender": "not_specified",
        "xdm:maritalStatus": "not_specified",
        "xdm:name": {
            "xdm:courtesyTitle": "string",
            "xdm:firstName": "string",
            "xdm:fullName": "string",
            "xdm:lastName": "string",
            "xdm:middleName": "string",
            "xdm:suffix": "string"
        },
        "xdm:nationality": "US",
        "xdm:taxId": "string"
    },
    "xdm:personalEmail": {
        "xdm:address": "john.smith@abc.com",
        "xdm:label": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:type": "unknown"
    },
    "xdm:repositoryCreatedBy": "string",
    "xdm:repositoryLastModifiedBy": "string"
}
```
