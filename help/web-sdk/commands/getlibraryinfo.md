---
title: getLibraryInfo
description: Récupérez des informations sur la version actuelle de la bibliothèque SDK Web.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

La commande `getLibraryInfo` vous fournit des informations sur la version de la bibliothèque SDK Web actuellement utilisée. Vous pouvez utiliser cette commande pour effectuer le suivi des versions du SDK Web que vous déployez sur différentes propriétés web.

## Informations sur la bibliothèque à l’aide de l’extension de balise SDK Web

L’extension de balise ne fournit pas d’interface pour envoyer cette commande. Utilisez l’éditeur de code personnalisé, en respectant la syntaxe de la bibliothèque JavaScript.

Si vous exécutez cette commande à l’aide de l’extension de balise, la version de l’extension de balise et la version de la bibliothèque sont incluses, concaténées avec un symbole `+`. La version de la bibliothèque SDK Web est répertoriée en premier, suivie de la version de l’extension de balise.

## Informations sur la bibliothèque à l’aide de la bibliothèque JavaScript SDK Web

Exécutez la commande `getLibraryInfo` lors de l’appel de votre instance configurée du SDK Web. Cette commande est généralement associée à une promesse JavaScript qui vous permet de récupérer les objets qu’elle renseigne.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`libraryInfo.commands`** : tableau de commandes pris en charge par cette version du SDK Web.
* **`libraryInfo.configs`** : un tableau de paramètres de configuration pris en charge par cette version du SDK Web.
* **`libraryInfo.version`** : version de la bibliothèque SDK Web.
