---
title: Débogage
seo-title: Débogage du SDK Web d’Adobe Experience Platform
description: Découvrez comment activer/désactiver le débogage du SDK Web d’Experience Platform
seo-description: Découvrez comment activer/désactiver le débogage du SDK Web d’Experience Platform
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 100%

---


# Débogage

Lorsque le débogage est activé, le SDK envoie des messages à la console du navigateur qui peuvent s’avérer utiles pour déboguer votre implémentation et comprendre le comportement du SDK. Le débogage permet également une validation synchrone du côté serveur des données collectées par rapport au schéma configuré.

Le débogage est désactivé par défaut, mais peut être activé de trois manières différentes :

* Commande `configure`
* Commande `debug`
* Paramètre de chaîne de requête

## Activation/désactivation du débogage avec la commande Configure

Lors de la configuration du SDK à l’aide de la commande `configure`, activez le débogage en définissant l’option `debugEnabled` sur `true`.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>Le débogage est ainsi activé pour tous les utilisateurs de la page web plutôt que pour votre navigateur personnel uniquement.

## Activation/désactivation du débogage avec la commande Debug

Activez/désactivez le débogage avec une commande `debug` distincte de la manière suivante :

```javascript
alloy("debug", {
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

Lorsque le débogage est défini par le biais de la commande`debug` ou du paramètre de chaîne de requête, il remplace toute option `debug` définie dans la commande `configure`. Dans ces deux cas, le débogage reste activé/désactivé pendant la durée de la session. En d’autres termes, si vous activez le débogage à l’aide de la commande debug ou du paramètre de chaîne de requête, il reste activé jusqu’à :

* la fin de votre session ;
* l’exécution de la commande `debug` ;
* la nouvelle définition du paramètre de chaîne de requête.
