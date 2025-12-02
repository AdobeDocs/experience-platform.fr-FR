---
title: getLibraryInfo
description: Récupérez des informations sur la version actuelle de la bibliothèque Web SDK.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# `getLibraryInfo`

La commande `getLibraryInfo` fournit des informations sur la version de la bibliothèque Web SDK actuellement utilisée. Vous pouvez utiliser cette commande pour suivre les versions du Web SDK que vous déployez sur différentes propriétés web.

Exécutez la commande `getLibraryInfo` lors de l’appel de votre instance configurée de Web SDK. Cette commande est généralement associée à une promesse JavaScript qui vous permet de récupérer les objets qu’elle renseigne.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`libraryInfo.commands`** : tableau de commandes pris en charge par cette version de Web SDK.
* **`libraryInfo.configs`** : tableau de paramètres de configuration pris en charge par cette version de Web SDK.
* **`libraryInfo.version`** : version de la bibliothèque Web SDK.

## Informations sur la bibliothèque à l’aide de l’extension de balise Web SDK

L’extension de balise ne fournit pas d’interface pour envoyer cette commande. Utilisez l’éditeur de code personnalisé, en respectant la syntaxe de la bibliothèque JavaScript.

Si vous exécutez cette commande à l’aide de l’extension de balise, la version de l’extension de balise et la version de bibliothèque sont incluses, concaténées avec un symbole `+`. La version de la bibliothèque Web SDK est répertoriée en premier, suivie de la version de l’extension de balise.
