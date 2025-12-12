---
title: Modules partagés dans les extensions web
description: Découvrez comment définir des modules de bibliothèque partagés pour les extensions web dans Adobe Experience Platform.
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 100%

---

# Modules partagés dans les extensions web

Un module partagé est un mécanisme par lequel vous pouvez communiquer avec d’autres extensions. Par exemple, l’extension A peut charger un élément de données de manière asynchrone et le rendre accessible à l’extension B via une [promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise).

Dans les implémentations JavaScript, tous les modules partagés sont instanciés à l’aide de la méthode [`getSharedModule`](../turbine.md#shared) fournie par la variable libre `turbine`.

Les modules partagés sont inclus dans les bibliothèques de balises, et ce, même s’ils ne sont jamais appelés à partir d’autres extensions. Afin de ne pas augmenter inutilement la taille de la bibliothèque, vous devez faire attention à ce que vous exposez comme module partagé.

Les modules partagés ne comportent pas de composant de vue.

Lors du développement de votre propre extension de balise, vous pouvez définir tous les modules partagés que vous souhaitez qu’elle fournisse. Par exemple, vous pouvez créer un module qui charge un identifiant utilisateur de manière asynchrone, puis le partage avec toute autre extension via une promesse :

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

Dans le [manifeste d’extension](../manifest.md), vous devez fournir un nom pour ce module partagé. Si vous l’appelez `user-id-promise`, une autre extension peut alors accéder à ce module partagé comme suit :

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Les modules partagés peuvent être tout ce que vous pouvez généralement exporter à partir d’un module CommonJS (comme des fonctions, des objets, des chaînes, des nombres ou des valeurs booléennes).
