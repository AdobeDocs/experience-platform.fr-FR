---
description: Cette page illustre l’appel API utilisé pour récupérer les détails d’une demande de publication de destination via l’Adobe Experience Platform Destination SDK.
title: Récupération d’une requête de publication de destination
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 36%

---


# Récupération d’une requête de publication de destination

>[!IMPORTANT]
>
>Vous ne devez utiliser ce point de terminaison d’API que si vous envoyez une destination productisée (publique), à utiliser par d’autres clients Experience Platform. Si vous créez une destination privée pour votre propre utilisation, vous n’avez pas besoin d’envoyer officiellement la destination à l’aide de l’API de publication.

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Une fois votre destination configurée et testée, vous pouvez l’envoyer à Adobe pour révision et publication. Lecture [Envoyer pour révision d’une destination créée dans Destination SDK](../guides/submit-destination.md) pour toutes les autres étapes, vous devez effectuer dans le cadre du processus d’envoi de destination.

Utilisez le point d’entrée de lʼAPI de publication des destinations pour envoyer une demande de publication dans les cas suivants :

* En tant que partenaire du Destination SDK, vous souhaitez que votre destination personnalisée soit disponible dans toutes les organisations Experience Platform, afin que tous les clients Experience Platform puissent l’utiliser ;
* Vous faites *toutes les mises à jour* à vos configurations. Les mises à jour de configuration ne sont répercutées dans la destination qu’après l’envoi d’une nouvelle demande de publication, qui est approuvée par l’équipe Experience Platform.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations dʼAPI de publication de destinations {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Liste des requêtes de publication de destination {#retrieve-list}

Vous pouvez récupérer une liste de toutes les destinations envoyées pour la publication pour votre organisation IMS en effectuant une requête GET au point d’entrée `/authoring/destinations/publish`.

**Format d’API**

Utilisez le format d’API suivant pour récupérer toutes les requêtes de publication pour votre compte.

```http
GET /authoring/destinations/publish
```

Utilisez le format d’API suivant pour récupérer une requête de publication spécifique, définie par la variable `{DESTINATION_ID}` .

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Requête**

Les deux requêtes suivantes récupèrent toutes les requêtes de publication pour votre organisation IMS ou une requête de publication spécifique, selon que vous transmettez ou non la variable `DESTINATION_ID` dans la requête.

Sélectionnez chaque onglet ci-dessous pour afficher la charge utile correspondante.

>[!BEGINTABS]

>[!TAB Récupération de toutes les requêtes de publication]

+++Requête

La requête suivante récupère la liste des requêtes de publication que vous avez envoyées, en fonction des [!DNL IMS Org ID] et la configuration des environnements de test.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Réponse

La réponse suivante renvoie un état HTTP 200 avec une liste de toutes les destinations soumises pour publication auxquelles vous avez accès, en fonction de l’identifiant de l’organisation IMS et du nom de l’environnement de test que vous avez utilisés. L’un d’eux `configId` correspond à la demande de publication pour une destination.

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

| Paramètre | Type | Description |
|---------|----------|------|
| `destinationId` | Chaîne | Identifiant de destination de la configuration de destination que vous avez envoyée pour publication. |
| `publishDetailsList.configId` | Chaîne | Identifiant unique de la demande de publication de destination pour la destination envoyée. |
| `publishDetailsList.allowedOrgs` | Chaîne | Renvoie les organisations Experience Platform pour lesquelles la destination est disponible. <br> <ul><li> Pour `"destinationType": "PUBLIC"`, ce paramètre renvoie `"*"`, ce qui signifie que la destination est disponible pour toutes les organisations Experience Platform.</li><li> Pour `"destinationType": "DEV"`, ce paramètre renvoie l’ID d’organisation de l’organisation que vous avez utilisée pour créer et tester la destination.</li></ul> |
| `publishDetailsList.status` | Chaîne | Statut de votre demande de publication de destination. Les valeurs possibles sont les suivantes :`TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED` ou `DEPRECATED`. Destinations avec la valeur `PUBLISHED` sont en ligne et peuvent être utilisés par les clients Experience Platform. |
| `publishDetailsList.destinationType` | Chaîne | Type de destination. Les valeurs peuvent être `DEV` et `PUBLIC`. `DEV` correspond à la destination dans votre organisation Experience Platform. `PUBLIC` correspond à la destination que vous avez envoyée pour publication. Pensez à ces deux options en termes Git, où la variable `DEV` La version représente votre branche de création locale et la `PUBLIC` version représente la branche principale distante. |
| `publishDetailsList.publishedDate` | Chaîne | Date à laquelle la destination a été envoyée pour publication, en temps Unix. |

{style="table-layout:auto"}

+++

>[!TAB Récupération d’une requête de publication spécifique]

+++Requête

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Paramètre | Description |
| -------- | ----------- |
| `{DESTINATION_ID}` | Identifiant de la destination pour laquelle vous souhaitez récupérer le statut de publication. |

+++

+++Réponse

Si vous avez passé une `DESTINATION_ID` dans l’appel API, la réponse renvoie un état HTTP 200 avec des informations détaillées sur la requête de publication de destination spécifiée.

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

{style="table-layout:auto"}

+++

>[!ENDTABS]

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.