---
title: Gestion du scintillement pour les expériences personnalisées à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment utiliser le SDK Web de Adobe Experience Platform pour gérer le scintillement sur les expériences utilisateur.
keywords: target;scintillement;prehideStyle;asynchrone;asynchrone;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 76%

---

# Gestion du scintillement

Lorsque vous tentez d’effectuer le rendu du contenu de personnalisation, le SDK doit s’assurer qu’il n’y a pas de scintillement. Le scintillement, également appelé FOOC (Flash du contenu original), est lorsqu’un contenu original est brièvement affiché avant que l’alternative n’apparaisse pendant le test/la personnalisation. Le SDK tente d’appliquer des styles CSS aux éléments de la page afin de s’assurer qu’ils sont masqués jusqu’à ce que le contenu de personnalisation soit correctement rendu.

La fonctionnalité de gestion des scintillements comporte quelques phases :

1. Prémasquage
1. Prétraitement
1. Rendu

## Prémasquage

Au cours de la phase de prémasquage, le SDK utilise l’option de configuration `prehidingStyle` pour créer une balise de style HTML et l’ajouter au modèle DOM afin de s’assurer que de grandes parties de la page sont masquées. Si vous ne savez pas quelles parties de la page seront personnalisées, il est recommandé de définir `prehidingStyle` sur `body { opacity: 0 !important }`. La page entière est ainsi masquée. Toutefois, cela a l’inconvénient d’entraîner des performances de rendu de page pires, signalées par des outils tels que Lighthouse, les tests de page web, etc. Pour optimiser les performances de rendu des pages, il est recommandé de définir `prehidingStyle` sur une liste d’éléments de conteneurs qui contiennent les parties de la page à personnaliser.

En supposant que vous ayez une page de HTML comme celle ci-dessous et que vous sachiez que seulement `bar` et `bazz` les éléments de conteneur seront toujours personnalisés :

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

Alors `prehidingStyle` doit être défini sur `#bar, #bazz { opacity: 0 !important }`.

## Prétraitement

La phase de prétraitement démarre une fois que le SDK a reçu le contenu personnalisé du serveur. Au cours de cette phase, la réponse est prétraitée, en veillant à ce que les éléments qui doivent contenir du contenu personnalisé soient masqués. Une fois ces éléments masqués, la balise de style HTML qui a été créée en fonction de l’option de configuration `prehidingStyle` est supprimée et le corps HTML ou les éléments masqués sont affichés.

## Rendu

Une fois que l’intégralité du contenu de personnalisation a été correctement rendue, ou en cas d’erreur, tous les éléments précédemment masqués s’affichent pour qu’aucun élément masqué par le SDK ne le reste sur la page.

## Gestion du scintillement lorsque le SDK est chargé de manière asynchrone

Il est recommandé de toujours charger le SDK de manière asynchrone afin d’obtenir les meilleures performances de rendu de page. Cela a toutefois des conséquences pour le rendu du contenu personnalisé. Lorsque le SDK est chargé de manière asynchrone, il est nécessaire d’utiliser l’extrait de code de prémasquage. L’extrait de code de prémasquage doit être ajouté avant le SDK dans la page HTML. Voici un exemple d’extrait de code qui masque tout le corps :

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Pour s’assurer que le corps HTML ou les éléments de conteneur ne sont pas masqués pendant une longue période, l’extrait de code de prémasquage utilise un minuteur qui, par défaut, supprime l’extrait de code après `3000` millisecondes. Les `3000` millisecondes représentent le temps d’attente maximal. Si la réponse du serveur a été reçue et traitée plus tôt, la balise de style HTML de prémasquage est supprimée dès que possible.
