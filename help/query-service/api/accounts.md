---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;guide api;service de requête;comptes de service de requête;comptes ;
solution: Experience Platform
title: Point de terminaison de l’API Comptes
description: Vous pouvez créer un compte Query Service pour le compte persistant .
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 5%

---

# Point de terminaison des comptes

Dans Adobe Experience Platform Query Service, les comptes sont utilisés pour créer des informations d’identification non expirantes que vous pouvez utiliser avec des clients SQL externes. Vous pouvez utiliser le point d’entrée `/accounts` dans l’API Query Service, ce qui vous permet de créer, récupérer, modifier et supprimer par programmation vos comptes d’intégration Query Service (également appelés compte technique).

## Commencer

Les points de terminaison utilisés dans ce guide font partie de l’API Query Service. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et comment lire des exemples d’appels API.

## Créer un compte

Vous pouvez créer un compte d’intégration de Query Service en envoyant une requête de POST au point de terminaison `/accounts`.

**Format d’API**

```http
POST /accounts
```

**Requête**

La requête suivante crée un compte d’intégration Query Service pour votre organisation.

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| Propriété | Description |
| -------- | ----------- |
| `accountName` | **Obligatoire** Nom du compte d’intégration de Query Service. |
| `assignedToUser` | **Obligatoire** Adobe ID pour lequel le compte d’intégration de Query Service sera créé. |
| `credential` | *(Facultatif)* Informations d’identification utilisées pour l’intégration de Query Service. Si elle n’est pas spécifiée, le système génère automatiquement des informations d’identification. |
| `description` | *(Facultatif)* Description du compte d’intégration de Query Service. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200, avec les détails du compte d’intégration Query Service que vous venez de créer. Vous pouvez utiliser ces détails de compte pour connecter Query Service à des clients externes.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Propriété | Description |
| -------- | ----------- |
| `technicalAccountName` | Nom du compte d’intégration de Query Service. |
| `technicalAccountId` | L’identifiant de votre compte d’intégration Query Service. Avec `credential`, ce composant compose votre mot de passe pour votre compte. |
| `credential` | Informations d’identification de votre compte d’intégration Query Service. Avec `technicalAccountId`, ce composant compose votre mot de passe pour votre compte. |

## Mettre à jour un compte

Vous pouvez mettre à jour votre compte d’intégration Query Service en effectuant une requête de PUT sur le point de terminaison `/accounts`.

**Format d’API**

```http
POST /accounts/{ACCOUNT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{ACCOUNT_ID}` | L’identifiant du compte d’intégration de Query Service que vous souhaitez mettre à jour. |

**Requête**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `accountName` | *(Facultatif)* Nom mis à jour du compte d’intégration de Query Service. |
| `assignedToUser` | *(Facultatif)* Adobe ID mise à jour à laquelle le compte d’intégration de Query Service est lié. |
| `credential` | *(Facultatif)* Informations d’identification mises à jour pour votre compte Query Service. |
| `description` | *(Facultatif)* Description mise à jour du compte d’intégration de Query Service. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur votre compte d’intégration Query Service récemment mis à jour.

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## Liste de tous les comptes

Vous pouvez récupérer une liste de tous les comptes d’intégration de Query Service en envoyant une requête de GET au point de terminaison `/accounts`.

**Format d’API**

```http
GET /accounts
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de tous les comptes d’intégration de Query Service.

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## Suppression d’un compte

Vous pouvez supprimer votre compte d’intégration Query Service en effectuant une requête de DELETE sur le point de terminaison `/accounts`.

**Format d’API**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{ACCOUNT_ID}` | L’identifiant du compte d’intégration de Query Service que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec un message indiquant que le compte a bien été supprimé.

```json
{
    "result": "Success"
}
```
