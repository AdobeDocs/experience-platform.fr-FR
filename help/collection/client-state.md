---
title: Gestion de l’état client
description: Découvrez comment Adobe Experience Platform Edge Network gère l’état du client.
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: client;état;gestion;edge;network;passerelle;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 98%

---

# Gestion de l’état client

Edge Network lui-même est sans état (il ne conserve pas sa propre session). Cependant, certains cas d’utilisation nécessitent une conservation de l’état côté client tels que :

* Identification cohérente des appareils (voir [identification des visiteurs](visitor-identification.md)).
* Collecte et application du consentement de l’utilisateur
* Conservation de l’identifiant de la session de personnalisation

Edge Network utilise un protocole de gestion des états, tout en déléguant l’aspect lié au stockage à son client/SDK, et inclut des entrées d’état dans ses réponses. Les entrées des navigateurs sont stockées sous forme de cookies.

La responsabilité du client est de les stocker et de les inclure dans toutes les demandes ultérieures. Le client doit également veiller à l’expiration correcte des entrées, conformément aux instructions de la passerelle. Lorsque les entrées ont été stockées sous forme de cookies, le navigateur effectue automatiquement toutes ces opérations.

Bien que les entrées d’état aient toujours une valeur simple `String` (visible pour l’appelant/le SDK), vous ne devez pas utiliser ni modifier les valeurs de quelque manière que ce soit. La structure/le format de la valeur ou même le nom lui-même peuvent changer à tout moment, ce qui peut entraîner un comportement inattendu pour les clients qui utilisent l’état en interne. L’état est conçu pour être toujours utilisé par la passerelle elle-même ou par d’autres services Edge.

## Conservation de l’état client sous forme de métadonnées

L’état renvoyé par [!DNL Edge Network] dans le corps de la réponse est un objet `Handle` avec le type `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| Attribut | Type | Description |
| --- | --- | --- |
| `key` | Chaîne | **Obligatoire**. Nom de l’entrée. |
| `value` | Chaîne | *Facultatif*. La valeur d’entrée. |
| `maxAge` | Nombre entier | *Facultatif* Délai (en secondes) jusqu’à l’expiration de l’entrée. En cas d’absence, les entrées ne doivent être stockées que pour la session en cours. |
| `attrs` | `Map<String, String>` | *Facultatif*. Liste facultative des attributs d’entrée. Pour toutes les connexions sécurisées avec un en-tête HTTP de référent sécurisé, l’attribut `SameSite` est défini sur `None`. |


Pour prendre en charge le balisage multiple (c’est-à-dire plusieurs instances SDK dans la même propriété, qui peuvent potentiellement renvoyer à différentes organisations), toutes les entrées d’état sont automatiquement précédées du préfixe `kndctr_` et de l’identifiant d’organisation sécurisé par une URL.

Lorsque le SDK du client reçoit un objet Handle `state:store` dans la réponse, il doit effectuer les opérations suivantes :

* Stockez les entrées côté client tout en respectant le délai d’expiration fourni par la passerelle.
* Chargez-les à partir du magasin client et incluez toutes les entrées non expirées dans les demandes ultérieures.

Voici un exemple de requête qui transmet l’état stocké côté client :

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## Conservez l’état du client dans les cookies du navigateur.

Lorsque vous travaillez avec les clients du navigateur, Edge Network peut automatiquement conserver les entrées sous forme de cookies du navigateur. Cela permet une prise en charge transparente du stockage des états, puisque les navigateurs respectent le protocole de gestion des états par défaut.

Presque toutes les entrées sont matérialisées sous forme de cookies internes lorsqu’elles sont activées et prises en charge (voir la remarque ci-dessous), mais la passerelle peut également stocker certains cookies tiers lorsque le domaine `adobedc.demdex.net` des cookies tiers est utilisé.

Comme les entrées sont toujours liées à une portée spécifique (appareil/application) par leur définition, seul le sous-ensemble compatible avec le contexte de requête actuel sera écrit par Edge Network. Les entrées non écrites sont
renvoyées dans un objet Handle `state:store`.

En règle générale, les entrées étendues au niveau de l’application sont toujours écrites sous forme de cookies internes, tandis que celles étendues au niveau de l’appareil sont écrites sous forme de cookies tiers. La décision est totalement transparente pour l’appelant. La passerelle décide quelles entrées peuvent être écrites, selon le contexte de l’appel.

L’appelant doit explicitement activer la prise en charge du stockage de l’état du client sous forme de cookies, à l’aide de l’indicateur `meta.state.cookiesEnabled` :

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| Attribut | Type | Description |
| --- | --- | --- |
| `cookiesEnabled` | Booléen | Lorsque ce paramètre est défini, la prise en charge des cookies est activée. La valeur par défaut est `false`. |
| `domain` | Chaîne | Obligatoire lorsque `cookiesEnabled: true`. Domaine de niveau supérieur sur lequel les cookies doivent être écrits. Edge Network utilise cette valeur pour décider si l’état peut être conservé sous forme de cookies. |

Bien que la prise en charge des cookies soit activée à l’aide de l’indicateur `cookiesEnabled`, Adobe Experience Platform Edge Network écrira uniquement les entrées d’état si le domaine de niveau supérieur de la requête correspond au `domain` spécifié par l’appelant. En cas de non-correspondance, les entrées sont renvoyées dans un objet Handle `state:store`.

Les cookies internes ne peuvent pas être écrits (même si la prise en charge est activée) dans les cas suivants :

* La requête est exécutée sur le domaine `adobedc.demdex.net` tiers.
* La requête est exécutée sur un domaine `CNAME` propriétaire différent de celui spécifié par l’appelant dans `meta.state.domain`.

## Sécurité des cookies

Tous les cookies comportent [l’indicateur sécurisé](https://developer.mozilla.org/fr-FR/docs/Web/HTTP/Cookies#restrict_access_to_cookies) activé dans la mesure du possible.

Tous les cookies sécurisés comportent [l’attribut SameSite](https://developer.mozilla.org/fr-FR/docs/Web/HTTP/Headers/Set-Cookie/SameSite) défini sur `None`, ce qui signifie que les cookies sont envoyés dans tous les contextes, aussi bien internes que cross-origin.

* Pour les cookies internes (`kndcrt_*`), l’indicateur `Secure` n’est défini que lorsque le contexte de la requête est sécurisé (HTTPS) et que le référent ([en-tête HTTP du référent](https://developer.mozilla.org/fr-FR/docs/Web/HTTP/Headers/Referer)) est également HTTPS. Si le référent n’est pas sécurisé (HTTP), l’indicateur `Secure` est retiré pour permettre au SDK web de les lire. Un cookie sécurisé ne peut pas être lu à partir d’un contexte non sécurisé.
* Pour le cookie tiers (demdex), l’indicateur `Secure` est toujours défini, car toutes les requêtes sont HTTPS. Par conséquent, le contexte de la requête est sécurisé et ce cookie n’est jamais lu à partir de JavaScript.

L’indicateur `Secure` n’est pas présent dans la [représentation des métadonnées des cookies](#state-as-metadata). Seul l’attribut `SameSite` est inclus. Dans ce cas, il est de la responsabilité du client de définir correctement l’indicateur `Secure` à chaque fois que l’attribut `SameSite` est présent. Les cookies avec `SameSite=None` doivent également spécifier l’attribut `Secure`, car ils nécessitent un contexte sécurisé (HTTPS).
