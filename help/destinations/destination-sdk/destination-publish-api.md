---
description: Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point d’entrée de l’API « authoring/destinations/publish ».
title: Opérations de l’API du point d’entrée de publication des destinations
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 72%

---

# Opérations de l’API du point d’entrée de publication des destinations {#publish-destination}

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Cette page répertorie et décrit toutes les opérations de l’API que vous pouvez effectuer à l’aide du point d’entrée de l’API `/authoring/destinations/publish`.

Une fois votre destination configurée et testée, vous pouvez l’envoyer à Adobe pour révision et publication. Lecture [Envoyer pour révision d’une destination créée dans Destination SDK](./submit-destination.md) pour toutes les autres étapes, vous devez effectuer dans le cadre du processus d’envoi de destination.

Utilisez le point d’entrée de lʼAPI de publication des destinations pour envoyer une demande de publication dans les cas suivants :

* En tant que partenaire du Destination SDK, vous souhaitez que votre destination personnalisée soit disponible dans toutes les organisations Experience Platform, afin que tous les clients Experience Platform puissent l’utiliser ;
* Vous souhaitez que votre destination personnalisée soit disponible dans toutes les sandbox de votre organisation Experience Platform.
* Vous faites *toutes les mises à jour* à vos configurations. Les mises à jour de configuration ne sont répercutées dans la destination qu’après l’envoi d’une nouvelle demande de publication, qui est approuvée par l’équipe Experience Platform.

## Prise en main des opérations dʼAPI de publication de destinations {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Envoyer une configuration de destination pour publication {#create}

Vous pouvez envoyer une configuration de destination pour publication en réalisant une requête POST au point d’entrée `/authoring/destinations/publish`.

**Format d’API**

```http
POST /authoring/destinations/publish
```

**Requête**

La requête suivante envoie une destination pour publication dans les organisations configurées par les paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point dʼentrée `/authoring/destinations/publish`.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `destinationId` | Chaîne | Identifiant de destination de la configuration de destination que vous envoyez pour publication. Obtenez l’identifiant de destination d’une configuration de destination à l’aide de la [référence de l’API de configuration de destination](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Chaîne | Utilisation `ALL` pour que votre destination apparaisse dans le catalogue pour tous les clients Experience Platform. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 201 avec les détails de la requête de publication de destination.

## Liste des requêtes de publication de destination {#retrieve-list}

Vous pouvez récupérer une liste de toutes les destinations envoyées pour la publication pour votre organisation IMS en effectuant une requête GET au point d’entrée `/authoring/destinations/publish`.

**Format d’API**

```http
GET /authoring/destinations/publish
```

**Requête**

La requête suivante récupère la liste des destinations soumises pour publication auxquelles vous avez accès, en fonction de la configuration de l’organisation IMS et de l’environnement de test.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse suivante renvoie un état HTTP 200 avec une liste des destinations envoyées pour publication auxquelles vous avez accès, en fonction de l’ID d’organisation IMS et du nom de la sandbox utilisés. L’un d’eux `configId` correspond à la demande de publication pour une destination.

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
| `destinationId` | Chaîne | Identifiant de destination de la configuration de destination que vous avez envoyée pour publication. |
| `publishDetailsList.configId` | Chaîne | Identifiant unique de la demande de publication de destination pour la destination envoyée. |
| `publishDetailsList.allowedOrgs` | Chaîne | Renvoie les organisations Experience Platform pour lesquelles la destination est disponible. <br> <ul><li> Pour `"destinationType": "PUBLIC"`, ce paramètre renvoie `"*"`, ce qui signifie que la destination est disponible pour toutes les organisations Experience Platform.</li><li> Pour `"destinationType": "DEV"`, ce paramètre renvoie l’ID d’organisation de l’organisation que vous avez utilisée pour créer et tester la destination.</li></ul> |
| `publishDetailsList.status` | Chaîne | Statut de votre demande de publication de destination. Les valeurs possibles sont les suivantes :`TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED` ou `DEPRECATED`. Destinations avec la valeur `PUBLISHED` sont en ligne et peuvent être utilisés par les clients Experience Platform. |
| `publishDetailsList.destinationType` | Chaîne | Type de destination. Les valeurs peuvent être `DEV` et `PUBLIC`. `DEV` correspond à la destination dans votre organisation Experience Platform. `PUBLIC` correspond à la destination que vous avez envoyée pour publication. Pensez à ces deux options en termes Git, où la variable `DEV` La version représente votre branche de création locale et la `PUBLIC` version représente la branche principale distante. |
| `publishDetailsList.publishedDate` | Chaîne | Date à laquelle la destination a été envoyée pour publication, en temps Unix. |

{style=&quot;table-layout:auto&quot;}

## Obtenez le statut d’une demande de publication de destination spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une demande de publication de destination spécifique en adressant une requête GET au point d’entrée `/authoring/destinations/publish` et en fournissant l’identifiant de la destination pour laquelle vous souhaitez récupérer le statut de publication.

**Format d’API**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{DESTINATION_ID}` | Identifiant de la destination pour laquelle vous souhaitez récupérer le statut de publication. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la requête de publication de destination spécifiée.

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

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après la lecture de ce document, vous savez désormais comment envoyer une demande de publication pour votre destination. L’équipe dʼAdobe Experience Platform examinera votre demande de publication et vous recontactera dans un délai de cinq jours ouvrables.
