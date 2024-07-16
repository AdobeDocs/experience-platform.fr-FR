---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;exemple de données;rpc;
solution: Experience Platform
title: Exemple de point d’entrée de l’API Data
description: Le point d’entrée /sampledata dans l’API Schema Registry vous permet de générer des exemples de données mappés à la structure de tout schéma XDM existant.
exl-id: 424d33ca-0624-4891-bf83-044ac2861579
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 18%

---

# Exemple de point d’entrée de données

Pour ingérer des données dans Adobe Experience Platform, le format et la structure des données doivent respecter un schéma de modèle de données d’expérience (XDM) existant. Selon la complexité du schéma pour un jeu de données spécifique, il peut être difficile de déterminer la forme exacte des données attendues par le jeu de données lors de l’ingestion.

À l’aide du point d’entrée `/sampledata` de l’API [!DNL Schema Registry], vous pouvez générer un exemple d’objet d’ingestion pour tout schéma créé précédemment.

## Commencer

Le point de terminaison utilisé dans ce guide fait partie de l’ [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

L’exemple de point d’entrée de données fait partie des appels de procédure distante (RPC) pris en charge par [!DNL Schema Registry]. Contrairement à d’autres points de terminaison dans l’API [!DNL Schema Registry], les points de terminaison RPC ne nécessitent pas d’en-têtes supplémentaires tels que `Accept` ou `Content-Type` et n’utilisent pas un `CONTAINER_ID`. Au lieu de cela, ils doivent utiliser l’espace de noms `/rpc`, comme illustré dans l’appel API ci-dessous.

## Récupération des exemples de données pour un schéma

Vous pouvez récupérer des exemples de données pour n’importe quel schéma dans la bibliothèque de schémas en spécifiant l’identifiant du schéma dans le chemin d’accès d’une requête de GET au point de terminaison .

**Format d’API**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` ou encodé URL `$id` du schéma pour lequel vous souhaitez générer des exemples de données. |

{style="table-layout:auto"}

**Requête**

La requête suivante génère des données d’exemple pour un schéma Loyalty Members.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
