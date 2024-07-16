---
title: Installation du SDK Web à l’aide de la bibliothèque JavaScript
description: Référencez la bibliothèque SDK Web à l’aide d’un fichier CDN autonome.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Installation du SDK Web à l’aide de la bibliothèque JavaScript

Au lieu d’installer le SDK Web sans [ utiliser l’extension de balise ](extension.md), vous pouvez référencer la bibliothèque JavaScript hébergée sur un CDN. Vous pouvez référencer la bibliothèque directement ou la télécharger et l’héberger sur votre propre infrastructure. Il est disponible dans des formats réduits et complets.

La bibliothèque SDK Web est disponible à l’aide de la structure d’URL suivante :

* **Minifié** : `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Full** : `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Voir les [ notes de mise à jour](../release-notes.md) pour connaître la dernière version à inclure dans l’URL. Par exemple, l’URL de la version complète de 2.19.1 est `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Ajout du code

Ajoutez le bloc de code suivant aussi haut que possible dans la balise `<head>` de votre HTML :

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Ce code crée de manière asynchrone un objet `alloy` qui vous permet d’appeler n’importe quelle commande de SDK Web. Si vous souhaitez charger le SDK Web de manière synchrone, vous pouvez supprimer l’attribut `async` dans la dernière ligne du bloc de code. La suppression de l’attribut `async` empêche le reste du document HTML d’être analysé et rendu par le navigateur jusqu’à ce que la bibliothèque soit chargée et exécutée. Ce délai supplémentaire avant l’affichage du contenu principal aux utilisateurs est généralement déconseillé, mais peut s’avérer pertinent en fonction des besoins de votre entreprise.
