---
title: Modules de bibliothèque dans les extensions web
description: Découvrez comment formater des modules de bibliothèque pour les extensions web dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '377'
ht-degree: 100%

---

# Modules de bibliothèque dans les extensions web

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

>[!IMPORTANT]
>
>Ce document couvre le format du module de bibliothèque pour les extensions web. Si vous développez une extension Edge, reportez-vous au guide sur le [formatage des modules d’extension Edge](../edge/format.md) à la place.

Un module de bibliothèque est un morceau de code réutilisable fourni par une extension émise dans la bibliothèque d’exécution des balises d’Adobe Experience Platform. Cette bibliothèque s’exécute ensuite sur le site web du client. Par exemple, un type d’événement `gesture` comporte un module Bibliothèque qui s’exécutera sur le site web du client et détectera les mouvements des utilisateurs.

Le module Bibliothèque est structuré comme un [module CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1). Dans un module CommonJS, les variables suivantes peuvent être utilisées :

## [!DNL require]

Vous pouvez accéder à une fonction `require` :

1. Modules principaux fournis par les balises. Ces modules sont accessibles à l’aide de `require('@adobe/reactor-name-of-module')`. Pour plus d’informations, consultez le document sur les [modules principaux](./core.md) disponibles.
1. Autres modules de votre extension. Tout module de votre extension est accessible via un chemin relatif. Le chemin relatif doit commencer par `./` ou `../`.

Cas d’utilisation :

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## [!DNL module]

Une variable libre nommée `module` est disponible, ce qui vous permet d’exporter l’API du module.

Cas d’utilisation :

```javascript
module.exports = function(…) { … }
```

## [!DNL exports]

Une variable libre nommée `exports` est disponible, ce qui vous permet d’exporter l’API du module.

Cas d’utilisation :

```javascript
exports.sayHello = function(…) { … }
```

Il s’agit d’une alternative à `module.exports` mais son utilisation est plus limitée. Veuillez lire [Présentation de la variable module.exports et des exports dans node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) pour mieux comprendre les différences entre `module.exports` et `exports` et les avertissements connexes liés à l’utilisation de `exports`. En cas de doute, simplifiez-vous la vie et utilisez `module.exports` plutôt que `exports`.

## Exécution et mise en cache

Lorsque la bibliothèque d’exécution des balises s’exécute, les modules sont immédiatement « installés » et leurs exports sont mis en cache. En supposant le module suivant :

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` sera consigné immédiatement, alors que `runs when necessary` ne sera consigné qu’une fois la fonction exportée appelée par le moteur des balises. Bien que cela puisse être inutile dans le cadre de votre module particulier, vous pouvez en profiter en effectuant toute configuration nécessaire avant d’exporter la fonction.
