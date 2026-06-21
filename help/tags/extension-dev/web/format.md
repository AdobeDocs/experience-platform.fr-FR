---
title: Modules de bibliothèque dans les extensions web
description: Découvrez comment formater des modules de bibliothèque pour les extensions web dans Adobe Experience Platform.
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
TQID: https://experienceleague.adobe.com/Qa76k-3GOH0qISa8erYFj5qkuN7FEDFrrCDkw-Hnsb8
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 340
ht-degree: 100%

---

# Modules de bibliothèque dans les extensions web

>[!IMPORTANT]
>
>Ce document couvre le format du module de bibliothèque pour les extensions web. Si vous développez une extension Edge, reportez-vous au guide sur le [formatage des modules d’extension Edge](../edge/format.md) à la place.

Un module de bibliothèque est un morceau de code réutilisable fourni par une extension émise dans la bibliothèque d’exécution des balises d’Adobe Experience Platform. Cette bibliothèque sʼexécute ensuite sur le site web du client. Par exemple, un type d’événement `gesture` comporte un module Bibliothèque qui s’exécutera sur le site web du client et détectera les mouvements des utilisateurs.

Le module Bibliothèque est structuré comme un [module CommonJS](https://nodejs.org/api/modules.html#modules-commonjs-modules). Dans un module CommonJS, les variables suivantes peuvent être utilisées :

## `require`

Vous pouvez accéder à une fonction `require` :

1. Modules principaux fournis par les balises. Ces modules sont accessibles à l’aide de `require('@adobe/reactor-name-of-module')`. Pour plus d’informations, consultez le document sur les [modules principaux](./core.md) disponibles.
1. Autres modules de votre extension. Tout module de votre extension est accessible via un chemin relatif. Le chemin relatif doit commencer par `./` ou `../`.

Cas d’utilisation :

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## `module`

Une variable libre nommée `module` est disponible, ce qui vous permet d’exporter l’API du module.

Cas d’utilisation :

```javascript
module.exports = function(…) { … }
```

## `exports` {#exports-variable}

Une variable libre nommée `exports` est disponible, ce qui vous permet d’exporter l’API du module.

Cas d’utilisation :

```javascript
exports.sayHello = function(…) { … }
```

Il s’agit d’une alternative à `module.exports` mais son utilisation est plus limitée. Veuillez lire [Présentation de la variable module.exports et des exports dans node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) pour mieux comprendre les différences entre `module.exports` et `exports` et les avertissements connexes liés à l’utilisation de `exports`. En cas de doute, simplifiez-vous la vie et utilisez `module.exports` plutôt que `exports`.

## Exécution et mise en cache

Lorsque la bibliothèque d’exécution des balises sʼexécute, les modules sont immédiatement « installés » et leurs exports sont mis en cache. En supposant le module suivant :

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` sera consigné immédiatement, alors que `runs when necessary` ne sera consigné quʼune fois la fonction exportée appelée par le moteur de balise. Bien que cela puisse être inutile dans le cadre de votre module particulier, vous pouvez en profiter en effectuant toute configuration nécessaire avant d’exporter la fonction.
