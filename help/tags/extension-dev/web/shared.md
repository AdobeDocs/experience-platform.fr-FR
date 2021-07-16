---
title: Modules partagés dans les extensions web
description: Découvrez comment définir des modules de bibliothèque partagés pour les extensions web dans Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 78%

---

# Modules partagés dans les extensions web

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Un module partagé est un mécanisme par lequel vous pouvez communiquer avec d’autres extensions. Dans les implémentations JavaScript, tous les modules partagés sont instanciés à l’aide de la méthode [`getSharedModule`](../turbine.md#shared) fournie par la variable libre `turbine`.

Lors du développement de votre propre extension de balise, vous pouvez définir tous les modules partagés que vous souhaitez qu’elle fournisse. Par exemple, vous pouvez créer un module qui charge un identifiant utilisateur de manière asynchrone, puis le partage avec toute autre extension via une [promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) :

```javascript
var userIdPromise = new Promise(/* load user id, then resolve promise */);
module.exports = userIdPromise;
```

Dans le [manifeste d’extension](../manifest.md), vous devez fournir un nom pour ce module partagé. Si vous l’appelez `user-id-promise`, une autre extension peut alors accéder à ce module partagé comme suit :

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Les modules partagés peuvent être tout ce que vous pouvez généralement exporter à partir d’un module CommonJS (comme des fonctions, des objets, des chaînes, des nombres ou des valeurs booléennes).
