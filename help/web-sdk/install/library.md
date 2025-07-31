---
title: Installation de Web SDK à l’aide de la bibliothèque JavaScript
description: Référencez la bibliothèque Web SDK à l’aide d’un fichier CDN autonome.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Installation de Web SDK à l’aide de la bibliothèque JavaScript

Au lieu d’installer le SDK Web sans [utiliser l’extension de balise](extension.md), vous pouvez référencer la bibliothèque JavaScript hébergée sur un réseau CDN. Vous pouvez référencer la bibliothèque directement ou la télécharger et l’héberger sur votre propre infrastructure. Il est disponible dans des formats minimisés et complets.

La bibliothèque Web SDK est disponible en utilisant la structure d&#39;URL suivante :

* **Minifié** : `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Complet** : `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Voir les [notes de mise à jour](../release-notes.md) pour connaître la dernière version à inclure dans l’URL. Par exemple, l’URL de la version complète 2.19.1 de est `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

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

Ce code crée de manière asynchrone un objet `alloy` qui vous permet d’appeler n’importe quelle commande Web SDK. Si vous souhaitez charger le SDK Web de manière synchrone, vous pouvez supprimer l’attribut `async` dans la dernière ligne du bloc de code. La suppression de l’attribut `async` bloque l’analyse et le rendu du reste du document HTML par le navigateur jusqu’à ce que la bibliothèque soit chargée et exécutée. Ce délai supplémentaire avant d’afficher le contenu principal aux utilisateurs et utilisatrices est généralement découragé, mais il peut s’avérer logique selon les besoins de votre entreprise.
