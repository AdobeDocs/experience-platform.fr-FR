---
title: Implémentation de bibliothèques tierces
description: Découvrez les différentes méthodes d’hébergement de bibliothèques tierces dans vos extensions de balises Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 67%

---

# Implémentation de bibliothèques tierces

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

L’un des principaux objectifs des extensions de balises dans Adobe Experience Platform est de vous permettre de mettre en oeuvre facilement les technologies (bibliothèques) marketing existantes dans votre site web. Utilisez les extensions pour implémenter les bibliothèques fournies par les réseaux de diffusion de contenu de tiers (Content diffusion Network) sans avoir à modifier manuellement le code HTML de votre site web.

Il existe plusieurs méthodes pour héberger des bibliothèques tierces (fournisseurs) dans vos extensions. Ce document présente un aperçu de ces différentes méthodes d’implémentation, y compris les avantages et les inconvénients de chacune de ces méthodes.

## Conditions préalables

Ce document nécessite une compréhension pratique des extensions dans les balises, y compris ce qu’elles peuvent faire et comment elles sont composées. Pour plus d’informations, consultez la [présentation du développement des extensions](./overview.md).

## Processus de chargement du code de base

En dehors du contexte des balises, il est important de comprendre comment les technologies marketing se chargent généralement sur un site web. Les fournisseurs de bibliothèques tierces fournissent un fragment de code (appelé code de base) qui doit être incorporé dans le code HTML de votre site web pour charger les fonctionnalités de la bibliothèque.

En général, les codes de base des technologies de marketing exécutent une variante du processus suivant lors du chargement sur votre site :

1. Configurez une fonction globale pouvant être utilisée pour interagir avec la bibliothèque du fournisseur.
1. Chargez la bibliothèque du fournisseur.
1. Effectuez une série d’appels initiaux en file d’attente vers la fonction globale à des fins de configuration et de suivi.

Pendant la configuration initiale de la fonction globale, vous pouvez encore appeler la fonction avant que le chargement de la bibliothèque ne soit terminé. Tous les appels que vous effectuez sont ajoutés au mécanisme de file d’attente du code de base, puis exécutés dans l’ordre séquentiel une fois la bibliothèque chargée.

Quand le chargement de la bibliothèque est terminé, la fonction globale est remplacée par une nouvelle fonction qui contourne la file d’attente et traite immédiatement les appels futurs à la fonction.

### Exemple de code de base

Le code JavaScript suivant est un exemple de code de base non minimisé pour la [balise de conversion Pinterest](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?), qui sera référencée plus loin dans ce document pour démontrer comment le code de base doit être adapté à différentes stratégies d’implémentation avec des balises :

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

En résumé, le code de base ci-dessus fournit une [expression de fonction immédiatement invoquée (IIFE)](https://developer.mozilla.org/fr-FR/docs/Glossary/IIFE) qui crée une fonction globale pour interagir avec la bibliothèque (`window.pintrk`). Elle affecte également à une variable `scriptURL` la valeur `https://s.pinimg.com/ct/core.js`, qui représente l’emplacement de la bibliothèque. Comme expliqué précédemment, toutes les fonctions appelées avant le chargement de la bibliothèque sont placées dans une file d’attente (`window.pintrk.queue`) pour être exécutées en séquence une fois la bibliothèque disponible.

La partie suivante du code de base est la plus pertinente pour comprendre comment la bibliothèque se charge sur votre site :

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

Le code de base crée un élément de script, le définit pour un chargement asynchrone et définit l’`src`URL sur `https://s.pinimg.com/ct/core.js`. Il ajoute ensuite l’élément de script au document en l’insérant avant le premier élément de script déjà présent dans le document.

## Options de mise en oeuvre des balises

Les sections ci-dessous montrent les différentes manières de charger les bibliothèques de fournisseurs dans vos extensions, en utilisant le code de base Pinterest illustré précédemment comme exemple. Chacun de ces exemples implique la création d’un type d’action [pour une extension web](./web/action-types.md) qui charge la bibliothèque sur votre site web.

>[!NOTE]
>
>Bien que les exemples ci-dessous utilisent les types d’action à des fins de démonstration, vous pouvez appliquer les mêmes principes à toute fonction qui charge la bibliothèque de balises sur votre site.


Les méthodes suivantes sont couvertes :

- [Implémentation de bibliothèques tierces](#implementing-third-party-libraries)
   - [Conditions préalables   ](#prerequisites)
   - [Processus de chargement du code de base](#base-code-loading-process)
      - [Exemple de code de base](#base-code-example)
   - [Options de mise en oeuvre des balises](#tags-implementation-options)
      - [Chargement au moment de l’exécution à partir de l’hôte fournisseur {#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [Chargement au moment de l’exécution à partir de l’hôte de bibliothèque de balises](#load-at-runtime-from-the-tag-library-host)
      - [Incorporer directement la bibliothèque](#embed-the-library-directly)
   - [Étapes suivantes](#next-steps)

### Chargement au moment de l’exécution à partir de l’hôte fournisseur {#vendor-host}

La méthode la plus courante pour l’hébergement de la bibliothèque de fournisseur consiste à utiliser le CDN du fournisseur.  Comme le code de base pour la plupart des bibliothèques de fournisseur est déjà configuré pour charger la bibliothèque à partir du CDN du fournisseur, vous pouvez configurer votre extension pour charger la bibliothèque à partir du même emplacement.

Cette approche est généralement la plus facile à gérer, car toutes les mises à jour apportées au fichier sur le CDN seront automatiquement chargées par l’extension.

Quand vous utilisez cette méthode, il suffit de coller le code de base entier directement dans un type d’action comme celui-ci :

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Vous pouvez éventuellement prendre d’autres mesures pour refactoriser cette implémentation. Puisque les variables `scriptElement` et `firstScriptElement` sont maintenant incluses dans la fonction exportée, vous pouvez supprimer l’IIFE parce que ces variables ne risquent pas de devenir globales.

En outre, les balises fournissent plusieurs [modules principaux](./web/core.md) qui sont des utilitaires que toute extension peut utiliser. Plus précisément, le module `@adobe/reactor-load-script` charge un script à partir d’un emplacement distant en créant un élément de script et en l’ajoutant au document. En utilisant ce module pour le processus de chargement de script, vous pouvez refactoriser encore plus le code d’action :

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### Chargement au moment de l’exécution à partir de l’hôte de bibliothèque de balises

L’utilisation d’un CDN comme fournisseur pour l’hébergement d’une bibliothèque présente plusieurs risques : le CDN peut échouer, le fichier peut être mis à jour avec un bug critique à tout moment, ou le fichier peut être compromis à des fins malhonnêtes.

Pour résoudre ces problèmes, vous pouvez choisir d’inclure la bibliothèque du fournisseur en tant que fichier distinct au sein de votre extension. L’extension peut ensuite être configurée de sorte que le fichier soit hébergé avec la bibliothèque de balises principale. Au moment de l’exécution, l’extension charge la bibliothèque du fournisseur à partir du même serveur que celui qui a livré la bibliothèque principale au site web.

>[!IMPORTANT]
>
>Dans certains cas, la bibliothèque du fournisseur peut charger du code supplémentaire à partir de serveurs tiers, comme c’est le cas avec la bibliothèque du fournisseur Pinterest. Dans ce cas, le regroupement de la bibliothèque du fournisseur avec votre extension risque de ne pas répondre complètement à toutes les préoccupations concernant les risques.

Pour implémenter cette méthode, vous devez d’abord télécharger la bibliothèque du fournisseur sur votre ordinateur. Dans le cas de Pinterest, la bibliothèque du fournisseur se trouve à l’adresse [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js). Une fois le fichier téléchargé, vous devez le placer dans votre projet d’extension. Dans l’exemple ci-dessous, le fichier est nommé `pinterest.js` et se trouve dans un dossier `vendor` du répertoire de projet.

Une fois que le fichier de bibliothèque est dans votre projet, vous devez mettre à jour votre [manifeste d’extension](./manifest.md) (`extension.json`) pour indiquer que la bibliothèque du fournisseur doit être fournie avec la bibliothèque de balises principale. Pour ce faire, ajoutez le chemin d’accès au fichier de bibliothèque dans un tableau `hostedLibFiles` :

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

Enfin, vous devez configurer votre code d’action pour charger la bibliothèque du fournisseur à partir du même serveur que celui qui héberge la bibliothèque principale. L’exemple ci-dessous utilise le code d’action généré dans la [section précédente](#vendor-host) comme point de départ. Avec l’[objet turbine](./turbine.md), vous devez transmettre le nom de fichier (sans chemin d’accès) du fichier fournisseur comme suit :

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Il est important de noter que lorsque vous utilisez cette méthode, vous devez mettre à jour manuellement votre fichier fournisseur téléchargé chaque fois que la bibliothèque est mise à jour sur son réseau de diffusion de contenu et publier les modifications dans une nouvelle version de votre extension.

### Incorporer directement la bibliothèque

Vous pouvez éviter d’avoir à charger la bibliothèque du fournisseur entièrement en incorporant directement le code de bibliothèque dans le code d’action lui-même, ce qui en fait un élément de la bibliothèque de balises principale. L’utilisation de cette méthode augmente la taille de la bibliothèque principale, mais évite d’avoir à effectuer une requête HTTP supplémentaire pour récupérer un fichier distinct.

Avec le code d’action créé dans la [section précédente](#vendor-host) comme point de départ, vous pouvez remplacer la ligne où le script est chargé par le contenu du script lui-même :

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## Étapes suivantes

Ce document fournit un aperçu des différentes méthodes d’hébergement de bibliothèques tierces dans vos extensions de balises. Bien que les exemples présentés soient axés sur les bibliothèques, ces techniques s’appliquent à tout élément de code que votre extension peut utiliser.

Reportez-vous à la documentation associée à ce guide pour en savoir plus sur les outils de configuration de vos extensions, y compris les types d’action, le manifeste d’extension, les modules principaux et l’objet Turbine.
