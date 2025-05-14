---
title: Point d’entrée de certificat public
description: Découvrez comment récupérer vos certificats publics à l’aide du point d’entrée /public-certificate de l’API du service MTLS.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---

# Point d’entrée de certificat public

>[!NOTE]
>
>Adobe ne prend plus en charge le téléchargement statique des certificats mTLS publics. Utilisez cette API pour récupérer des certificats valides pour vos intégrations. La récupération automatisée est désormais nécessaire pour éviter les interruptions de service.

Ce guide explique comment utiliser le point d’entrée de certificat public pour récupérer en toute sécurité des certificats publics pour les applications Adobe de votre organisation. Elle comprend un exemple d’appel API et des instructions détaillées pour aider les développeurs à authentifier et vérifier les échanges de données.

## Commencer

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des détails importants sur les en-têtes requis et sur la manière d’interpréter les exemples d’appels API.

## Chemins d’accès aux API {#paths}

Les informations suivantes sont les chemins d’accès API essentiels dont vous aurez besoin pour utiliser l’API du service mTLS. Il s’agit notamment de l’URL de la passerelle de plateforme, du chemin de base de l’API et d’un exemple de chemin complet pour récupérer un certificat public.

- URL de la passerelle PLATFORM : `https://platform.adobe.io/`
- Chemin de base de cette API : `/data/core/mtls`
- Exemple de chemin complet : `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Récupération des certificats publics {#list}

Envoyez une requête GET au point d’entrée `/v1/certificate/public-certificate` pour récupérer les certificats publics de l’une des applications Adobe de votre organisation.

**Format d’API**

```http
GET /v1/certificate/public-certificate
```

Les paramètres de requête facultatifs suivants peuvent être utilisés lors de la récupération de vos certificats publics.

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `page` | Indique la page à partir de laquelle les résultats de votre requête démarreront. | `page=5` |
| `limit` | Nombre maximal de certificats publics à récupérer par page. | `limit=20` |

{style="table-layout:auto"}

**Requête**

Un exemple de requête pour renvoyer les certificats publics associés à votre organisation est visible dans la section réductible ci-dessous.

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

Une réponse réussie renvoie un état HTTP 200 et répertorie les certificats publics de votre organisation.

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
| `certCommonName` | Nom commun (NC) du certificat, qui représente généralement le nom ou l’identité du serveur ou de l’entité auquel le certificat est délivré. |
| `publicCertificate` | Certificat public réel au format de chaîne, utilisé pour authentifier et chiffrer les communications. |
| `expiryDate` | Date et heure d’expiration du certificat public, au format ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Automatisation du cycle de vie des certificats {#certificate-lifecycle-automation}

Adobe automatise le cycle de vie des certificats mTLS publics pour assurer la continuité et réduire les interruptions de service.

- Les certificats sont émis à nouveau 60 jours avant l’expiration.
- Les certificats sont révoqués 30 jours avant l’expiration.

>[!NOTE]
>
>Ces délais seront raccourcis au fil du temps conformément aux directives du forum [CA/B](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), qui visent à réduire la durée de vie des certificats à un maximum de 47 jours.

Vous devez mettre à jour vos intégrations pour prendre en charge la récupération automatisée via l’API. Ne vous fiez pas aux téléchargements manuels de certificats ou aux copies statiques, car ils peuvent entraîner l’expiration ou la révocation de certificats.

## Étapes suivantes

Après avoir récupéré vos certificats publics à l’aide de l’API, mettez à jour vos intégrations pour appeler régulièrement ce point d’entrée avant l’expiration des certificats. Pour tester cet appel de manière interactive, consultez la page de référence de l’API [MTLS](https://developer.adobe.com/experience-platform-apis/references/mtls-service/). Pour obtenir des instructions plus générales sur les intégrations basées sur des certificats, reportez-vous à la [ Présentation du chiffrement des données dans Adobe Experience Platform ](../../landing/governance-privacy-security/encryption.md) ou à la [Présentation de la gouvernance des données](../home.md).
