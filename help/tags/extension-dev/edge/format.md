---
title: Modules de bibliothèque dans les extensions Edge
description: Mise en forme des modules de bibliothèque pour les extensions de balise dans une propriété Edge.
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 100%

---

# Modules de bibliothèque dans les extensions Edge

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

>[!IMPORTANT]
>
>Ce document couvre le format du module de bibliothèque pour les extensions Edge. Si vous développez une extension web, consultez le guide de [formatage des modules d’extension web](../web/format.md) à la place.

Un module de bibliothèque est un morceau de code réutilisable fourni par une extension émise dans la bibliothèque d’exécution de balises d’Adobe Experience Platform (la bibliothèque exécutée sur le nœud Edge). Par exemple, un type d’action `sendBeacon` aura un module de bibliothèque exécuté sur le nœud Edge et enverra une balise.

Le module Bibliothèque est structuré comme un [module CommonJS](https://nodejs.org/api/modules.html#modules-commonjs-modules). Dans un module CommonJS, les variables suivantes peuvent être utilisées :

## [!DNL require]

Une fonction `require` est à disposition pour vous permettre d’accéder aux modules de votre extension. Tout module de votre extension est accessible via un chemin relatif. Le chemin relatif doit commencer par `./` ou `../`.

Cas d’utilisation :

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

Une variable libre nommée `module` est disponible, ce qui vous permet d’exporter l’API du module.

Cas d’utilisation :

```js
module.exports = (…) => { … }
```

## [!DNL exports]

Une variable libre nommée `exports` est disponible, ce qui vous permet d’exporter l’API du module.

Cas d’utilisation :

```js
exports.sayHello = (…) => { … }
```

Il s’agit d’une alternative à `module.exports` mais son utilisation est plus limitée. Veuillez lire [Présentation de la variable module.exports et des exports dans node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) pour mieux comprendre les différences entre `module.exports` et `exports` et les avertissements connexes liés à l’utilisation de `exports`. En cas de doute, simplifiez-vous la vie et utilisez `module.exports` plutôt que `exports`.

## Signature du module côté serveur

Tous les types de module (éléments de données, conditions ou actions) fournis par votre extension seront appelés avec les mêmes paramètres : [contexte](./context.md).

```js
exports.sayHello = (context) => { … }
```
