---
title: Installation du SDK Web d’Adobe Experience Platform
seo-title: SDK Web Adobe Experience Platform installation du SDK
description: Découvrez comment installer le SDK Web de la plateforme d’expérience
seo-description: Découvrez comment installer le SDK Web de la plateforme d’expérience
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Installation du SDK

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

La première étape de la mise en oeuvre du SDK Web d’Adobe Experience Platform consiste à copier et coller le &quot;code de base&quot; suivant le plus haut possible dans la balise `<head>` de votre code HTML :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js" async></script>
```

Le code de base crée une fonction globale nommée `alloy`. Utilisez cette fonction pour interagir avec le SDK. Si vous souhaitez nommer la fonction globale quelque chose d’autre, vous pouvez modifier le `alloy` nom comme suit :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="alloy.js" async></script>
```

Dans cet exemple, la fonction globale est renommée `mycustomname`, au lieu de `alloy`.

>[!IMPORTANT]
>Pour éviter des problèmes potentiels, utilisez un nom contenant au moins un caractère qui n’est pas un chiffre et qui n’entre pas en conflit avec le nom d’une propriété déjà trouvée sur `window`.

Ce code de base, en plus de créer une fonction globale, charge également le code supplémentaire contenu dans un fichier externe \(`alloy.js`\) hébergé sur un serveur. Par défaut, ce code est chargé de manière asynchrone pour permettre à votre page Web d’être aussi performante que possible. Il s’agit de l’implémentation recommandée.

## Prise en charge d’Internet Explorer

Ce SDK utilise des promesses, qui est une méthode de communication de l’achèvement des  asynchrones. L’implémentation [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilisée par le kit SDK est prise en charge en mode natif par tous les navigateurs de, à l’exception d’Internet Explorer. Pour utiliser le kit SDK dans Internet Explorer, vous devez disposer d’un `window.Promise` polyremplissage [](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Pour déterminer si vous avez déjà `window.Promise` des polyplaties :

1. Ouvrez votre site Web dans Internet Explorer.
1. Ouvrez la console de débogage du navigateur.
1. Entrez `window.Promise` dans la console, puis appuyez sur Entrée.

Si quelque chose d’autre que `undefined` apparaît, vous avez probablement déjà été polychargé `window.Promise`. Une autre façon de déterminer si `window.Promise` est polyrempli consiste à charger votre site Web après avoir suivi les instructions d’installation ci-dessus. Si le SDK renvoie une erreur en mentionnant quelque chose à propos d’une promesse, il est probable que vous n’ayez pas été polychargé `window.Promise`.

Si vous avez déterminé que vous devez polyremplir `window.Promise`, incluez la balise de script suivante au-dessus du code de base fourni précédemment :

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Ceci charge un script qui s’assure qu’ `window.Promise` il s’agit d’une implémentation Promise valide.

## Chargement synchrone du fichier JavaScript

Comme expliqué précédemment, le code de base que vous avez copié et collé dans le code HTML de votre site Web charge un fichier externe avec du code supplémentaire. Ce code supplémentaire contient les fonctionnalités de base du SDK. Toute commande que vous tentez d’exécuter pendant le chargement de ce fichier est mise en file d’attente, puis traitée une fois le fichier chargé. Il s’agit de la méthode d’installation la plus performante.

Dans certaines circonstances, toutefois, vous pouvez vouloir charger le fichier de manière synchrone \(d&#39;autres informations sur ces circonstances seront documentées ultérieurement\). Cela empêche le reste du HTML d’être analysé et rendu par le navigateur jusqu’à ce que le fichier externe ait été chargé et exécuté. Ce délai supplémentaire avant l’affichage du contenu principal pour les utilisateurs est généralement déconseillé, mais peut être pertinent en fonction des circonstances.

Pour charger le fichier de manière synchrone au lieu de manière asynchrone, supprimez l’ `async` attribut de la deuxième `script` balise, comme illustré ci-dessous :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js"></script>
```
