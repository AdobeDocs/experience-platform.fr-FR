---
title: Débogage
seo-title: Débogage du SDK Web d’Adobe Experience Platform
description: Découvrez comment activer/désactiver le débogage du SDK Web Experience Platform
seo-description: Découvrez comment activer/désactiver le débogage du SDK Web Experience Platform
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Débogage

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Lorsque le débogage est activé, le SDK envoie des messages à la console du navigateur qui peuvent s’avérer utiles pour déboguer votre implémentation et comprendre le comportement du SDK. Le débogage génère également une validation synchrone côté serveur des données collectées par rapport au que vous avez configuré.

Le débogage est désactivé par défaut, mais il est possible de basculer de trois manières différentes :

* `configure` command
* `debug` command
* Paramètre de chaîne de 

## Basculement du débogage avec la commande Configurer

Lors de la configuration du SDK à l’aide de la `configure` commande, activez le débogage en définissant l’ `debugEnabled` option sur `true`.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>Cela active le débogage pour tous les utilisateurs de la page Web plutôt que pour votre navigateur personnel uniquement.

## Basculement du débogage avec la commande Débogage

Basculez le débogage avec une `debug` commande distincte comme suit :

```javascript
alloy("debug", {
  "enabled": true
});
```

Si vous préférez ne pas modifier le code de votre page Web ou ne souhaitez pas que les messages de journalisation soient produits pour tous les utilisateurs de votre site Web, ceci est particulièrement utile car vous pouvez exécuter la `debug` commande dans la console JavaScript de votre navigateur à tout moment.

## Basculement du débogage avec un paramètre de chaîne de 

Basculez le débogage en définissant un paramètre de chaîne de  `alloy_debug` sur `true` ou `false` comme suit :

```HTTP
http://example.com/?alloy_debug=true
```

Tout comme la `debug` commande, si vous préférez ne pas modifier le code de votre page Web ou ne souhaitez pas que les messages de journalisation soient générés pour tous les utilisateurs de votre site Web, ceci est particulièrement utile car vous pouvez définir le paramètre de chaîne de  du lors du chargement de la page Web dans votre navigateur.

## Priorité et durée

Lorsque le débogage est défini par le biais de la `debug` commande ou du paramètre de chaîne de , il remplace toute `debug` option définie dans la `configure` commande. Dans ces deux cas, le débogage reste basculé pendant la durée de la session. En d’autres termes, si vous activez le débogage à l’aide de la commande de débogage ou du paramètre de chaîne de , il reste activé jusqu’à ce que l’un des paramètres suivants soit :

* Fin de votre session
* Vous exécutez la `debug` commande
* Vous définissez à nouveau le paramètre de chaîne de 
