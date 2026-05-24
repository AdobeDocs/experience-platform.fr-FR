---
title: thirdPartyCookiesEnabled
description: Autorisez l’utilisation de cookies tiers pour identifier les visiteurs.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
TQID: https://experienceleague.adobe.com/Do2Kw6kb1yxrwmqU7SD3hGL9eqorgWDb68FsAKkUYUY
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 207
ht-degree: 4%

---

# `thirdPartyCookiesEnabled`

La propriété `thirdPartyCookiesEnabled` est une valeur booléenne qui détermine si le SDK Web définit les cookies dans un contexte tiers. L’activation de cette option est utile si vous souhaitez identifier les visiteurs entre les sous-domaines ou les domaines détenus par votre organisation. Cependant, de nombreux navigateurs modernes limitent la définition et l’expiration des cookies tiers. Si le navigateur d’un visiteur ne prend pas en charge les cookies tiers, cette propriété n’a aucun effet.

La propriété `thirdPartyCookiesEnabled` contrôle également si un [`CORE ID`](/help/collection/identity/overview.md#core-id-and-third-party-identity) peut être demandé lors d’appels [`getIdentity`](../getidentity.md).

Lorsque cette option est activée, le SDK Web utilise Adobe Audience Manager pour identifier un visiteur. Lorsque cette option est désactivée, l’appel à Audience Manager est désactivé. Voir [Comprendre les appels au domaine Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=fr) dans le guide de l’utilisateur d’Audience Manager pour plus d’informations.

Définissez la valeur booléenne `thirdPartyCookiesEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, elle est définie par défaut sur `true`. Définissez cette valeur sur `false` si vous ne souhaitez pas que le SDK Web utilise Audience Manager pour identifier les visiteurs.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## Activation des cookies tiers à l’aide de l’extension de balise Web SDK

Ce paramètre peut être configuré dans l’extension de balise Web SDK à l’aide des [&#x200B; Paramètres de configuration des identités &#x200B;](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies).
