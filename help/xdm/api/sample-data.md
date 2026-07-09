---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;données d’exemple;données d’exemple;rpc;
solution: Experience Platform
title: Point d’entrée de l’API Sample Data
description: Le point d’entrée /sampledata de l’API Schema Registry vous permet de générer des données d’exemple mappées à la structure de tout schéma XDM existant.
exl-id: 424d33ca-0624-4891-bf83-044ac2861579
TQID: https://experienceleague.adobe.com/WOd6r69PzAffQt1SAVqIZJCLpyZEzkMW8R7pwXeKUxI
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 9eb5b266c15495d852a671829d46fd127ad33ac9
workflow-type: tm+mt
source-wordcount: 319
ht-degree: 17%

---

# Point d’entrée des données d’exemple

Pour ingérer des données dans Adobe Experience Platform, leur format et structure doivent être conformes à un schéma de modèle de données d’expérience (XDM) existant. En fonction de la complexité du schéma pour un jeu de données spécifique, il peut être difficile de déterminer la forme exacte des données attendues par le jeu de données lors de l’ingestion.

À l’aide du point d’entrée `/sampledata` dans l’API [!DNL Schema Registry], vous pouvez générer un exemple d’objet d’ingestion pour tout schéma créé précédemment.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de l’API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry). [[!DNL Schema Registry] Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

Le point d’entrée des données d’exemple fait partie des appels de procédure distante (RPC) pris en charge par le [!DNL Schema Registry]. Contrairement aux autres points d&#39;entrée de l&#39;API [!DNL Schema Registry], les points d&#39;entrée RPC ne nécessitent pas d&#39;en-têtes supplémentaires tels que `Accept` ou `Content-Type`, et n&#39;utilisent pas de `CONTAINER_ID`. Ils doivent plutôt utiliser l’espace de noms `/rpc`, comme illustré dans l’appel API ci-dessous.

## Récupération de données d’exemple pour un schéma

Vous pouvez récupérer des données d’exemple pour n’importe quel schéma de la bibliothèque des schémas en spécifiant l’identifiant du schéma dans le chemin d’une requête GET vers le point d’entrée .

**Format d’API**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | `$id` codée en `meta:altId` ou en URL du schéma pour lequel vous souhaitez générer des données d’exemple. |

{style="table-layout:auto"}

**Requête**

La requête suivante génère des données d’exemple pour un schéma Membres du programme de fidélité .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un objet de données d’exemple pour le schéma spécifié.

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
