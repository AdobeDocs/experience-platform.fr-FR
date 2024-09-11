---
title: Point de terminaison de certificat public
description: Découvrez comment récupérer vos certificats publics à l’aide du point de terminaison /public-certificate de l’API du service MTLS.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: 754044621cdaf1445f809bceaa3e865261eb16f0
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 3%

---

# Point d’entrée du certificat public

Ce guide explique comment utiliser le point de terminaison de certificat public pour récupérer en toute sécurité les certificats publics pour les applications d’Adobe de votre entreprise. Il comprend un exemple d’appel API et des instructions détaillées pour aider les développeurs à s’authentifier et à vérifier les exchanges de données.

## Commencer

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et comment lire des exemples d’appels API.

## Chemins d’accès API {#paths}

Les informations suivantes constituent les chemins d’API essentiels dont vous aurez besoin pour utiliser l’API mTLS Service. Il s’agit notamment de l’URL de la passerelle de plateforme, du chemin d’accès de base de l’API et d’un exemple de chemin d’accès complet pour la récupération d’un certificat public.

- URL de la passerelle PLATFORM : `https://platform.adobe.io/`
- Chemin d’accès de base pour cette API : `/data/core/mtls`
- Exemple de chemin complet : `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Récupération de vos certificats publics {#list}

Vous pouvez récupérer les certificats publics pour l’une des applications d’Adobe de votre organisation en envoyant une requête de GET au point de terminaison `/v1/certificate/public-certificate`.

**Format d’API**

```http
GET /v1/certificate/public-certificate
```

Les paramètres de requête facultatifs suivants peuvent être utilisés lors de la récupération de vos certificats publics.

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `page` | Indique à partir de quelle page commencent les résultats de votre requête. | `page=5` |
| `limit` | Nombre maximal de certificats publics que vous souhaitez récupérer par page. | `limit=20` |

{style="table-layout:auto"}

**Requête**

Un exemple de requête pour renvoyer les certificats publics associés à votre organisation est présenté dans la section réductible ci-dessous.

+++Exemple de requête

```shell
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 et répertorie les certificats publics pour votre organisation.

+++Exemple de réponse réussie

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| Propriété | Description |
| --- | --- |
| `certCommonName` | Nom commun (CN) du certificat, qui représente généralement le nom ou l’identité du serveur ou de l’entité à laquelle le certificat est émis. |
| `publicCertificate` | Le certificat public réel au format chaîne, qui est utilisé pour authentifier et chiffrer les communications. |
| `expiryDate` | Date et heure d’expiration du certificat public, au format ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Étapes suivantes

Après avoir lu ce guide, vous comprenez désormais comment récupérer vos certificats publics à l’aide de l’API Adobe Experience Platform. Pour en savoir plus sur la gestion des données client pour garantir la conformité aux réglementations et aux politiques organisationnelles, consultez la [présentation de la gouvernance des données](../home.md).

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->
