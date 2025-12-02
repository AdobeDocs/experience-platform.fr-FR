---
title: prehidingStyle
description: Créez une définition CSS qui permet au contenu personnalisé de se charger sans scintillement.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

La propriété `prehidingStyle` vous permet de définir un sélecteur CSS pour masquer le contenu personnalisé jusqu’à son chargement. Cette propriété est utile dans les implémentations de Web SDK synchrones pour éviter le scintillement. Adobe recommande d’utiliser le [fragment de code de masquage préalable](/help/collection/use-cases/personalization/manage-flicker.md) pour les implémentations asynchrones de Web SDK.

Les sélecteurs CSS que vous définissez dans cette propriété commencent à masquer le contenu lorsque vous exécutez la première commande [`sendEvent`](../sendevent/overview.md) sur une page. Le contenu est affiché lorsqu’une réponse d’Adobe est reçue, ce qui inclut généralement du contenu personnalisé. Le contenu est également affiché si la commande `sendEvent` échoue ou expire.

Si vous incluez à la fois `prehidingStyle` et le fragment de code de masquage préalable dans votre implémentation, ce dernier est prioritaire sur cette propriété de configuration.

Définissez la chaîne de `prehidingStyle` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, rien n’est masqué lors de l’exécution de la première commande `sendEvent` sur une page. Définissez cette valeur sur le sélecteur CSS et le bloc de déclaration de votre choix pour les bibliothèques chargées de manière synchrone.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## Prémasquage du style à l’aide de l’extension de balise Web SDK

Ces paramètres peuvent être configurés dans l’extension de balise Web SDK à l’aide des paramètres de configuration de [Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md).
