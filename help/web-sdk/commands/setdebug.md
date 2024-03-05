---
title: setDebug
description: Activez ou désactivez le paramètre de débogage du SDK Web.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

La variable `setDebug` vous permet d’entrer ou de quitter le mode de débogage dans le SDK Web. Il s’agit de l’une des options disponibles pour [débogage](../use-cases/debugging.md). Adobe conseille d’activer le mode de débogage dans les environnements de développement ou simplement sur votre ordinateur local dans les environnements de production.

## Définition du débogage à l’aide de l’extension de balise SDK Web

L’extension de balise ne permet pas d’activer/désactiver les options de débogage dans l’interface utilisateur. Vous pouvez utiliser l’éditeur de code personnalisé à l’aide de la syntaxe JavaScript ou saisir le code JavaScript dans la console du navigateur lorsque vous vous trouvez sur votre site.

## Définir le débogage à l’aide de la bibliothèque JavaScript du SDK Web

Exécutez la variable `setDebug` lors de l’appel de votre instance configurée du SDK Web. La seule option de l’objet de configuration est `enabled`, qui est une valeur booléenne qui détermine si le mode de débogage est activé.

```js
alloy("setDebug", {"enabled": true});
```
