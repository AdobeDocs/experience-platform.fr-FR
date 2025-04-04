---
title: Identifiants d’appareils propriétaires dans Web SDK
description: Découvrez comment configurer des identifiants d’appareil propriétaires (FPID) dans le SDK Web Adobe Experience Platform.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 0%

---


# Identifiants d’appareils propriétaires dans Web SDK

Adobe Experience Platform Web SDK attribue [des identifiants Adobe Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=fr) aux visiteurs du site Web à l’aide de cookies afin de suivre le comportement des utilisateurs. Pour tenir compte des restrictions du navigateur sur la durée de vie des cookies, vous pouvez choisir de définir et de gérer vos propres identifiants d’appareil à la place. Il s’agit d’identifiants d’appareil propriétaires (`FPIDs`).

>[!NOTE]
>
>La prise en charge des identifiants d’appareil propriétaires n’est disponible que lors de l’envoi de données à Experience Platform Edge Network via le SDK Web.

>[!IMPORTANT]
>
>Les identifiants d’appareils propriétaires ne sont pas compatibles avec la fonctionnalité [cookies tiers](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) de Web SDK.
>Vous pouvez utiliser des identifiants d’appareil propriétaires ou des cookies tiers, mais vous ne pouvez pas utiliser les deux fonctionnalités simultanément.

Ce document explique comment configurer des identifiants d’appareil propriétaires pour votre implémentation de Web SDK.

## Conditions préalables

Ce guide suppose que vous connaissez le fonctionnement des données d’identité pour Experience Platform Web SDK, y compris le rôle des ECID et des `identityMap`. Pour plus d’informations, consultez la présentation des [données d’identité dans le SDK Web](./overview.md).

## Utilisation d’identifiants d’appareil propriétaires (FPID) {#using-fpid}

Les identifiants d’appareil propriétaires ([!DNL FPIDs]) effectuent le suivi des visiteurs à l’aide de cookies propriétaires. Les cookies propriétaires sont plus efficaces lorsqu’ils sont définis à l’aide d’un serveur qui utilise un enregistrement DNS [A](https://datatracker.ietf.org/doc/html/rfc1035) (pour IPv4) ou [enregistrement AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (pour IPv6), par opposition à un [!DNL CNAME] DNS ou un code [!DNL JavaScript].

>[!IMPORTANT]
>
>Les enregistrements [!DNL A] ou [!DNL AAAA] ne sont pris en charge que pour la définition et le suivi des cookies. La principale méthode de collecte de données consiste à utiliser un [!DNL CNAME] [!DNL DNS]. En d’autres termes, les [!DNL FPIDs] sont définis à l’aide d’un enregistrement [!DNL A] ou [!DNL AAAA], puis envoyés à Adobe à l’aide d’un [!DNL CNAME].
>
>Le programme de certificat géré par Adobe [](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) est également toujours pris en charge pour la collecte de données propriétaire.

Une fois qu’un cookie [!DNL FPID] est défini, sa valeur peut être récupérée et envoyée à Adobe au fur et à mesure de la collecte des données d’événement. Les [!DNL FPIDs] collectées sont utilisées comme adresses de contrôle pour générer des [!DNL ECIDs], qui continuent à être les identifiants principaux dans les applications Adobe Experience Cloud.

Pour envoyer à Edge Network un [!DNL FPID] destiné à un visiteur ou une visiteuse du site Web, vous devez inclure le [!DNL FPID] dans le `identityMap` de ce visiteur ou de cette visiteuse. Pour plus d’informations, reportez-vous à la section plus bas dans ce document sur [l’utilisation des FPID dans `identityMap`](#identityMap).

### Exigences de formatage des identifiants d’appareils propriétaires {#formatting-requirements}

Edge Network accepte uniquement les [!DNL IDs] conformes au format [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Les identifiants d’appareil qui ne sont pas au format [!DNL UUIDv4] seront rejetés.

La génération d’un [!DNL UUID] se traduit presque toujours par un identifiant unique et aléatoire, la probabilité d’une collision étant négligeable. [!DNL UUIDv4] ne peut pas être prédéfini à l’aide d’adresses IP ou de toute autre information personnelle identifiable ([!DNL PII]). Les [!DNL UUIDs] sont omniprésents et des bibliothèques sont disponibles pour pratiquement tous les langages de programmation afin de les générer.

## Définition d’un cookie d’ID propriétaire dans l’interface utilisateur des flux de données {#setting-cookie-datastreams}

Vous pouvez spécifier un nom de cookie dans l’interface utilisateur des flux de données, où le [!DNL FPID] peut résider, plutôt que d’avoir à lire la valeur du cookie et à inclure le [!DNL FPID] dans le mappage d’identité.

>[!IMPORTANT]
>
>Cette fonctionnalité nécessite que la [collecte de données propriétaire](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en) soit activée.

Consultez la [documentation sur les flux de données](../../datastreams/configure.md) pour plus d’informations sur la configuration d’un flux de données.

Lors de la configuration de votre flux de données, activez l’option **[!UICONTROL Cookie interne d’identifiant]**. Ce paramètre indique à Edge Network de se référer à un cookie spécifié lors de la recherche d’un identifiant d’appareil interne, plutôt que de rechercher cette valeur dans le [mappage d’identités](#identityMap).

Consultez la documentation relative aux [cookies propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr) pour plus d’informations sur leur fonctionnement avec Adobe Experience Cloud.

![Image de l’interface utilisateur d’Experience Platform montrant la configuration du flux de données mettant en surbrillance le paramètre Cookie interne d’identifiant](../assets/first-party-id-datastreams.png)

Lors de l’activation de ce paramètre, vous devez indiquer le nom du cookie dans lequel l’identifiant doit être stocké.

Lorsque vous utilisez des identifiants propriétaires, vous ne pouvez pas effectuer de synchronisations des identifiants tiers. Les synchronisations des identifiants tiers reposent sur le service [!DNL Visitor ID] et les `UUID` générés par ce service. Lors de l’utilisation de la fonctionnalité d’identifiant propriétaire, l’[!DNL ECID] est générée sans l’utilisation du service [!DNL Visitor ID], ce qui rend les synchronisations d’identifiants tiers impossibles.

Lorsque vous utilisez des identifiants propriétaires, les fonctionnalités [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager) ciblées vers l’activation dans les plateformes partenaires ne sont pas prises en charge, car les synchronisations des identifiants partenaires Audience Manager sont principalement basées sur `UUIDs` ou `DIDs`. Le [!DNL ECID] dérivé d’un identifiant propriétaire n’est pas lié à un `UUID`, ce qui le rend impossible à résoudre.

## Définition d’un cookie à l’aide de votre propre serveur {#set-cookie-server}

Lors de la définition d’un cookie à l’aide d’un serveur que vous possédez, vous pouvez utiliser différentes méthodes pour empêcher que le cookie ne soit restreint en raison de politiques de navigateur :

* Génération de cookies à l’aide de langages de script côté serveur
* Définissez des cookies en réponse à une requête d’API envoyée à un sous-domaine ou à un autre point d’entrée du site
* Générer des cookies à l’aide d’un [!DNL CMS]
* Générer des cookies à l’aide d’un [!DNL CDN]

>[!IMPORTANT]
>
>Les cookies définis à l’aide de la méthode `document.cookie` de JavaScript ne seront presque jamais protégés des politiques de navigateur qui limitent la durée des cookies.

### Quand définir le cookie {#when-to-set-cookie}

Le cookie [!DNL FPID] doit idéalement être défini avant d’envoyer toute requête à Edge Network. Cependant, dans les cas où cela n’est pas possible, un [!DNL ECID] est toujours généré à l’aide des méthodes existantes et agit comme identifiant principal tant que le cookie existe.

En supposant que le [!DNL ECID] soit finalement affecté par une politique de suppression de navigateur, mais que le [!DNL FPID] ne l’est pas, le [!DNL FPID] deviendra l’identifiant principal lors de la visite suivante et sera utilisé pour amorcer le [!DNL ECID] à chaque visite suivante.

### Définition de l’expiration du cookie {#set-expiration}

La définition de l’expiration d’un cookie doit être prise en compte soigneusement lors de l’implémentation de la fonctionnalité [!DNL FPID]. Lorsque vous prenez cette décision, vous devez tenir compte des pays ou régions dans lesquels votre organisation opère, ainsi que des lois et politiques de chacune de ces régions.

Dans le cadre de cette décision, vous pouvez adopter une politique de configuration des cookies à l’échelle de l’entreprise ou une politique qui varie pour les utilisateurs dans chaque paramètre régional où vous intervenez.

Quel que soit le paramètre que vous choisissez pour l’expiration initiale d’un cookie, vous devez vous assurer d’inclure une logique qui prolonge l’expiration du cookie chaque fois qu’une nouvelle visite du site se produit.

## Impact des indicateurs de cookie {#cookie-flag-impact}

Plusieurs indicateurs de cookie affectent la manière dont les cookies sont traités sur différents navigateurs :

* [`HTTPOnly`](#http-only)
* [`Sécurisé`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Les cookies définis avec l’indicateur `HTTPOnly` ne sont pas accessibles à l’aide de scripts côté client. Cela signifie que si vous définissez un indicateur de `HTTPOnly` lors de la définition du [!DNL FPID], vous devez utiliser un langage de script côté serveur pour lire la valeur du cookie à inclure dans le `identityMap`.

Si vous choisissez qu’Edge Network lise la valeur du cookie [!DNL FPID], la définition de l’indicateur `HTTPOnly` garantit que la valeur n’est accessible par aucun script côté client, mais n’aura aucun impact négatif sur la capacité d’Edge Network à lire le cookie.

>[!NOTE]
>
>L’utilisation de l’indicateur `HTTPOnly` n’a pas d’impact sur les politiques de cookie qui peuvent limiter la durée de vie des cookies. Cependant, il s’agit toujours d’un élément à prendre en compte lorsque vous définissez et lisez la valeur de l’[!DNL FPID].

### `Secure` {#secure}

Les cookies définis avec l’attribut `Secure` ne sont envoyés au serveur qu’avec une requête chiffrée via le protocole [!DNL HTTPS]. L’utilisation de cet indicateur peut permettre de s’assurer que les personnes malveillantes ne peuvent pas accéder facilement à la valeur du cookie . Dans la mesure du possible, il est toujours préférable de définir l’indicateur de `Secure`.

### `SameSite` {#same-site}

L’attribut `SameSite` permet aux serveurs de déterminer si les cookies sont envoyés avec des requêtes intersites. L’attribut fournit une certaine protection contre les attaques multisites par falsification. Trois valeurs sont possibles : `Strict`, `Lax` et `None`. Consultez votre équipe interne pour déterminer le paramètre adapté à votre organisation.

Si aucun attribut `SameSite` n’est spécifié, le paramètre par défaut de certains navigateurs est désormais `SameSite=Lax`.

## Utilisation de FPID dans `identityMap` {#identityMap}

Vous trouverez ci-dessous un exemple de la manière de définir un [!DNL FPID] dans le `identityMap` :

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

Comme pour les autres types d’identité, vous pouvez inclure le [!DNL FPID] avec d’autres identités dans `identityMap`. Voici un exemple des [!DNL FPID] inclus avec un [!DNL CRM ID] authentifié :

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
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

Si le [!DNL FPID] est contenu dans un cookie lu par Edge Network lorsque la collecte de données propriétaire est activée, vous ne devez capturer que les [!DNL CRM ID] authentifiés :

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

L’`identityMap` suivante entraînerait une réponse d’erreur de la part d’Edge Network, car il lui manque l’indicateur `primary` pour le [!DNL FPID]. Au moins un des identifiants présents dans `identityMap` doit être marqué comme `primary`.

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

Dans ce cas, la réponse d’erreur renvoyée par Edge Network est similaire à ce qui suit :

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

## Définir un FPID sur votre propre domaine {#setting-fpid-domain}

Outre la définition du [!DNL FPID] dans le mappage d’identités, vous pouvez définir le cookie [!DNL FPID] sur votre propre domaine, si vous avez configuré un [!DNL CNAME] de collecte de données propriétaire.

Lorsque la collecte de données propriétaire est activée à l’aide d’un [!DNL CNAME], tous les cookies de votre domaine sont envoyés sur les requêtes effectuées au point d’entrée de la collecte de données.

Tous les cookies non pertinents pour la collecte de données d’Adobe sont ignorés. Par [!DNL FPID], vous pouvez spécifier le nom du cookie [!DNL FPID] dans la configuration du flux de données. Dans ce cas, Edge Network lit le contenu du cookie [!DNL FPID] au lieu de rechercher le [!DNL FPID] dans le mappage d’identité.

Pour utiliser cette fonctionnalité, vous devez définir le [!DNL FPID] au niveau supérieur de votre domaine au lieu d’un sous-domaine spécifique. Si vous le définissez sur un sous-domaine, la valeur du cookie ne sera pas envoyée à Edge Network et la solution [!DNL FPID] ne fonctionnera pas comme prévu.

## Hiérarchie des identifiants {#id-hierarchy}

En présence d’un [!DNL ECID] et d’un [!DNL FPID], le [!DNL ECID] a la priorité dans l’identification de l’utilisateur. Cela permet de s’assurer que lorsqu’un [!DNL ECID] existant est présent dans la boutique de cookies de navigateur, il reste l’identifiant principal et que le nombre de visiteurs existant ne risque pas d’être affecté. Pour les utilisateurs existants, le [!DNL FPID] ne deviendra pas l’identité principale tant que le [!DNL ECID] n’aura pas expiré ou n’aura pas été supprimé en raison d’une politique de navigateur ou d’un processus manuel.

Les identités sont hiérarchisées dans l’ordre suivant :

1. [!DNL ECID] inclus dans le `identityMap`
1. [!DNL ECID] stocké dans un cookie
1. [!DNL FPID] inclus dans le `identityMap`
1. [!DNL FPID] stocké dans un cookie

## Migration vers des identifiants d’appareil propriétaires {#migrating-to-fpid}

Si vous migrez vers des identifiants d’appareil propriétaires à partir d’une mise en œuvre précédente, il peut être difficile de visualiser à quoi pourrait ressembler la transition à un niveau inférieur.

Pour illustrer ce processus, prenons l’exemple d’un client qui a déjà visité votre site et de l’impact d’une migration [!DNL FPID] sur la manière dont ce client est identifié dans les solutions Adobe.

![Diagramme montrant comment les valeurs d’identifiant d’un client sont mises à jour entre les visites après la migration vers les FPID](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>Le cookie `ECID` est toujours prioritaire sur le `FPID`.

| Consultez votre | Description |
| --- | --- |
| Première visite | Supposons que vous n’ayez pas encore commencé à définir le cookie [!DNL FPID]. Le [!DNL ECID] contenu dans le cookie [AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) est l’identifiant utilisé pour identifier le visiteur. |
| Deuxième visite | Le déploiement de la solution [!DNL FPID] a commencé. Le [!DNL ECID] existant est toujours présent et reste l’identifiant principal pour l’identification des visiteurs. |
| Troisième visite | Entre la deuxième et la troisième visite, un délai suffisant s’est écoulé avant que le [!DNL ECID] ne soit supprimé en raison d’une politique de navigateur. Cependant, comme le [!DNL FPID] a été défini à l’aide d’un enregistrement [!DNL A] [!DNL DNS], le [!DNL FPID] persiste. Le [!DNL FPID] est désormais considéré comme l’ID principal et utilisé pour amorcer le [!DNL ECID], qui est écrit sur l’appareil de l’utilisateur final. L’utilisateur serait désormais considéré comme un nouveau visiteur dans les solutions Adobe Experience Platform et Experience Cloud. |
| Quatrième visite | Entre la troisième et la quatrième visite, il s’est écoulé suffisamment de temps pour que le [!DNL ECID] ait été supprimé en raison d’une politique de navigateur. Comme lors de la précédente visite, la [!DNL FPID] reste due à la manière dont elle a été conçue. Cette fois, la même [!DNL ECID] est générée que la visite précédente. L’utilisateur est vu dans toutes les solutions Experience Platform et Experience Cloud comme le même utilisateur que la visite précédente. |
| Cinquième visite | Entre la quatrième et la cinquième visite, l’utilisateur final a effacé tous les cookies dans son navigateur. Une nouvelle [!DNL FPID] est générée et utilisée pour amorcer la création d’une nouvelle [!DNL ECID]. L’utilisateur serait désormais considéré comme un nouveau visiteur dans les solutions Adobe Experience Platform et Experience Cloud. |

{style="table-layout:auto"}

## FAQ {#faq}

Vous trouverez ci-dessous une liste de réponses aux questions les plus fréquemment posées à propos des identifiants d’appareil propriétaires.

### En quoi l’amorçage d’un ID diffère-t-il de la simple génération d’un ID ?

Le concept d’amorçage est unique dans la mesure où le [!DNL FPID] transmis à Adobe Experience Cloud est converti en [!DNL ECID] à l’aide d’un algorithme déterministe. Chaque fois que le même [!DNL FPID] est envoyé à Edge Network, le même [!DNL ECID] est ensemencé à partir du [!DNL FPID].

### Quand l’identifiant d’appareil interne doit-il être généré ?

Pour réduire le gonflement potentiel des visiteurs et visiteuses, le [!DNL FPID] doit être généré avant d’effectuer votre première requête à l’aide du SDK Web. Cependant, si vous ne pouvez pas le faire, une [!DNL ECID] sera toujours générée pour cet utilisateur et sera utilisée comme identifiant principal. Le [!DNL FPID] qui a été généré ne deviendra pas l’identifiant principal tant que le [!DNL ECID] n’est pas présent.

### Quelles méthodes de collecte de données prennent en charge les identifiants d’appareils propriétaires ?

Actuellement, seul Web SDK prend en charge les identifiants d’appareil propriétaires.

### Les identifiants d’appareil propriétaires sont-ils stockés dans des solutions Experience Platform ou Experience Cloud ?

Une fois que le [!DNL FPID] a été utilisé pour amorcer un [!DNL ECID], il est supprimé du `identityMap` et remplacé par le [!DNL ECID] qui a été généré. Le [!DNL FPID] n’est stocké dans aucune solution Adobe Experience Platform ou Experience Cloud.
