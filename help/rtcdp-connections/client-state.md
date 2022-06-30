---
title: Gestion de l’état client
description: Découvrez comment Adobe Experience Platform Edge Network gère l’état du client
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: client;état;gestion;périphérie;réseau;passerelle;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 3%

---

# Gestion de l’état client

Le réseau Edge lui-même est sans état (il ne conserve pas sa propre session). Cependant, certains cas d’utilisation nécessitent une persistance de l’état côté client, comme :

* Identification cohérente des appareils (voir [identification des visiteurs](visitor-identification.md))
* Collecte et application du consentement de l’utilisateur
* Conservation de l’ID de session de personnalisation

Le réseau Edge utilise un protocole de gestion des états, déléguant l’aspect de stockage à son client/SDK et inclut des entrées d’état dans ses réponses. Pour les navigateurs, les entrées sont stockées sous la forme de cookies.

La responsabilité du client est de les stocker et de les inclure dans toutes les requêtes suivantes. Le client doit également veiller à l’expiration correcte des entrées, conformément aux instructions de la passerelle. Lorsque les entrées ont été stockées sous la forme de cookies, le navigateur effectue toutes ces opérations automatiquement.

Bien que les entrées d’état aient toujours une valeur simple `String` (visible par l’appelant/le SDK), vous ne devez pas utiliser ni modifier les valeurs d’aucune manière. La structure/le format de la valeur ou même le nom lui-même peut changer à tout moment, ce qui peut entraîner un comportement inattendu pour les clients qui utilisent l’état en interne. L’état est conçu pour être toujours utilisé par la passerelle elle-même ou d’autres services Edge.

## Conserver l’état client en tant que métadonnées

L’état renvoyé par la variable [!DNL Edge Network] dans le corps de la réponse est une `Handle` avec le type `state:store`.

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
| `maxAge` | Nombre entier | *Facultatif* Durée de vie (TTL) de l’entrée, en secondes. En cas d’absence, les entrées ne doivent être stockées que pour la session en cours. |
| `attrs` | `Map<String, String>` | *Facultatif*. Liste facultative d’attributs d’entrée. Pour toutes les connexions sécurisées avec un en-tête HTTP de référent sécurisé, la variable `SameSite` est défini sur `None`. |


Pour prendre en charge le balisage multiple (c’est-à-dire plusieurs instances de SDK dans la même propriété, qui peuvent potentiellement référencer différentes organisations), toutes les entrées d’état sont automatiquement précédées du préfixe `kndctr_` et l’ID d’organisation sécurisé par une URL.

Lorsque le SDK client reçoit une `state:store` dans la réponse , il doit effectuer les opérations suivantes :

* Stocker les entrées côté client, en respectant le délai d’expiration fourni par la passerelle.
* Chargez-les à partir du magasin client et incluez toutes les entrées non expirées dans les requêtes suivantes.

Voici un exemple de requête qui transmet l’état stocké côté client :

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

## Conserver l’état du client dans les cookies de navigateur

Lorsque vous utilisez des clients de navigateur, le réseau Edge peut conserver automatiquement les entrées en tant que cookies de navigateur. Cela permet une prise en charge transparente du stockage des états, puisque les navigateurs respectent le protocole de gestion des états par défaut.

Presque toutes les entrées sont matérialisées en tant que cookies propriétaires lorsqu’elles sont activées et prises en charge (voir la note ci-dessous), mais la passerelle peut également stocker certains cookies tiers lorsque des cookies tiers sont `adobedc.demdex.net` domain est utilisé.

Comme les entrées sont toujours liées à une portée spécifique (appareil/application) par leur définition, seul le sous-ensemble compatible avec le contexte de requête actuel sera écrit par le réseau Edge. Les entrées non écrites sont renvoyées dans une `state:store` gestion.

En règle générale, les entrées de portée de l’application sont toujours écrites en tant que cookies propriétaires, tandis que les entrées de portée de l’appareil sont écrites en tant que cookies tiers. La décision est totalement transparente pour l’appelant. La passerelle décide quelles entrées peuvent être écrites, selon le contexte de l’appel.

L’appelant doit explicitement activer la prise en charge du stockage de l’état du client en tant que cookies, via l’événement `meta.state.cookiesEnabled` Indicateur :

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
| `cookiesEnabled` | Booléen | Lorsqu’elle est définie, la prise en charge des cookies est activée. La valeur par défaut est `false`. |
| `domain` | Chaîne | Requis when `cookiesEnabled: true`. Domaine de niveau supérieur sur lequel les cookies doivent être écrits. Le réseau Edge utilise cette valeur pour décider si l’état peut être conservé en tant que cookies. |

Même si la prise en charge des cookies est activée via la variable `cookiesEnabled` Indicateur : Adobe Experience Platform Edge Network écrira uniquement les entrées d’état si le domaine de niveau supérieur de la requête correspond à la variable `domain` spécifié par l’appelant. En cas de non-correspondance, les entrées sont renvoyées dans une `state:store` gestion.

Les cookies propriétaires ne peuvent pas être écrits (même si la prise en charge est activée) dans les cas suivants :

* La demande est envoyée à un tiers `adobedc.demdex.net` domaine.
* La demande est envoyée par un propriétaire `CNAME` domaine, différent de celui spécifié par l’appelant dans `meta.state.domain`.

## Sécurité des cookies

Tous les cookies ont la variable [Indicateur sécurisé](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) activée dans la mesure du possible.

Tous les cookies sécurisés comportent la variable [Attribut SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) défini sur `None`, ce qui signifie que les cookies sont envoyés dans tous les contextes, aussi bien propriétaires que cross-origin.

* Pour les cookies propriétaires (`kndcrt_*`), la variable `Secure` L’indicateur n’est défini que lorsque le contexte de la requête est sécurisé (HTTPS) et lorsque le référent ([En-tête HTTP du référent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) est également HTTPS. Si le référent n’est pas sécurisé (HTTP), la variable `Secure` est omis pour permettre au SDK Web de les lire. Un cookie sécurisé ne peut pas être lu à partir d’un contexte non sécurisé.
* Pour le cookie tiers (demdex), la variable `Secure` L’indicateur est toujours défini, car toutes les requêtes sont HTTPS. Par conséquent, le contexte de la requête est sécurisé et ce cookie n’est jamais lu à partir de JavaScript.

Le `Secure` L’indicateur n’est pas présent dans la variable [représentation des métadonnées des cookies](#state-as-metadata). Seule la variable `SameSite` est inclus. Dans ce cas, il est de la responsabilité du client de définir correctement la variable `Secure` à chaque fois que la variable `SameSite` est présent. Cookies avec `SameSite=None` doit également spécifier la variable `Secure` , puisqu’ils nécessitent un contexte sécurisé (HTTPS).
