---
title: Installer le SDK Web à l’aide du package NPM
description: Utilisez un package NPM pour installer et référencer la bibliothèque Web SDK.
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: b1574940b3afbd98cd60a079fdf7b10153e8e9d7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Installer le SDK Web à l’aide du package NPM

Adobe Experience Platform Web SDK est disponible sous la forme d’un [package NPM](https://www.npmjs.com). L’installation du package NPM vous permet de contrôler le processus de création de la bibliothèque JavaScript Adobe Experience Platform Web SDK. Le package NPM expose les modules EcmaScript version 5 ou les modules EcmaScript version 2015 (ES6) destinés à être exécutés dans le navigateur.

```bash
npm install @adobe/alloy
```

Le package NPM de Adobe Experience Platform Web SDK expose une fonction `createInstance`. L’option de nom transmise à la fonction contrôle le préfixe utilisé dans la journalisation. Vous trouverez ci-dessous des exemples d’utilisation du package .

## Utilisation du package comme module ECMAScript 2015 (ES6)

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Le package NPM repose sur des modules CommonJS. Par conséquent, lors de l’utilisation d’un bundler, assurez-vous que le bundler prend en charge les modules CommonJS. Certains bundlers, comme [Rollup](https://rollupjs.org), nécessitent un [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) qui fournit la prise en charge de CommonJS.

## Utilisation du package comme module ECMAScript 5

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```
