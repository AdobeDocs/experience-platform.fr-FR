---
title: thirdPartyCookiesEnabled
description: Autorisez l’utilisation de cookies tiers pour identifier les visiteurs.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

La propriété `thirdPartyCookiesEnabled` est une valeur booléenne qui détermine si le SDK Web définit les cookies dans un contexte tiers. L’activation de cette option est utile si vous souhaitez identifier les visiteurs entre les sous-domaines ou les domaines détenus par votre organisation. Cependant, de nombreux navigateurs modernes limitent la définition et l’expiration des cookies tiers. Si le navigateur d’un visiteur ne prend pas en charge les cookies tiers, cette propriété n’a aucun effet.

La propriété `thirdPartyCookiesEnabled` contrôle également si un [`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk) peut être demandé lors d’appels [`getIdentity`](../getidentity.md).

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
