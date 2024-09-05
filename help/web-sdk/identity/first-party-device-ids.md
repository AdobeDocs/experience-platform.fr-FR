---
title: Identifiants d’appareil propriétaires dans le SDK Web
description: Découvrez comment configurer des identifiants d’appareil propriétaires (FPID) dans le SDK Web de Adobe Experience Platform.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 1cb38e3eaa83f2ad0e7dffef185d5edaf5e6c38c
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---


# Identifiants d’appareil propriétaires dans le SDK Web

Le SDK Web de Adobe Experience Platform affecte des [Adobe Experience Cloud IDs (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=fr) aux visiteurs du site Web à l’aide de cookies afin d’effectuer le suivi du comportement des utilisateurs. Pour tenir compte des restrictions du navigateur sur la durée de vie des cookies, vous pouvez choisir de définir et de gérer vos propres identifiants d’appareil à la place. Ils sont appelés identifiants d’appareil propriétaires (`FPIDs`).

>[!NOTE]
>
>La prise en charge des identifiants d’appareil propriétaires n’est disponible que lors de l’envoi de données à l’Edge Network Experience Platform via le SDK Web.

>[!IMPORTANT]
>
>Les identifiants d’appareil propriétaires ne sont pas compatibles avec la fonctionnalité [ de cookies tiers](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) du SDK Web.
>Vous pouvez utiliser des identifiants d’appareil propriétaires ou des cookies tiers, mais vous ne pouvez pas utiliser les deux fonctionnalités simultanément.

Ce document explique comment configurer des identifiants d’appareil propriétaires pour votre mise en oeuvre de SDK Web.

## Conditions préalables

Ce guide suppose que vous connaissez le fonctionnement des données d’identité pour le SDK Web Platform, y compris le rôle des ECID et `identityMap`. Pour plus d’informations, consultez la présentation de [données d’identité dans le SDK Web](./overview.md) .

## Utilisation d’identifiants d’appareil propriétaires (FPID) {#using-fpid}

Les identifiants d’appareil propriétaires ([!DNL FPIDs]) effectuent le suivi des visiteurs à l’aide de cookies propriétaires. Les cookies propriétaires sont plus efficaces lorsqu’ils sont définis à l’aide d’un serveur qui utilise un [enregistrement A](https://datatracker.ietf.org/doc/html/rfc1035) DNS (pour IPv4) ou un [enregistrement AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (pour IPv6), par opposition à un code DNS [!DNL CNAME] ou [!DNL JavaScript].

>[!IMPORTANT]
>
>Les enregistrements [!DNL A] ou [!DNL AAAA] ne sont pris en charge que pour la définition et le suivi des cookies. La méthode principale de collecte de données est [!DNL DNS] [!DNL CNAME]. En d’autres termes, [!DNL FPIDs] sont définis à l’aide d’un enregistrement [!DNL A] ou [!DNL AAAA], puis sont envoyés à l’Adobe à l’aide d’un [!DNL CNAME].
>
>Le [programme de certificat géré par l’Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) est également toujours pris en charge pour la collecte de données propriétaires.

Une fois qu’un cookie [!DNL FPID] est défini, sa valeur peut être récupérée et envoyée à l’Adobe lorsque les données d’événement sont collectées. Les [!DNL FPIDs] collectés sont utilisés comme graines pour générer [!DNL ECIDs], qui restent les identifiants principaux dans les applications Adobe Experience Cloud.

Pour envoyer un [!DNL FPID] pour un visiteur de site web à l’Edge Network, vous devez inclure le [!DNL FPID] dans le `identityMap` de ce visiteur. Pour plus d’informations, reportez-vous à la section plus bas de ce document sur [ à l’aide de FPID dans `identityMap`](#identityMap).

### Exigences de mise en forme des identifiants de périphérique propriétaires {#formatting-requirements}

L’Edge Network accepte uniquement les [!DNL IDs] conformes au [format UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Les identifiants d’appareil qui ne sont pas au format [!DNL UUIDv4] seront rejetés.

La génération d’un [!DNL UUID] va presque toujours générer un identifiant unique et aléatoire, avec une probabilité de collision négligeable. [!DNL UUIDv4] ne peut pas être envoyé à l’aide d’adresses IP ou d’autres informations d’identification personnelles ([!DNL PII]). [!DNL UUIDs] sont omniprésents et des bibliothèques sont disponibles pour pratiquement tous les langages de programmation pour les générer.

## Définition d’un cookie d’identifiant propriétaire dans l’interface utilisateur des flux de données {#setting-cookie-datastreams}

Vous pouvez spécifier un nom de cookie dans l’interface utilisateur des flux de données, où [!DNL FPID] peut résider, plutôt que d’avoir à lire la valeur du cookie et à inclure le [!DNL FPID] dans la carte d’identité.

>[!IMPORTANT]
>
>Cette fonctionnalité nécessite que [Collecte de données propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en) soit activée.

Pour plus d’informations sur la configuration d’un flux de données, consultez la [documentation sur les jeux de données](../../datastreams/configure.md) .

Lors de la configuration de votre flux de données, activez l’option **[!UICONTROL Cookie d’identifiant propriétaire]** . Ce paramètre indique à l’Edge Network de se référer à un cookie spécifié lors de la recherche d’un identifiant d’appareil propriétaire, plutôt que de rechercher cette valeur dans la [carte d’identité](#identityMap).

Consultez la documentation sur les [cookies propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr) pour plus d’informations sur leur utilisation avec Adobe Experience Cloud.

![Image de l’interface utilisateur de Platform montrant la configuration de la banque de données mettant en évidence le paramètre du cookie d’ID propriétaire](../assets/first-party-id-datastreams.png)

Lorsque vous activez ce paramètre, vous devez indiquer le nom du cookie dans lequel l’ID doit être stocké.

Lorsque vous utilisez des identifiants propriétaires, vous ne pouvez pas effectuer de synchronisation d’identifiants tiers. Les synchronisations des identifiants tiers dépendent du service [!DNL Visitor ID] et du `UUID` généré par ce service. Lors de l’utilisation de la fonctionnalité d’identifiant propriétaire, [!DNL ECID] est généré sans l’utilisation du service [!DNL Visitor ID], ce qui rend impossible la synchronisation d’identifiants tiers.

Lorsque vous utilisez des identifiants propriétaires, les fonctionnalités [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager) ciblées pour l’activation dans les plateformes partenaires ne sont pas prises en charge, étant donné que les synchronisations des identifiants partenaires d’Audience Manager sont principalement basées sur `UUIDs` ou `DIDs`. Le [!DNL ECID] dérivé d’un identifiant propriétaire n’est pas lié à un `UUID`, ce qui le rend inadressable.

## Définition d’un cookie à l’aide de votre propre serveur {#set-cookie-server}

Lorsque vous définissez un cookie à l’aide d’un serveur que vous détenez, vous pouvez utiliser différentes méthodes pour empêcher que le cookie ne soit limité en raison des stratégies de navigateur :

* Génération de cookies à l’aide de langages de script côté serveur
* Définir des cookies en réponse à une requête d’API envoyée à un sous-domaine ou à un autre point de terminaison du site
* Générer des cookies à l’aide d’un [!DNL CMS]
* Générer des cookies à l’aide d’un [!DNL CDN]

>[!IMPORTANT]
>
>Les cookies définis à l’aide de la méthode `document.cookie` de JavaScript ne seront presque jamais protégés des stratégies de navigateur qui limitent les durées des cookies.

### Quand définir le cookie {#when-to-set-cookie}

Le cookie [!DNL FPID] doit idéalement être défini avant d’adresser toute requête à l’Edge Network. Cependant, dans les scénarios où cela n’est pas possible, un [!DNL ECID] est toujours généré à l’aide de méthodes existantes et agit comme identifiant principal tant que le cookie existe.

En supposant que [!DNL ECID] soit finalement affecté par une stratégie de suppression du navigateur, mais que [!DNL FPID] ne l’soit pas, [!DNL FPID] deviendra l’identifiant principal lors de la prochaine visite et sera utilisé pour amorcer le [!DNL ECID] à chaque visite ultérieure.

### Définition de l’expiration du cookie {#set-expiration}

La définition de l’expiration d’un cookie doit être soigneusement étudiée lorsque vous implémentez la fonctionnalité [!DNL FPID]. Lorsque vous décidez de cela, vous devez tenir compte des pays ou des régions dans lesquels votre organisation opère, ainsi que des lois et politiques dans chacune de ces régions.

Dans le cadre de cette décision, vous souhaiterez peut-être adopter une stratégie de définition des cookies à l’échelle de l’entreprise ou une stratégie qui varie selon les utilisateurs dans chaque région où vous opérez.

Quel que soit le paramètre choisi pour l’expiration initiale d’un cookie, vous devez vous assurer d’inclure une logique qui prolonge l’expiration du cookie chaque fois qu’une nouvelle visite sur le site se produit.

## Impact des indicateurs de cookie {#cookie-flag-impact}

Différents indicateurs de cookie affectent le traitement des cookies dans différents navigateurs :

* [`HTTPOnly`](#http-only)
* [`Secure`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Les cookies définis à l’aide de l’indicateur `HTTPOnly` ne sont pas accessibles à l’aide de scripts côté client. Cela signifie que si vous définissez un indicateur `HTTPOnly` lors de la définition de [!DNL FPID], vous devez utiliser un langage de script côté serveur pour lire la valeur du cookie à inclure dans `identityMap`.

Si vous choisissez que l’Edge Network lise la valeur du cookie [!DNL FPID], la définition de l’indicateur `HTTPOnly` garantit que la valeur n’est accessible par aucun script côté client, mais n’aura aucun impact négatif sur la capacité de l’Edge Network à lire le cookie.

>[!NOTE]
>
>L’utilisation de l’indicateur `HTTPOnly` n’a aucun impact sur les stratégies de cookies qui peuvent restreindre la durée de vie des cookies. Cependant, il reste quelque chose à prendre en compte lorsque vous définissez et lisez la valeur de [!DNL FPID].

### `Secure` {#secure}

Les cookies définis avec l’attribut `Secure` ne sont envoyés au serveur qu’avec une requête chiffrée via le protocole [!DNL HTTPS]. L’utilisation de cet indicateur permet de s’assurer que les attaquants du milieu ne peuvent pas facilement accéder à la valeur du cookie. Lorsque cela est possible, il est toujours préférable de définir l’indicateur `Secure`.

### `SameSite` {#same-site}

L’attribut `SameSite` permet aux serveurs de déterminer si des cookies sont envoyés avec des requêtes intersites. L’attribut offre une certaine protection contre les attaques par falsification intersites. Il existe trois valeurs possibles : `Strict`, `Lax` et `None`. Consultez votre équipe interne pour déterminer quel paramètre convient à votre entreprise.

Si aucun attribut `SameSite` n’est spécifié, le paramètre par défaut de certains navigateurs est désormais `SameSite=Lax`.

## Utilisation des FPID dans `identityMap` {#identityMap}

Vous trouverez ci-dessous un exemple de la manière dont vous définiriez un [!DNL FPID] dans le `identityMap` :

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

Comme pour les autres types d’identité, vous pouvez inclure [!DNL FPID] avec d’autres identités dans `identityMap`. Voici un exemple des [!DNL FPID] inclus avec un [!DNL CRM ID] authentifié :

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

Si le [!DNL FPID] est contenu dans un cookie en cours de lecture par l’Edge Network lorsque la collecte de données propriétaires est activée, vous devez capturer uniquement les [!DNL CRM ID] authentifiés :

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

Les `identityMap` suivants provoqueraient une réponse d’erreur de l’Edge Network, car l’indicateur `primary` est manquant pour l’élément [!DNL FPID]. Au moins un des identifiants présents dans `identityMap` doit être marqué comme `primary`.

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

Dans ce cas, la réponse d’erreur renvoyée par l’Edge Network est similaire à ce qui suit :

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

## Hiérarchie des identifiants {#id-hierarchy}

En présence d’un [!DNL ECID] et d’un [!DNL FPID], la priorité [!DNL ECID] est donnée à l’identification de l’utilisateur. Ainsi, lorsqu’un [!DNL ECID] existant est présent dans le magasin de cookies du navigateur, il reste l’identifiant principal et le nombre de visiteurs existants ne risque pas d’être affecté. Pour les utilisateurs existants, [!DNL FPID] ne deviendra l’identité principale que lorsque [!DNL ECID] expirera ou sera supprimé en raison d’une stratégie de navigateur ou d’un processus manuel.

Les identités sont classées par priorité dans l’ordre suivant :

1. [!DNL ECID] inclus dans le `identityMap`
1. [!DNL ECID] stocké dans un cookie
1. [!DNL FPID] inclus dans le `identityMap`
1. [!DNL FPID] stocké dans un cookie

## Migration vers des identifiants d’appareil propriétaires {#migrating-to-fpid}

Si vous effectuez une migration vers des identifiants d’appareil propriétaires à partir d’une mise en oeuvre précédente, il peut s’avérer difficile de visualiser à quoi pourrait ressembler la transition à un faible niveau.

Pour illustrer ce processus, imaginez un scénario impliquant un client qui a déjà visité votre site et quel impact une migration [!DNL FPID] aurait sur la manière dont ce client est identifié dans les solutions Adobe.

![Diagramme montrant comment les valeurs d&#39;identifiant d&#39;un client sont mises à jour entre les visites après la migration vers FPID](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>Le cookie `ECID` est toujours prioritaire par rapport à `FPID`.

| Consultez votre | Description |
| --- | --- |
| Première visite | Supposons que vous n’ayez pas encore commencé à définir le cookie [!DNL FPID]. Le [!DNL ECID] contenu dans le [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) sera l’identifiant utilisé pour identifier le visiteur. |
| Deuxième visite | Le déploiement de la solution [!DNL FPID] a commencé. Le [!DNL ECID] existant est toujours présent et reste l’identifiant principal pour l’identification des visiteurs. |
| Troisième visite | Entre la deuxième et la troisième visite, suffisamment de temps s’est écoulé pour que [!DNL ECID] ait été supprimé en raison de la stratégie du navigateur. Cependant, comme [!DNL FPID] a été défini à l’aide d’un enregistrement [!DNL DNS] [!DNL A], [!DNL FPID] persiste. [!DNL FPID] est désormais considéré comme l’ID principal et utilisé pour amorcer le [!DNL ECID], qui est écrit sur l’appareil de l’utilisateur final. L’utilisateur est désormais considéré comme un nouveau visiteur dans Adobe Experience Platform et les solutions Experience Cloud. |
| Quatrième visite | Entre la troisième et la quatrième visites, suffisamment de temps s’est écoulé pour que [!DNL ECID] ait été supprimé en raison de la stratégie du navigateur. Comme la visite précédente, le [!DNL FPID] reste dû à la manière dont il a été défini. Cette fois, le même [!DNL ECID] est généré que la visite précédente. L’utilisateur est considéré dans l’ensemble des solutions Experience Platform et Experience Cloud comme le même utilisateur que la visite précédente. |
| Cinquième visite | Entre la quatrième et la cinquième visites, l’utilisateur final a effacé tous les cookies dans son navigateur. Un nouveau [!DNL FPID] est généré et utilisé pour amorcer la création d’un nouveau [!DNL ECID]. L’utilisateur est désormais considéré comme un nouveau visiteur dans Adobe Experience Platform et les solutions Experience Cloud. |

{style="table-layout:auto"}

## FAQ {#faq}

Vous trouverez ci-dessous une liste de réponses aux questions fréquentes sur les identifiants d’appareils propriétaires.

### En quoi l’envoi d’un identifiant diffère-t-il de la simple génération d’un identifiant ?

Le concept d’ensemencement est unique dans la mesure où le [!DNL FPID] transmis à Adobe Experience Cloud est converti en [!DNL ECID] à l’aide d’un algorithme déterministe. Chaque fois que le même [!DNL FPID] est envoyé à l&#39;Edge Network, le même [!DNL ECID] est envoyé à partir du [!DNL FPID].

### Quand l’identifiant d’appareil propriétaire doit-il être généré ?

Pour réduire l’inflation potentielle des visiteurs, [!DNL FPID] doit être généré avant d’effectuer votre première requête à l’aide du SDK Web. Cependant, si vous ne parvenez pas à le faire, un [!DNL ECID] sera toujours généré pour cet utilisateur et sera utilisé comme identifiant principal. Le [!DNL FPID] généré ne deviendra pas l’identifiant principal tant que [!DNL ECID] n’est pas présent.

### Quelles méthodes de collecte de données prennent en charge les identifiants d’appareil propriétaires ?

Actuellement, seul le SDK Web prend en charge les identifiants d’appareil propriétaires.

### Les identifiants d’appareil propriétaires sont-ils stockés sur une plateforme ou une solution Experience Cloud ?

Une fois que [!DNL FPID] a été utilisé pour amorcer un [!DNL ECID], il est déposé à partir de `identityMap` et remplacé par le [!DNL ECID] généré. [!DNL FPID] n’est stocké dans aucune solution Adobe Experience Platform ou Experience Cloud.
