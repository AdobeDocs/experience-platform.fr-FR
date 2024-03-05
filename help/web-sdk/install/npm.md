---
title: Installation du SDK Web à l’aide du package NPM
description: Utilisez un package NPM pour installer et référencer la bibliothèque SDK Web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Installation du SDK Web à l’aide du package NPM

Le SDK Web de Adobe Experience Platform est disponible sous la forme d’un [Package NPM](https://www.npmjs.com). L’installation du package NPM vous permet de contrôler le processus de génération de la bibliothèque JavaScript du SDK Web Adobe Experience Platform. Le package NPM expose les modules EcmaScript version 5 ou les modules EcmaScript version 2015 (ES6) destinés à être exécutés dans le navigateur.

```bash
npm install @adobe/alloy
```

Le package NPM du SDK Web Adobe Experience Platform expose une `createInstance` de la fonction L’option de nom transmise à la fonction contrôle le préfixe utilisé dans la journalisation. Vous trouverez ci-dessous des exemples d’utilisation du module .

## Utilisation du package comme module ECMAScript 2015 (ES6)

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Le package NPM repose sur des modules CommonJS ; par conséquent, lors de l’utilisation d’un bundler, assurez-vous que le bundler prend en charge les modules CommonJS. Certains lots, tels que [Cumul](https://rollupjs.org), requiert une [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) qui fournit la prise en charge de CommonJS.

## Utilisation du package comme module ECMAScript 5

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
