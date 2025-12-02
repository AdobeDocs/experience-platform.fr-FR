---
title: Gestion du scintillement pour les expériences personnalisées à l’aide de Adobe Experience Platform Web SDK
description: Découvrez comment utiliser Adobe Experience Platform Web SDK pour gérer le scintillement des expériences utilisateur.
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 54%

---

# Gestion du scintillement

Lorsque vous tentez d’effectuer le rendu du contenu de personnalisation, le SDK doit s’assurer qu’il n’y a pas de scintillement. Le scintillement, également appelé FOOC (Flash of Original Content), correspond au moment où un contenu original est brièvement affiché avant que l’alternative n’apparaisse lors du test/de la personnalisation. Le SDK tente d’appliquer des styles CSS aux éléments de la page afin de s’assurer qu’ils sont masqués jusqu’à ce que le contenu de personnalisation soit correctement rendu.

La gestion du scintillement dépend du déploiement du SDK Web de manière synchrone ou asynchrone. Vérifiez la balise `<head>` dans laquelle vous déployez `alloy.js` ou le chargeur de balises. La présence de l’attribut `async` dans la balise `<script>` détermine si le SDK Web se charge de manière asynchrone.

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

La gestion synchrone du scintillement est divisée en trois phases :

1. Prémasquage
1. Prétraitement
1. Rendu

Au cours de la **phase de pré-masquage**, le SDK utilise la propriété de configuration [`prehidingStyle`](../../js/commands/configure/prehidingstyle.md) pour créer une balise de style HTML et l’ajouter au DOM afin de s’assurer que les sections souhaitées de la page sont masquées. Si vous ne savez pas quelles parties de la page seront personnalisées, il est recommandé de définir `prehidingStyle` sur `body { opacity: 0 !important }`. La page entière est ainsi masquée. Cela a toutefois l’inconvénient d’entraîner une dégradation des performances de rendu des pages signalées par des outils tels que Lighthouse, les tests de page web, etc. Pour optimiser les performances de rendu des pages, il est recommandé de définir `prehidingStyle` sur une liste d’éléments de conteneurs qui contiennent les parties de la page à personnaliser.

Supposons que vous ayez une page HTML comme celle ci-dessous et que vous sachiez que seuls les éléments de conteneur `bar` et `bazz` seront jamais personnalisés :

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

Une fois que le SDK a reçu du contenu personnalisé du serveur, la **phase de prétraitement** commence. Au cours de cette phase, la réponse est prétraitée, en veillant à ce que les éléments qui doivent contenir du contenu personnalisé soient masqués. Une fois ces éléments masqués, la balise de style HTML qui a été créée en fonction de l’option de configuration `prehidingStyle` est supprimée et le corps HTML ou les éléments masqués sont affichés.

Une fois que tout le contenu de personnalisation a été rendu avec succès, ou en cas d’erreur, la **phase de rendu** commence. Tous les éléments précédemment masqués s’affichent pour vous assurer qu’aucun élément masqué de la page n’a été masqué par le SDK.

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
