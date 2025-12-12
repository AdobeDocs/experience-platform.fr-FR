---
title: Modules de bibliothèque principaux pour les extensions web
description: Découvrez les principaux modules Bibliothèque que vous pouvez utiliser dans vos extensions web.
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 100%

---

# Modules de bibliothèque principaux pour les extensions web

Ce document fournit une liste de modules de bibliothèque principaux que vous pouvez utiliser dans vos extensions web. Vous pouvez accéder à ces modules à l’aide de `require('@adobe/{MODULE}')`, où `{MODULE}` est le nom du module principal à utiliser.

## [!DNL reactor-object-assign]

`reactor-object-assign` imite la [`Object.assign`](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Objets_globaux/Object/assign) méthode native en copiant les propriétés des objets sources vers un objet cible.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

L’objet `reactor-cookie` est un utilitaire permettant de lire et d’écrire des cookies. Pour plus d’informations, voir le [package npm js-cookie](https://www.npmjs.com/package/js-cookie).

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` représente l’objet [`Document`](https://developer.mozilla.org/fr-FR/docs/Web/API/Document). Cela peut être bénéfique lors du test du module en permettant aux tests d’injecter un objet `document` fictif à l’aide d’utilitaires tels que [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` est un utilitaire d’analyse et de sérialisation des [chaînes de requête](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

Cet utilitaire utilise les méthodes suivantes :

* `queryString.parse({STRING})` : analyse une chaîne de requête dans un objet. Les caractères de début `?`, `#` et `&` sur la chaîne de requête sont ignorés.
* `queryString.stringify({OBJECT})` : convertit un objet en chaîne de requête.

### [!DNL reactor-load-script]

`reactor-load-script` est une fonction qui charge un script lorsqu’on lui donne une URL. Une balise de script sera créée et placée dans le nœud `head` du document. Une [promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) est renvoyée, que vous pouvez utiliser pour déterminer quand le chargement du script réussit ou échoue.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` est un constructeur qui imite l’[API Promise](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) native dans ECMAScript 6. Si l’API Promise native est disponible, elle est renvoyée à la place.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` représente l’objet [`Window`](https://developer.mozilla.org/fr-FR/docs/Web/API/Window). Cela peut être bénéfique lors du test du module en permettant aux tests d’injecter un objet `Window` fictif à l’aide d’utilitaires tels que [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
