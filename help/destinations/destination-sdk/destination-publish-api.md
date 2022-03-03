---
description: Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/destinations/publish`.
title: Opérations de point d’entrée de l’API de publication Destinations
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 702a5b7154724faa9f5e6847b462e0ae90475571
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 5%

---

# Opérations de l’API du point d’entrée Publier les destinations {#publish-destination}

>[!IMPORTANT]
>
>**Point de terminaison de l’API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du `/authoring/destinations/publish` Point d’entrée de l’API.

Après avoir configuré et testé votre destination, vous pouvez l’envoyer à Adobe pour révision et publication. Lecture [Envoyer pour révision d’une destination créée dans Destination SDK](./submit-destination.md) pour toutes les autres étapes, vous devez effectuer dans le cadre du processus d’envoi de destination.

Utilisez le point de terminaison de l’API des destinations de publication pour envoyer une requête de publication lorsque :

* En tant que partenaire de Destination SDK, vous souhaitez rendre votre destination productisée disponible dans toutes les organisations Experience Platform pour que tous les clients Experience Platform puissent l’utiliser ;
* Vous souhaitez rendre votre destination personnalisée disponible dans votre propre organisation Experience Platform, dans tous les environnements de test.

## Prise en main des opérations de l’API de publication de destination {#get-started}

Avant de poursuivre, veuillez consulter la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Envoyer une configuration de destination pour publication {#create}

Vous pouvez envoyer une configuration de destination pour publication en adressant une requête de POST au `/authoring/destinations/publish` point de terminaison .

**Format d’API**

```http
POST /authoring/destinations/publish
```

**Requête**

La requête suivante envoie une destination pour la publication dans les organisations configurées par les paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par la fonction `/authoring/destinations/publish` point de terminaison .

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `destinationId` | Chaîne | ID de destination de la configuration de destination que vous envoyez pour publication. Obtention de l’identifiant de destination d’une configuration de destination à l’aide de la variable [référence de l’API de configuration de destination](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Chaîne | Utilisation `ALL` pour que votre destination apparaisse dans le catalogue pour tous les clients Experience Platform. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de votre requête de publication de destination.

## Liste des requêtes de publication de destination {#retrieve-list}

Vous pouvez récupérer une liste de toutes les destinations envoyées pour publication pour votre organisation IMS en adressant une demande de GET à la fonction `/authoring/destinations/publish` point de terminaison .

**Format d’API**

```http
GET /authoring/destinations/publish
```

**Requête**

La requête suivante récupère la liste des destinations soumises pour publication auxquelles vous avez accès, en fonction de la configuration de l’organisation IMS et de l’environnement de test.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse suivante renvoie un état HTTP 200 avec une liste des destinations soumises pour publication auxquelles vous avez accès, en fonction de l’identifiant de l’organisation IMS et du nom de l’environnement de test que vous avez utilisés. One `configId` correspond à la requête de publication pour une destination.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `destinationId` | Chaîne | ID de destination de la configuration de destination que vous avez envoyée pour publication. |
| `publishDetailsList.configId` | Chaîne | Identifiant unique de la requête de publication de destination pour votre destination envoyée. |
| `publishDetailsList.allowedOrgs` | Chaîne | Renvoie les organisations Experience Platform pour lesquelles la destination est disponible. <br> <ul><li> Pour `"destinationType": "PUBLIC"`, ce paramètre renvoie `"*"`, ce qui signifie que la destination est disponible pour toutes les organisations Experience Platform.</li><li> Pour `"destinationType": "DEV"`, ce paramètre renvoie l’ID d’organisation de l’organisation que vous avez utilisée pour créer et tester la destination.</li></ul> |
| `publishDetailsList.status` | Chaîne | État de votre requête de publication de destination. Les valeurs possibles sont `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinations avec la valeur `PUBLISHED` sont en ligne et peuvent être utilisés par les clients Experience Platform. |
| `publishDetailsList.destinationType` | Chaîne | Type de destination. Les valeurs peuvent être `DEV` et `PUBLIC`. `DEV` correspond à la destination dans votre organisation Experience Platform. `PUBLIC` correspond à la destination que vous avez envoyée pour publication. Pensez à ces deux options en termes Git, où la variable `DEV` La version représente votre branche de création locale et la `PUBLIC` version représente la branche principale distante. |
| `publishDetailsList.publishedDate` | Chaîne | Date à laquelle la destination a été envoyée pour publication, dans l’heure considérée. |

{style=&quot;table-layout:auto&quot;}

## Obtention de l’état d’une requête de publication de destination spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une requête de publication de destination spécifique en adressant une requête de GET à la fonction `/authoring/destinations/publish` point de terminaison et en indiquant l’identifiant de la destination pour laquelle vous souhaitez récupérer l’état de publication.

**Format d’API**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{DESTINATION_ID}` | L’identifiant de la destination pour laquelle vous souhaitez récupérer l’état de publication. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la requête de publication de destination spécifiée.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

## Gestion des erreurs d’API

Les points de terminaison de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Voir [Codes d’état d’API](../../landing/troubleshooting.md#api-status-codes) et [erreurs d’en-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez désormais comment envoyer une requête de publication pour votre destination. L’équipe Adobe Experience Platform examinera votre demande de publication et vous recontactera pendant cinq jours ouvrables.
