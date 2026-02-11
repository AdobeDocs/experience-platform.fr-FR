---
title: Code de base
description: Mettre les commandes en file d’attente (amorçage) pendant le chargement asynchrone de la bibliothèque de collecte de données.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Code de base

Le code de base permet le démarrage en mettant les commandes en file d’attente pendant le chargement asynchrone du Adobe Experience Platform Web SDK. Une fois le code de base exécuté, vous pouvez appeler immédiatement n’importe quelle commande telle que [`configure`](../commands/configure/overview.md) ou [`sendEvent`](../commands/sendevent/overview.md) sans vous soucier des conditions de concurrence ou du timing de la bibliothèque une fois le chargement terminé. Lorsque le chargement du SDK Web se termine, les commandes placées en file d’attente s’exécutent dans l’ordre « premier entré, premier sorti » (ordre dans lequel elles étaient placées en file d’attente).

Les commandes renvoient des promesses, même lorsqu’elles sont placées en file d’attente. Si une commande est mise en file d’attente, la promesse est résolue ou refusée une fois la commande exécutée lorsque le chargement du SDK Web se termine. Si le chargement du SDK Web n’est jamais terminé (par exemple, le chargement de la bibliothèque échoue), les promesses en file d’attente restent en attente.

## Ajouter le code de base

Placez le code de base aussi haut que possible dans la balise `<head>`, avant tout script pouvant appeler le SDK Web.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Après avoir ajouté le code de base, chargez le SDK Web à l’aide de la méthode choisie ([chargeur de bibliothèque JavaScript](library.md) ou [code intégré de balises](/help/tags/extensions/client/web-sdk/getting-started.md)). Pour les implémentations basées sur des balises, le code de base est pris en charge dans l’extension de balise Web SDK 2.34.0 et les versions ultérieures.

Ce code de base n’est **pas** requis dans les scénarios suivants :

* Si vous chargez la bibliothèque JavaScript de manière synchrone. Le chargement synchrone bloque l’analyse pendant la récupération et l’exécution de la bibliothèque.
* Si vous utilisez l’extension de balise, tous les appels au SDK Web sont effectués dans les règles ou actions de balise. Il vous suffit d’inclure le code de base si votre implémentation fait référence au Web SDK en dehors de votre bibliothèque de balises. La plupart des implémentations de balises n’appellent généralement pas Web SDK en dehors de la bibliothèque de balises. Par conséquent, la plupart des implémentations de balises ne nécessitent pas le code de base.

## Exemples

Voir les commentaires dans cet exemple de code pour comprendre la durée de mise en file d’attente et de résolution des commandes. Cet exemple s’applique à la fois à la bibliothèque JavaScript et à l’extension de balise :

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## Renommer l’instance SDK

Vous pouvez renommer la fonction globale appelée en modifiant la dernière ligne du code de base. Modification :

```js
(window,["alloy"]);
```

A :

```js
(window,["ingot"]);
```

Cette modification vous permet d’appeler des commandes à l’aide de `ingot` au lieu de `alloy` :

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## Plusieurs instances SDK

Vous pouvez éventuellement utiliser le code de base pour configurer plusieurs instances SDK sur une page. Pour plus d’informations[&#x200B; voir &#x200B;](../../use-cases/multiple-instances.md) Utilisation de plusieurs instances Web SDK .
