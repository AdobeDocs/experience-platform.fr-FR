---
title: Installation du SDK Web de Adobe Experience Platform
description: Découvrez la procédure d’installation du SDK Web d’Experience Platform.
keywords: installation du sdk web;installation du sdk web;internet explorer;promesse;package npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 31%

---

# Installation du SDK {#installing-the-sdk}

Il existe trois façons d’utiliser le SDK Web de Adobe Experience Platform prises en charge :

1. La méthode recommandée pour utiliser le SDK Web de Adobe Experience Platform consiste à utiliser l’interface utilisateur de collecte de données ou l’interface utilisateur Experience Platform.
1. Le SDK Web de Adobe Experience Platform est également disponible sur un réseau de diffusion de contenu (CDN) que vous pouvez utiliser.
1. Utilisez la bibliothèque NPM qui exporte les modules EcmaScript 5 et EcmaScript 2015 (ES6).

## Option 1 : Installation de l’extension de balise

Pour obtenir de la documentation sur l’extension de balise, reportez-vous à la section [documentation de lancement](../../tags/extensions/web/sdk/overview.md)

## Option 2 : Installation de la version autonome prédéfinie

La version prédéfinie est disponible sur un CDN. Vous pouvez référencer la bibliothèque sur le réseau de diffusion de contenu directement sur votre page, ou la télécharger et l’héberger sur votre propre infrastructure. Il est disponible dans des formats minimisés et non minimisés. La version non minimisée est utile à des fins de débogage.

Structure de l’URL : https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OU alloy.js pour la version non minimisée.

Par exemple :


* Minified : [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Non minimisé : [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)


### Ajout du code {#adding-the-code}

La version autonome prédéfinie nécessite un &quot;code de base&quot; ajouté directement à la page. Copiez et collez le &quot;code de base&quot; suivant le plus haut possible dans la `<head>` de votre HTML :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

Le &quot;code de base&quot; crée une fonction globale nommée `alloy`. Utilisez cette fonction pour interagir avec le SDK. Si vous souhaitez appeler autrement la fonction globale, modifiez la variable `alloy` name comme suit :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

Dans cet exemple, la fonction globale est renommée `mycustomname`, au lieu de `alloy`.

>[!IMPORTANT]
>
>Pour éviter des problèmes potentiels, utilisez un nom contenant au moins un caractère qui n’est pas un chiffre et qui n’entre pas en conflit avec le nom d’une propriété existant déjà sur `window`.

Ce code de base, en plus de créer une fonction globale, charge également le code supplémentaire contenu dans un fichier externe \(`alloy.js`\) hébergé sur un serveur. Par défaut, ce code est chargé de manière asynchrone pour permettre à votre page web d’être aussi performante que possible. Il s’agit de l’implémentation recommandée.

### Prise en charge d’Internet Explorer {#support-internet-explore}

Ce SDK utilise des promesses, qui sont une méthode de communication de l’achèvement des tâches asynchrones. Le [Promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) La mise en oeuvre utilisée par le SDK est prise en charge en mode natif par tous les navigateurs cibles, à l’exception de [!DNL Internet Explorer]. Pour utiliser le SDK sur [!DNL Internet Explorer], vous devez avoir `window.Promise` [polyfillé](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Pour déterminer si `window.Promise` est déjà polyfillé :

1. Ouvrez votre site web dans [!DNL Internet Explorer].
1. Ouvrez la console de débogage du navigateur.
1. Saisissez `window.Promise` dans la console, puis appuyez sur Entrée.

Si autre chose que `undefined` s’affiche, `window.Promise` est déjà polyfillé. Une autre façon de déterminer si `window.Promise` est polyfillé consiste à charger votre site web après avoir suivi les instructions d’installation ci-dessus. Si le SDK renvoie une erreur à propos d’une promesse, il est probable que `window.Promise` n’ait pas été polyfillé.

Si vous avez déterminé que vous devez polyfiller `window.Promise`, incluez la balise de script suivante au-dessus du code de base fourni précédemment :

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Cette balise charge un script qui s’assure que `window.Promise` est une implémentation de promesse valide.

>[!NOTE]
>
>Si vous choisissez de charger une implémentation de promesse différente, assurez-vous qu’elle prend en charge `Promise.prototype.finally`.

### Chargement synchrone du fichier JavaScript {#loading-javascript-synchronously}

Comme expliqué dans la section [Ajout du code](#adding-the-code), le code de base que vous avez copié et collé dans le HTML de votre site web charge un fichier externe. Le fichier externe contient les principales fonctionnalités du SDK. Toute commande que vous tentez d’exécuter pendant le chargement de ce fichier est mise en file d’attente, puis traitée une fois le fichier chargé. Le chargement asynchrone du fichier est la méthode d’installation la plus performante.

Dans certaines circonstances, toutefois, vous pouvez vouloir charger le fichier de manière synchrone \(des informations supplémentaires sur ces circonstances seront documentées ultérieurement\). Cela empêche le reste du HTML d’être analysé et rendu par le navigateur jusqu’à ce que le fichier externe ait été chargé et exécuté. Ce délai supplémentaire avant l’affichage du contenu principal pour les utilisateurs est généralement déconseillé, mais peut être pertinent en fonction des circonstances.

Pour charger le fichier de manière synchrone plutôt qu’asynchrone, supprimez l’attribut `async` de la deuxième balise `script`, comme illustré ci-dessous :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js"></script>
```

## Option 3 : Utilisation du package NPM

Le SDK Web Adobe Experience Platform est également disponible sous la forme d’un package NPM. [NPM](https://www.npmjs.com) est le gestionnaire de modules pour JavaScript. L’installation du package NPM vous permet de contrôler le processus de création pour le JavaScript du SDK Web Adobe Experience Platform. Le package NPM expose les modules EcmaScript version 5 ou les modules EcmaScript version 2015 (ES6) destinés à être exécutés dans le navigateur.

```bash
npm install @adobe/alloy
```

Le package NPM du SDK Web Adobe Experience Platform expose une `createInstance` fonction . Cette fonction est utilisée pour créer une instance. L’option de nom transmise à la fonction contrôle le préfixe utilisé dans la journalisation. Vous trouverez ci-dessous des exemples d’utilisation du module .

### Utilisation du package en tant que module ECMAScript 2015 (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Le package NPM repose sur les modules CommonJS ; par conséquent, lors de l’utilisation d’un bundler, assurez-vous que le bundler prend en charge les modules CommonJS. Certains lots, tels que [Cumul](https://rollupjs.org), requiert une [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) qui fournit la prise en charge de CommonJS.

### Utilisation du package comme module ECMAScript 5

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Prise en charge d’Internet Explorer

Le SDK Adobe Experience Platform utilise des promesses, qui sont une méthode de communication de l’achèvement des tâches asynchrones. Le [Promesse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) La mise en oeuvre utilisée par le SDK est prise en charge en mode natif par tous les navigateurs cibles, à l’exception de [!DNL Internet Explorer]. Pour utiliser le SDK sur [!DNL Internet Explorer], vous devez avoir `window.Promise` [polyfillé](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Une bibliothèque que vous pouvez utiliser pour polyfiller la promesse est promesse-polyfill. Voir [documentation promo-polyfill](https://www.npmjs.com/package/promise-polyfill) pour plus d’informations sur la procédure d’installation avec NPM.

>[!NOTE]
>
>Si vous choisissez de charger une implémentation de promesse différente, assurez-vous qu’elle prend en charge `Promise.prototype.finally`.
