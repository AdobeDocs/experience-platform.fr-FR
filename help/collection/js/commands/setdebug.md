---
title: setDebug
description: Activez ou désactivez le paramètre de débogage Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

La commande `setDebug` permet d’accéder au mode de débogage ou d’en quitter le SDK Web. Il s’agit de l’une des nombreuses options disponibles pour [débogage](../../use-cases/debugging.md). Adobe conseille d’activer le mode de débogage dans les environnements de développement ou uniquement sur votre ordinateur local dans les environnements de production.

Exécutez la commande `setDebug` lors de l’appel de votre instance configurée de Web SDK. La seule option de l’objet de configuration est `enabled`, qui est une valeur booléenne qui détermine si le mode de débogage est activé.

```js
alloy("setDebug", {"enabled": true});
```

## Définir le débogage à l’aide de l’extension de balise Web SDK

Appelez [`_satellite.setDebug()`](/help/collection/tags/setdebug.md) dans la console du navigateur sur une page sur laquelle une bibliothèque de balises est implémentée. L’extension de balise Web SDK ne permet pas d’activer/désactiver les options de débogage dans l’interface utilisateur des balises elle-même.
