---
title: Installation du SDK Web d’Adobe Experience Platform
seo-title: Installation du SDK Web d’Adobe Experience Platform
description: Découvrez la procédure d’installation du SDK Web d’Experience Platform
seo-description: Découvrez la procédure d’installation du SDK Web d’Experience Platform
translation-type: tm+mt
source-git-commit: 12cbcc26956cba2e14d64734c9210fa79bcc70b9
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 66%

---


# Installation du SDK {#installing-the-sdk}

La méthode privilégiée pour utiliser le SDK Web de Adobe Experience Platform est le [lancement](http://launch.adobe.com/). Recherchez l&#39;extension `AEP Web SDK` dans le catalogue d&#39;extensions, installez-la, puis configurez-la.

Le SDK Web AEP est également disponible sur un CDN que vous pouvez utiliser. Vous pouvez référencer ce fichier ou le télécharger et l’héberger sur votre propre infrastructure. Il est disponible dans une version réduite et non réduite. La version non réduite est utile pour le débogage.

Structure d’URL : https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OU alliage.js pour la version non réduite.

Par exemple :

* Minifié : [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js)
* Non minifié : [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js)

## ajouter le code {#adding-the-code}

The first step in implementing the Adobe Experience Platform [!DNL Web SDK] is to copy and paste the following &quot;base code&quot; as high as possible in the `<head>` tag of your HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Le code de base crée une fonction globale appelée `alloy`. Utilisez cette fonction pour interagir avec le SDK. Si vous souhaitez appeler autrement la fonction globale, vous pouvez modifier le nom `alloy` de la manière suivante :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Dans cet exemple, la fonction globale est renommée `mycustomname`, au lieu de `alloy`.

>[!IMPORTANT]
>Pour éviter des problèmes potentiels, utilisez un nom contenant au moins un caractère qui n’est pas un chiffre et qui n’entre pas en conflit avec le nom d’une propriété existant déjà sur `window`.

Ce code de base, en plus de créer une fonction globale, charge également le code supplémentaire contenu dans un fichier externe \(`alloy.js`\) hébergé sur un serveur. Par défaut, ce code est chargé de manière asynchrone pour permettre à votre page web d’être aussi performante que possible. Il s’agit de l’implémentation recommandée.

## Prise en charge d’Internet Explorer {#support-internet-explore}

Ce SDK utilise des promesses, ce qui est une méthode de communication de l’achèvement des tâches asynchrones. The [Promise](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) implementation used by the SDK is natively supported by all target browsers except [!DNL Internet Explorer]. To use the SDK on [!DNL Internet Explorer], you need to have `window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Pour déterminer si `window.Promise` est déjà polyfillé :

1. Open your website in [!DNL Internet Explorer].
1. Ouvrez la console de débogage du navigateur.
1. Saisissez `window.Promise` dans la console, puis appuyez sur Entrée.

Si autre chose que `undefined` s’affiche, `window.Promise` est déjà polyfillé. Une autre façon de déterminer si `window.Promise` est polyfillé consiste à charger votre site web après avoir suivi les instructions d’installation ci-dessus. Si le SDK renvoie une erreur à propos d’une promesse, il est probable que `window.Promise` n’ait pas été polyfillé.

Si vous avez déterminé que vous devez polyfiller `window.Promise`, incluez la balise de script suivante au-dessus du code de base fourni précédemment :

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Cela charge un script qui s’assure que `window.Promise` est une implémentation de promesse valide.

>[!NOTE]
>
>Si vous choisissez de charger une autre implémentation Promise, veillez à ce qu’elle prenne en charge `Promise.prototype.finally`.

## Chargement synchrone du fichier JavaScript {#loading-javascript-synchronously}

As explained in the section [Adding the code](#adding-the-code), the base code you have copied and pasted into your website&#39;s HTML loads an external file with additional code. Ce code supplémentaire contient les fonctionnalités de base du SDK. Toute commande que vous tentez d’exécuter pendant le chargement de ce fichier est mise en file d’attente, puis traitée une fois le fichier chargé. Cette méthode d’installation est la plus performante.

Dans certaines circonstances, toutefois, vous pouvez vouloir charger le fichier de manière synchrone \(des informations supplémentaires sur ces circonstances seront documentées ultérieurement\). Cela empêche le reste du HTML d’être analysé et rendu par le navigateur jusqu’à ce que le fichier externe ait été chargé et exécuté. Ce délai supplémentaire avant l’affichage du contenu principal pour les utilisateurs est généralement déconseillé, mais peut être pertinent en fonction des circonstances.

Pour charger le fichier de manière synchrone plutôt qu’asynchrone, supprimez l’attribut `async` de la deuxième balise `script`, comme illustré ci-dessous :

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js"></script>
```
