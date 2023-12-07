---
title: Débogage dans le SDK Web de Adobe Experience Platform
description: Découvrez comment activer/désactiver les fonctionnalités de débogage dans le SDK Web Experience Platform.
keywords: débogage du sdk web;débogage;configurer;commande de configuration;commande de débogage;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 50%

---

# Débogage

Lorsque le débogage est activé, le SDK envoie des messages à la console du navigateur qui peuvent s’avérer utiles pour déboguer votre mise en oeuvre et comprendre le comportement du SDK.

Le débogage est désactivé par défaut, mais peut être activé de quatre manières différentes :

* Commande `configure`
* Commande `setDebug`
* Paramètre de chaîne de requête
* Activation/désactivation du débogage dans Adobe Experience Platform Debugger. Adobe Experience Platform est un outil puissant qui examine vos pages web et vous aide à déboguer les problèmes d’implémentation avec vos produits Experience Cloud. Adobe Experience Platform Debugger est disponible sous la forme d’un [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) extension . Le débogage peut être activé à partir de l’onglet de configuration de la section SDK Web AEP.

![Image de l’interface utilisateur du débogueur Experience Platform affichant l’écran de configuration.](../assets/enable-debugging.png)

## Activation/désactivation du débogage avec la commande Configure

Lors de la configuration du SDK à l’aide de la commande `configure`, activez le débogage en définissant l’option `debugEnabled` sur `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Le débogage est ainsi activé pour tous les utilisateurs de la page web plutôt que pour votre navigateur personnel uniquement.

## Activation/désactivation du débogage avec la commande Debug

Activez/désactivez le débogage avec une commande `debug` distincte de la manière suivante :

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Si vous préférez ne pas modifier le code de votre page web ou ne souhaitez pas que les messages de journalisation soient générés pour tous les utilisateurs de votre site web, cette méthode est particulièrement utile, car vous pouvez exécuter la commande `debug` dans la console JavaScript de votre navigateur à tout moment.

## Activation/désactivation du débogage avec un paramètre de chaîne de requête

Activez/désactivez le débogage en définissant un paramètre de chaîne de requête `alloy_debug` sur `true` ou `false` de la manière suivante :

```HTTP
http://example.com/?alloy_debug=true
```

Tout comme la commande `debug`, si vous préférez ne pas modifier le code de votre page web ou ne souhaitez pas que les messages de journalisation soient générés pour tous les utilisateurs de votre site Web, cette méthode est particulièrement utile, car vous pouvez définir le paramètre de chaîne lors du chargement de la page web dans votre navigateur.

## Priorité et durée

Lorsque le débogage est défini par le biais de la commande`debug` ou du paramètre de chaîne de requête, il remplace toute option `debug` définie dans la commande `configure`. Dans ces deux cas, le débogage reste activé pendant la durée de la session. En d’autres termes, si vous activez le débogage à l’aide de la commande debug ou du paramètre de chaîne de requête, il reste activé jusqu’à :

* la fin de votre session ;
* l’exécution de la commande `debug` ;
* la nouvelle définition du paramètre de chaîne de requête.

## Récupération des informations sur la bibliothèque

Il est souvent utile d’accéder à certains détails de la bibliothèque que vous avez chargée sur votre site web. Pour cela, exécutez la commande `getLibraryInfo` de la manière suivante :

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

Actuellement, l’objet `libraryInfo` fourni contient les propriétés suivantes :

* `version`: il s’agit de la version de la bibliothèque chargée. Par exemple, si la version de la bibliothèque chargée était 1.0.0, la valeur serait `1.0.0`. Lorsque la bibliothèque est exécutée dans l’extension de balise (appelée &quot;SDK Web AEP&quot;), la version est la version de la bibliothèque et la version de l’extension de balise associée à un signe &quot;+&quot;. Par exemple, si la version de la bibliothèque est 1.0.0 et que la version de l’extension de balise est 1.2.0, la valeur sera `1.0.0+1.2.0`.
* `commands`: il s’agit de toutes les commandes disponibles prises en charge par la bibliothèque chargée.
* `configs`: il s’agit de toutes les configurations actuelles de la bibliothèque chargée.
