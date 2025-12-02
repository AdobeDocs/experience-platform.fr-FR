---
title: setDebug()
description: Activez le débogage sur votre site via la console du navigateur.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

La méthode `_satellite.setDebug()` vous permet d’activer ou de désactiver le [débogage](../use-cases/debugging.md) sur votre site. Cette méthode est destinée à s’exécuter localement dans la console de votre navigateur. Adobe vous conseille de ne pas appeler cette méthode dans les règles de balises.

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`** : active le [débogage](../use-cases/debugging.md). Les messages générés par la bibliothèque de balises (y compris [`_satellite.logger`](logger.md)) sont visibles dans la console de votre navigateur.
* **`_satellite.setDebug(false);`** : permet de désactiver le débogage. Les messages de console générés par la bibliothèque de balises ne sont pas visibles.

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>Les messages écrits avec des `console.log()` natifs de JavaScript sont toujours visibles par toute personne avec les outils de développement ouverts. Adobe recommande d’utiliser [`_satellite.logger`](logger.md) si possible.

## Persistance du mode de débogage

Lors de l’appel de cette méthode, le mode de débogage utilise la portée suivante :

* **Session du navigateur** : le mode de débogage persiste lors du chargement de la page. Elle reste activée jusqu’à ce que vous mettiez fin à la session du navigateur ou que vous la désactiviez explicitement.
* **Étendue à l’origine** : le mode de débogage persiste uniquement pour le même site (domaine + port + protocole).
* **Par profil de navigateur** : le mode de débogage n’est pas inter-profils.

D’autres formes de [débogage](../use-cases/debugging.md) peuvent avoir un impact sur le mode de débogage et le remplacer à l’aide de la méthode de la console du navigateur.
