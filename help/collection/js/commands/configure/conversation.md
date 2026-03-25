---
title: conversation
description: Configurez les paramètres de conversation Brand Concierge.
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 13%

---

# `conversation`

>[!AVAILABILITY]
>
>Brand Concierge pour le SDK Web est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

L’objet `conversation` contient des options de configuration pour les sessions de conversation Brand Concierge. Cet objet est pris en charge dans les versions 2.31.0 ou ultérieures de Web SDK.

## Propriétés

| Propriété | Type | Description |
| --- | --- | --- |
| **`collectSources`** | `boolean` | Détermine si le SDK Web lit le paramètre de chaîne de requête `adobe_brand_concierge_source` et l&#39;inclut dans `xdm.channel.referringSource`. La valeur par défaut est `false`. |
| **`stickyConversationSession`** | `boolean` | Détermine si le SDK Web définit un cookie de session pour conserver les sessions de conversation Brand Concierge entre les chargements de page. La valeur par défaut est `false`. Si cet attribut est omis ou défini sur `false`, la conversation Brand Concierge démarre une nouvelle session à chaque chargement de page. |

## Exemple

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## Configuration des paramètres de conversation à l’aide de l’extension de balise Web SDK

Ces paramètres peuvent être configurés dans l’extension de balise Web SDK à l’aide des paramètres de [Brand Concierge](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
