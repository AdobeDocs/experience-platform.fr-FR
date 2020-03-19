---
title: Rendu du contenu personnalisé
seo-title: Adobe Experience Platform Web SDK Rendu du contenu personnalisé
description: Découvrez comment rendre du contenu personnalisé avec le SDK Web de la plateforme d’expérience
seo-description: Découvrez comment rendre du contenu personnalisé avec le SDK Web de la plateforme d’expérience
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Rendu du contenu personnalisé

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Le SDK effectue automatiquement le rendu du contenu personnalisé lorsque vous envoyez un au serveur et que vous le définissez `viewStart` comme `true` option sur le  du.

```javascript
alloy("event", {
  "viewStart": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Le rendu d’un contenu personnalisé est asynchrone. Il ne doit donc pas y avoir d’hypothèse sur le moment où un élément de contenu particulier fait partie de la page.

## Gestion du scintillement

Lorsque vous tentez de rendre le contenu de personnalisation, le SDK doit s’assurer qu’il n’y a pas de scintillement. Flicker, également appelé FOOC (Flash du contenu original), est lorsqu’un contenu original est brièvement affiché avant que l’alternative n’apparaisse pendant le test ou la personnalisation. Le kit SDK tente d’appliquer des styles CSS aux éléments de la page afin de s’assurer que ces éléments sont masqués jusqu’à ce que le contenu de personnalisation soit rendu correctement.

La fonctionnalité de gestion des scintillements comporte quelques phases :

1. Prévisualisation
1. Prétraitement
1. Rendu

### Prévisualisation

Au cours de la phase de prémasquage, le kit SDK utilise l’option `prehidingStyle` de configuration pour créer une balise de style HTML et l’ajouter au modèle DOM afin de s’assurer que de grandes portions de la page sont masquées. Si vous ne savez pas quelles portions de la page seront personnalisées, il est recommandé de les définir `prehidingStyle` sur `body { opacity: 0 !important }`. Cela permet de s’assurer que la page entière est masquée. Cela a toutefois l&#39;inconvénient de réduire les performances de rendu des pages signalées par des outils tels que Lighthouse, les tests de page Web, etc. Pour optimiser les performances de rendu de la page, il est recommandé de définir `prehidingStyle` sur un d’éléments  qui contiennent les parties de la page qui seront personnalisées.

En supposant que vous ayez une page HTML comme celle ci-dessous et que vous sachiez que seuls `bar` et `bazz` les éléments  seront jamais personnalisés :

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

Alors le `prehidingStyle` problème devrait être réglé sur quelque chose comme `#bar, #bazz { opacity: 0 !important }`.

### Prétraitement

La phase de prétraitement commence une fois que le SDK a reçu le contenu personnalisé du serveur. Au cours de cette phase, la réponse est prétraitée, en veillant à ce que les éléments qui doivent contenir du contenu personnalisé soient masqués. Une fois ces éléments masqués, la balise de style HTML qui a été créée en fonction de l’option `prehidingStyle` de configuration est supprimée et le corps HTML ou les éléments  masqués sont affichés.

### Rendu

Une fois que tout le contenu de la personnalisation a été rendu correctement, ou en cas d’erreur, tous les éléments précédemment masqués s’affichent pour vous assurer qu’il n’y a aucun élément masqué sur la page qui a été masqué par le SDK.

## Gestion du scintillement lorsque le SDK est chargé de manière asynchrone

Il est recommandé de toujours charger le SDK de manière asynchrone afin d’obtenir les meilleures performances de rendu de page. Cela a toutefois des implications pour le rendu du contenu personnalisé. Lorsque le SDK est chargé de manière asynchrone, il est nécessaire d’utiliser le fragment de code prémasqué. Le fragment de code prémasqué doit être ajouté avant le kit SDK dans la page HTML. Voici un exemple de fragment de code qui masque tout le corps :

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Pour s’assurer que le corps HTML ou les éléments  du ne sont pas masqués pendant une longue période, le fragment de code prémasqué utilise un minuteur qui, par défaut, supprime le fragment de code après `3000` des millisecondes. Les `3000` millisecondes représentent le temps d’attente maximal. Si la réponse du serveur a été reçue et traitée plus tôt, la balise de style HTML prémasquée est supprimée dès que possible.
