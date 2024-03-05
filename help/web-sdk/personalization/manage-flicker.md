---
title: Gestion du scintillement pour les expériences personnalisées à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment utiliser le SDK Web de Adobe Experience Platform pour gérer le scintillement sur les expériences utilisateur.
keywords: target;scintillement;prehideStyle;asynchrone;asynchrone;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 53%

---

# Gestion du scintillement

Lorsque vous tentez d’effectuer le rendu du contenu de personnalisation, le SDK doit s’assurer qu’il n’y a pas de scintillement. Le scintillement, également appelé FOOC (Flash du contenu original), est lorsqu’un contenu original est brièvement affiché avant que l’alternative n’apparaisse pendant le test/la personnalisation. Le SDK tente d’appliquer des styles CSS aux éléments de la page afin de s’assurer qu’ils sont masqués jusqu’à ce que le contenu de personnalisation soit correctement rendu.

La gestion du scintillement dépend du déploiement synchrone ou asynchrone du SDK Web. Vérifiez les `<head>` balise où déployer `alloy.js` ou le chargeur de balises. La présence de la variable `async` dans la variable `<script>` détermine si le SDK Web se charge de manière asynchrone.

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## Gestion du scintillement pour les déploiements synchrones

La gestion synchrone des scintillements se divise en trois phases :

1. Prémasquage
1. Prétraitement
1. Rendu

Durant : **phase de prémasquage**, le SDK utilise la variable [`prehidingStyle`](../commands/configure/prehidingstyle.md) pour créer une balise de style de HTML et l’ajouter au modèle DOM afin de vous assurer que les sections souhaitées de la page sont masquées. Si vous ne savez pas quelles parties de la page seront personnalisées, il est recommandé de définir `prehidingStyle` sur `body { opacity: 0 !important }`. La page entière est ainsi masquée. Toutefois, cela a l’inconvénient d’entraîner des performances de rendu de page pires, signalées par des outils tels que Lighthouse, les tests de page web, etc. Pour optimiser les performances de rendu des pages, il est recommandé de définir `prehidingStyle` sur une liste d’éléments de conteneurs qui contiennent les parties de la page à personnaliser.

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

Une fois que le SDK a reçu du contenu personnalisé du serveur, la variable **phase de prétraitement** commence. Au cours de cette phase, la réponse est prétraitée, en veillant à ce que les éléments qui doivent contenir du contenu personnalisé soient masqués. Une fois ces éléments masqués, la balise de style HTML qui a été créée en fonction de l’option de configuration `prehidingStyle` est supprimée et le corps HTML ou les éléments masqués sont affichés.

Une fois que le contenu de personnalisation a été rendu avec succès, ou en cas d’erreur, la variable **phase de rendu** commence. Tous les éléments précédemment masqués s’affichent pour vous assurer qu’aucun élément masqué sur la page n’a été masqué par le SDK.

## Gestion du scintillement pour les déploiements asynchrones

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
