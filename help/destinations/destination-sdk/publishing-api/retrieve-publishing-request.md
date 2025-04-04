---
description: Cette page illustre comment l’appel API est utilisé pour récupérer des détails sur une requête de publication de destination avec Adobe Experience Platform Destination SDK.
title: Récupération d’une requête de publication de destination
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 98%

---

# Récupération d’une requête de publication de destination

>[!IMPORTANT]
>
>Vous ne devez utiliser ce point d’entrée de l’API que si vous soumettez une destination personnalisée (publique), qui sera utilisée par d’autres clients et clientes d’Experience Platform. Si vous créez une destination privée destinée à votre propre usage, vous n’avez pas besoin de soumettre officiellement la destination avec l’API de publication.

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Une fois la destination configurée et testée, vous pouvez l’envoyer à Adobe pour révision et publication. Consultez la documentation [Envoyer pour révision une destination créée dans Destination SDK](../guides/submit-destination.md) pour découvrir les autres étapes à suivre dans le cadre du processus de soumission d’une destination.

Utilisez le point d’entrée de lʼAPI de publication des destinations pour envoyer une demande de publication dans les cas suivants :

* En tant que partenaire du Destination SDK, vous souhaitez que votre destination personnalisée soit disponible dans toutes les organisations Experience Platform, afin que tous les clients et clientes Experience Platform puissent l’utiliser ;
* Vous *mettez à jour* vos configurations. Les mises à jour de configuration sont prises en compte dans la destination uniquement après la soumission d’une nouvelle requête de publication, qui est approuvée par l’équipe d’Experience Platform.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations dʼAPI de publication de destinations {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Liste des requêtes de publication de destination {#retrieve-list}

Vous pouvez récupérer une liste de toutes les destinations envoyées pour la publication pour votre organisation IMS en effectuant une requête GET au point d’entrée `/authoring/destinations/publish`.

**Format d’API**

Utilisez le format d’API suivant pour récupérer toutes les requêtes de publication pour votre compte.

```http
GET /authoring/destinations/publish
```

Utilisez le format d’API suivant pour récupérer une requête de publication spécifique, définie par le paramètre `{DESTINATION_ID}`.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Requête**

Les deux requêtes suivantes récupèrent toutes les requêtes de publication pour votre organisation IMS ou une requête de publication spécifique, selon que vous transmettez ou non le paramètre `DESTINATION_ID` dans la requête.

Sélectionnez chaque onglet ci-dessous pour afficher la payload correspondante.

>[!BEGINTABS]

>[!TAB Récupération de toutes les requêtes de publication]

+++Requête

La requête suivante récupère la liste des requêtes de publication auxquels vous avez accès en fonction de [!DNL IMS Org ID] et de la configuration du sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Réponse

La réponse suivante renvoie le statut HTTP 200 avec une liste de toutes les destinations envoyées pour publication auxquelles vous avez accès en fonction de l’identifiant d’organisation IMS et du nom du sandbox utilisé. L’un d’eux `configId` correspond à la demande de publication pour une destination.

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
| `publishDetailsList.allowedOrgs` | Chaîne | Renvoie les organisations Experience Platform pour lesquelles la destination est disponible. <br> <ul><li> Quand ce paramètre est défini sur `"destinationType": "PUBLIC"`, il renvoie `"*"`, ce qui signifie que la destination est disponible pour toutes les organisations Experience Platform.</li><li> Quand ce paramètre est défini sur `"destinationType": "DEV"`, il renvoie l’identifiant d’organisation de l’organisation que vous avez utilisée pour créer et tester la destination.</li></ul> |
| `publishDetailsList.status` | Chaîne | Statut de votre demande de publication de destination. Les valeurs possibles sont les suivantes : `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED` ou `DEPRECATED`. Les destinations avec la valeur `PUBLISHED` sont en ligne et peuvent être utilisées par la clientèle d’Experience Platform. |
| `publishDetailsList.destinationType` | Chaîne | Type de destination. Les valeurs peuvent être `DEV` et `PUBLIC`. `DEV` correspond à la destination dans votre organisation Experience Platform. `PUBLIC` correspond à la destination que vous avez envoyée pour publication. Pensez à ces deux options en termes Git, où la version `DEV` représente votre branche de création locale et la version `PUBLIC` représente la branche principale éloignée. |
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

Si vous avez transmis un `DESTINATION_ID` dans l’appel API, la réponse renvoie le statut HTTP 200 avec des informations détaillées sur la requête de publication de destination spécifiée.

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
| `publishDetailsList.allowedOrgs` | Chaîne | Renvoie les organisations Experience Platform pour lesquelles la destination est disponible. <br> <ul><li> Quand ce paramètre est défini sur `"destinationType": "PUBLIC"`, il renvoie `"*"`, ce qui signifie que la destination est disponible pour toutes les organisations Experience Platform.</li><li> Quand ce paramètre est défini sur `"destinationType": "DEV"`, il renvoie l’identifiant d’organisation de l’organisation que vous avez utilisée pour créer et tester la destination.</li></ul> |
| `publishDetailsList.status` | Chaîne | Statut de votre demande de publication de destination. Les valeurs possibles sont les suivantes : `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED` ou `DEPRECATED`. Les destinations avec la valeur `PUBLISHED` sont en ligne et peuvent être utilisées par la clientèle d’Experience Platform. |
| `publishDetailsList.destinationType` | Chaîne | Type de destination. Les valeurs peuvent être `DEV` et `PUBLIC`. `DEV` correspond à la destination dans votre organisation Experience Platform. `PUBLIC` correspond à la destination que vous avez envoyée pour publication. Pensez à ces deux options en termes Git, où la version `DEV` représente votre branche de création locale et la version `PUBLIC` représente la branche principale éloignée. |
| `publishDetailsList.publishedDate` | Chaîne | Date à laquelle la destination a été envoyée pour publication, en temps Unix. |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.
