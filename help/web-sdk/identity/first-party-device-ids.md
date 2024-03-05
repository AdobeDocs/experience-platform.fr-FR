---
title: Identifiants d’appareil propriétaires dans le SDK Web
description: Découvrez comment configurer des identifiants d’appareil propriétaires (FPID) pour le SDK Web de Adobe Experience Platform.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 0%

---

# Identifiants d’appareil propriétaires dans le SDK Web

Le SDK Web de Adobe Experience Platform affecte [Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=fr) aux visiteurs du site web à l’aide de cookies pour effectuer le suivi du comportement des utilisateurs. Pour tenir compte des restrictions du navigateur sur la durée de vie des cookies, vous pouvez choisir de définir et de gérer vos propres identifiants d’appareil à la place. On parle alors d’identifiants d’appareil propriétaires (FPID).

>[!NOTE]
>
>La prise en charge des identifiants d’appareil propriétaires n’est disponible que lors de l’envoi de données à Platform Edge Network via le SDK Web Platform.

>[!IMPORTANT]
>
>Les identifiants d’appareil propriétaires ne sont pas compatibles avec la variable [cookies tiers](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) dans le SDK Web.
>Vous pouvez utiliser des identifiants d’appareil propriétaires ou des cookies tiers, mais vous ne pouvez pas utiliser les deux fonctionnalités simultanément.

Ce document explique comment configurer des identifiants d’appareil propriétaires pour votre mise en oeuvre du SDK Web Platform.

## Conditions préalables

Ce guide suppose que vous connaissez le fonctionnement des données d’identité pour le SDK Web Platform, y compris le rôle des ECID et des `identityMap`. Consultez la présentation sur [données d’identité dans le SDK Web](./overview.md) pour plus d’informations.

## Utilisation des FPID

Les FPID effectuent le suivi des visiteurs à l’aide de cookies propriétaires. Les cookies propriétaires sont plus efficaces lorsqu’ils sont définis à l’aide d’un serveur qui utilise un DNS. [Un enregistrement](https://datatracker.ietf.org/doc/html/rfc1035) (pour IPv4) ou [Enregistrement AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (pour IPv6), par opposition à un CNAME DNS ou à un code JavaScript.

>[!IMPORTANT]
>
>`A` ou `AAAA` Les enregistrements ne sont pris en charge que pour la définition et le suivi des cookies. La méthode principale de collecte de données est un CNAME DNS. En d’autres termes, les FPID sont définis à l’aide d’un enregistrement A ou AAAA, puis sont envoyés à l’Adobe à l’aide d’un CNAME.
>
>La variable [Programme de certificat géré par Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) est également toujours pris en charge pour la collecte de données propriétaires.

Une fois qu’un cookie FPID est défini, sa valeur peut être récupérée et envoyée à l’Adobe à mesure que les données d’événement sont collectées. Les FPID collectés sont utilisés comme graines pour générer des ECID, qui restent les principaux identifiants dans les applications Adobe Experience Cloud.

Pour envoyer un FPID pour un visiteur de site web vers Platform Edge Network, vous devez inclure le FPID dans la variable `identityMap` pour ce visiteur. Reportez-vous à la section plus loin dans ce document sur [utilisation des FPID dans `identityMap`](#identityMap) pour plus d’informations.

### Exigences de mise en forme des identifiants

Le réseau Platform Edge n’accepte que les identifiants conformes au [Format UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Les ID d’appareil qui ne sont pas au format UUIDv4 seront rejetés.

La génération d’un UUID entraîne presque toujours un identifiant unique et aléatoire, la probabilité qu’une collision se produise étant négligeable. UUIDv4 ne peut pas être transféré à l’aide d’adresses IP ou d’autres informations d’identification personnelles (PII). Les UUID sont omniprésents et des bibliothèques sont disponibles pour pratiquement tous les langages de programmation pour les générer.

## Définition d’un cookie à l’aide de votre propre serveur

Lors de la définition d’un cookie à l’aide d’un serveur que vous détenez, différentes méthodes peuvent être utilisées pour empêcher que le cookie ne soit limité en raison des stratégies de navigateur :

* Génération de cookies à l’aide de langages de script côté serveur
* Définir des cookies en réponse à une requête d’API envoyée à un sous-domaine ou à un autre point de terminaison du site
* Génération de cookies à l’aide d’un CMS
* Génération de cookies à l’aide d’un réseau de diffusion de contenu

>[!IMPORTANT]
>
>Cookies définis à l’aide des `document.cookie` ne sera presque jamais protégée des stratégies de navigateur qui limitent les durées des cookies.

### Quand définir le cookie

Dans l’idéal, le cookie FPID doit être défini avant d’adresser toute requête au réseau Edge. Cependant, dans les cas où cela n’est pas possible, un ECID est toujours généré à l’aide de méthodes existantes et agit comme identifiant principal tant que le cookie existe.

En supposant que l’ECID soit finalement affecté par une stratégie de suppression du navigateur, mais que le FPID ne l’est pas, le FPID deviendra l’identifiant principal lors de la prochaine visite et sera utilisé pour amorcer l’ECID à chaque visite ultérieure.

### Définition de l’expiration du cookie

La définition de l’expiration d’un cookie doit être soigneusement étudiée lorsque vous implémentez la fonctionnalité FPID. Lorsque vous décidez de cela, vous devez tenir compte des pays ou des régions dans lesquels votre organisation opère, ainsi que des lois et politiques dans chacune de ces régions.

Dans le cadre de cette décision, vous souhaiterez peut-être adopter une stratégie de définition des cookies à l’échelle de l’entreprise ou une stratégie qui varie selon les utilisateurs dans chaque région où vous opérez.

Quel que soit le paramètre choisi pour l’expiration initiale d’un cookie, vous devez vous assurer d’inclure une logique qui prolonge l’expiration du cookie chaque fois qu’une nouvelle visite sur le site se produit.

## Impact des indicateurs de cookie

Différents indicateurs de cookie affectent le traitement des cookies dans différents navigateurs :

* [`HTTPOnly`](#http-only)
* [`Secure`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Cookies définis à l’aide de la variable `HTTPOnly` L’indicateur n’est pas accessible à l’aide de scripts côté client. Cela signifie que si vous définissez une variable `HTTPOnly` lors de la définition du FPID, vous devez utiliser un langage de script côté serveur pour lire la valeur du cookie à inclure dans la variable `identityMap`.

Si vous choisissez que Platform Edge Network lise la valeur du cookie FPID, définissez la variable `HTTPOnly` L’indicateur garantit que la valeur n’est pas accessible par les scripts côté client, mais n’aura aucun impact négatif sur la capacité de Platform Edge Network à lire le cookie.

>[!NOTE]
>
>Utilisation de la variable `HTTPOnly` L’indicateur n’a aucun impact sur les stratégies de cookies qui peuvent limiter la durée de vie du cookie. Cependant, il reste quelque chose à prendre en compte lorsque vous définissez et lisez la valeur du FPID.

### `Secure` {#secure}

Les cookies définis avec la variable `Secure` sont uniquement envoyés au serveur avec une requête chiffrée via le protocole HTTPS. L’utilisation de cet indicateur permet de s’assurer que les attaquants du milieu ne peuvent pas facilement accéder à la valeur du cookie. Si possible, il est toujours préférable de définir la variable `Secure` Indicateur.

### `SameSite` {#same-site}

La variable `SameSite` permet aux serveurs de déterminer si les cookies sont envoyés avec des requêtes intersites. L’attribut offre une certaine protection contre les attaques par falsification intersites. Il existe trois valeurs possibles : `Strict`, `Lax`, et `None`. Consultez votre équipe interne pour déterminer quel paramètre convient à votre entreprise.

Si non `SameSite` est spécifié, le paramètre par défaut de certains navigateurs est désormais `SameSite=Lax`.

## Utilisation des FPID dans `identityMap` {#identityMap}

Vous trouverez ci-dessous un exemple de définition d’un FPID dans la variable `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Comme pour les autres types d’identité, vous pouvez inclure le FPID avec d’autres identités dans `identityMap`. Voici un exemple du FPID inclus avec un identifiant CRM authentifié :

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Si le FPID est contenu dans un cookie lu par le réseau Edge lorsque la collecte de données propriétaires est activée, vous devez capturer uniquement l’identifiant CRM authentifié :

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Les éléments suivants `identityMap` entraînerait une réponse d’erreur de la part du réseau Edge, puisqu’il manque la variable `primary` pour le FPID. Au moins l’un des identifiants présents dans `identityMap` doit être marqué comme `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

Dans ce cas, la réponse d’erreur renvoyée par le réseau Edge serait similaire à ce qui suit :

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## Hiérarchie des identifiants

Lorsqu’un ECID et un FPID sont présents, l’ECID est hiérarchisé dans l’identification de l’utilisateur. Ainsi, lorsqu’un ECID existant est présent dans le magasin de cookies du navigateur, il reste l’identifiant principal et le nombre de visiteurs existants ne risque pas d’être affecté. Pour les utilisateurs existants, le FPID ne devient l’identité principale que lorsque l’ECID expire ou est supprimé en raison d’une stratégie de navigateur ou d’un processus manuel.

Les identités sont classées par priorité dans l’ordre suivant :

1. ECID inclus dans `identityMap`
1. ECID stocké dans un cookie
1. FPID inclus dans `identityMap`
1. FPID stocké dans un cookie

## Migration vers des identifiants d’appareil propriétaires

Si vous migrez vers l’utilisation de FPID à partir d’une mise en oeuvre précédente, il peut s’avérer difficile de visualiser à quoi pourrait ressembler la transition à un faible niveau.

Pour illustrer ce processus, imaginez un scénario impliquant un client qui a déjà visité votre site et quel impact une migration FPID aurait sur la manière dont ce client est identifié dans les solutions Adobe.

![Diagramme montrant comment les valeurs d’identifiant d’un client sont mises à jour entre les visites après la migration vers les FPID](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>La variable `ECID` le cookie est toujours prioritaire par rapport au `FPID`.

| Visite | Description |
| --- | --- |
| Première visite | Supposons que vous n’ayez pas encore commencé à définir le cookie FPID. L’ECID contenu dans la variable [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) est l’identifiant utilisé pour identifier le visiteur. |
| Deuxième visite | Le déploiement de la solution d’identification des appareils propriétaires a commencé. L’ECID existant est toujours présent et reste l’identifiant principal pour l’identification des visiteurs. |
| Troisième visite | Entre la deuxième et la troisième visite, suffisamment de temps s’est écoulé pour que l’ECID ait été supprimé en raison de la stratégie de navigateur. Cependant, comme le FPID a été défini à l’aide d’un enregistrement A DNS, le FPID persiste. Le FPID est désormais considéré comme l’ID principal et utilisé pour envoyer l’ECID, qui est écrit sur l’appareil de l’utilisateur final. L’utilisateur est désormais considéré comme un nouveau visiteur dans Adobe Experience Platform et les solutions Experience Cloud. |
| Quatrième visite | Entre la troisième et la quatrième visites, suffisamment de temps s’est écoulé pour que l’ECID ait été supprimé en raison de la stratégie de navigateur. Comme la visite précédente, le FPID reste dû à la manière dont il a été défini. Cette fois, le même ECID est généré comme la visite précédente. L’utilisateur est considéré dans l’ensemble des solutions Experience Platform et Experience Cloud comme le même utilisateur que la visite précédente. |
| Cinquième visite | Entre la quatrième et la cinquième visites, l’utilisateur final a effacé tous les cookies dans son navigateur. Un nouveau FPID est généré et utilisé pour amorcer la création d’un nouvel ECID. L’utilisateur est désormais considéré comme un nouveau visiteur dans Adobe Experience Platform et les solutions Experience Cloud. |

{style="table-layout:auto"}

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions fréquentes sur les identifiants d’appareils propriétaires.

### En quoi l’envoi d’un identifiant diffère-t-il de la simple génération d’un identifiant ?

Le concept d’ensemencement est unique dans la mesure où le FPID transmis à Adobe Experience Cloud est converti en ECID à l’aide d’un algorithme déterministe. Chaque fois que le même FPID est envoyé au réseau Adobe Experience Platform Edge, le même ECID est envoyé à partir du FPID.

### Quand l’identifiant d’appareil propriétaire doit-il être généré ?

Pour réduire le gonflement potentiel des visiteurs, le FPID doit être généré avant d’effectuer votre première requête à l’aide du SDK Web. Cependant, si vous ne parvenez pas à le faire, un ECID sera toujours généré pour cet utilisateur et sera utilisé comme identifiant principal. Le FPID généré ne deviendra pas l’identifiant principal tant que l’ECID n’est plus présent.

### Quelles méthodes de collecte de données prennent en charge les identifiants d’appareil propriétaires ?

Actuellement, seul le SDK Web prend en charge les FPID.

### Les FPID sont-ils stockés sur une plateforme ou une solution Experience Cloud ?

Une fois que le FPID a été utilisé pour envoyer un ECID, il est supprimé de la variable `identityMap` et remplacé par l’ECID qui a été généré. Le FPID n’est stocké dans aucune solution Adobe Experience Platform ou Experience Cloud.
