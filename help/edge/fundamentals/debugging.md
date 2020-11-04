---
title: Débogage
seo-title: Débogage du SDK Web d’Adobe Experience Platform
description: Découvrez comment activer/désactiver le débogage du SDK Web d’Experience Platform
seo-description: Découvrez comment activer/désactiver le débogage du SDK Web d’Experience Platform
keywords: debugging web sdk;debugging;configure;configure command;debug command;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: f63c897dd1a8a8ad9ef7ac025bf05b22265ea95a
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 92%

---


# Débogage

Lorsque le débogage est activé, le SDK envoie des messages à la console du navigateur qui peuvent s’avérer utiles pour déboguer votre implémentation et comprendre le comportement du SDK. Le débogage permet également une validation synchrone du côté serveur des données collectées par rapport au schéma configuré.

Le débogage est désactivé par défaut, mais il est possible de l’activer de trois manières différentes :

* Commande `configure`
* Commande `setDebug`
* Paramètre de chaîne de requête

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

Lorsque le débogage est défini par le biais de la commande`debug` ou du paramètre de chaîne de requête, il remplace toute option `debug` définie dans la commande `configure`. Dans ces deux cas, le débogage reste également activé pendant la durée de la session. En d’autres termes, si vous activez le débogage à l’aide de la commande debug ou du paramètre de chaîne de requête, il reste activé jusqu’à :

* la fin de votre session ;
* l’exécution de la commande `debug` ;
* la nouvelle définition du paramètre de chaîne de requête.

## Récupération des informations sur la bibliothèque

Il est souvent utile d’accéder à certains détails de la bibliothèque que vous avez chargée sur votre site web. Pour cela, exécutez la commande `getLibraryInfo` de la manière suivante :

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Actuellement, l’objet `libraryInfo` fourni contient les propriétés suivantes :

* `version` Il s’agit de la version de la bibliothèque chargée. Par exemple, si la version de la bibliothèque chargée est 1.0.0, la valeur est `1.0.0`.
