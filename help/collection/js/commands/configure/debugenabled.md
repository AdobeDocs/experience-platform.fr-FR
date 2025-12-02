---
title: debugEnabled
description: Utilisez le code pour activer les fonctionnalités de débogage dans le Web SDK.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

La propriété `debugEnabled` vous permet d’activer ou de désactiver le débogage à l’aide du code Web SDK. Il s’agit de l’une des méthodes disponibles pour activer le [débogage](/help/collection/use-cases/debugging.md). L’activation du débogage dans votre implémentation peut être plus pratique que d’autres méthodes lors du développement de sites web lorsque vous souhaitez toujours activer le débogage. Cette méthode de débogage l’active pour tous les visiteurs. Elle n’est donc pas recommandée pour les pages d’exploitation. Consultez la page du cas d’utilisation [Débogage](/help/collection/use-cases/debugging.md) pour découvrir d’autres façons d’activer le débogage.

Définissez le booléen `debugEnabled` sur `true` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK, elle est définie par défaut sur `false`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## Activer le débogage à l’aide de l’extension de balise Web SDK

Aucune option de débogage n’est disponible en mode natif à l’aide de l’extension de balise Web SDK. Utilisez une [autre méthode de débogage](/help/collection/use-cases/debugging.md) lors de la configuration de la propriété de balise.
