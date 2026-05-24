---
title: Installer le SDK Web à l’aide du package NPM
description: Utilisez un package NPM pour installer et référencer la bibliothèque Web SDK.
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
TQID: https://experienceleague.adobe.com/72KJtyfIf-2QXKbRLxuTuttBOFsmovDBGIeK8uNkOr8
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 174
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
