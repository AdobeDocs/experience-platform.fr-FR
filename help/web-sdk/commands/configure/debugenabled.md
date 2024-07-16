---
title: debugEnabled
description: Utilisez le code pour activer les fonctionnalités de débogage dans le SDK Web.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

La propriété `debugEnabled` vous permet d’activer ou de désactiver le débogage à l’aide du code du SDK Web. Il s’agit de l’une des méthodes disponibles pour activer le [débogage](../../use-cases/debugging.md). L’activation du débogage dans votre mise en oeuvre peut s’avérer plus pratique que les autres méthodes lors du développement d’un site web lorsque vous souhaitez toujours activer le débogage. Cette méthode de débogage l’active pour tous les visiteurs. Elle n’est donc pas recommandée pour les pages de production.

Consultez la page de cas d’utilisation [Débogage](../../use-cases/debugging.md) pour plus d’informations sur l’activation du débogage.

## Activation du débogage à l’aide de l’extension de balise SDK Web

Aucune option de débogage n’est disponible en mode natif à l’aide de l’extension de balise SDK Web. Utilisez une [autre méthode de débogage](../../use-cases/debugging.md).

## Activation du débogage à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la valeur booléenne `debugEnabled` sur `true` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK, elle est définie par défaut sur `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
