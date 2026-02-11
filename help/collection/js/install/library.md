---
title: Installation de la bibliothèque JavaScript Web SDK
description: Référencez la bibliothèque Web SDK à l’aide d’un fichier CDN autonome.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Installation de la bibliothèque JavaScript Web SDK

Si vous choisissez de ne pas utiliser l’extension de balise [Web SDK](/help/tags/extensions/client/web-sdk/overview.md), vous pouvez installer le SDK Web en référençant la bibliothèque JavaScript autonome hébergée sur le réseau CDN d’Adobe. Vous pouvez référencer la bibliothèque directement ou la télécharger et l’héberger sur votre propre infrastructure. Il est disponible dans des formats minimisés et complets.

La bibliothèque Web SDK est disponible en utilisant la structure d&#39;URL suivante :

* **Minifié** : `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **Complet** : `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

Consultez les [notes de mise à jour de Web SDK](../release-notes.md) pour connaître la dernière version à inclure dans l’URL. Par exemple, l’URL de la version complète 2.19.1 de est `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Ajout du code de base et du chargeur de bibliothèque

Le code à ajouter se compose de deux sections :

* **Code de base** : autorise le démarrage en mettant les commandes en file d’attente pendant le chargement asynchrone du SDK Web. Voir [Code de base](base-code.md) pour plus d’informations. Adobe recommande d’utiliser le code de base lors du chargement asynchrone de la bibliothèque afin d’éviter des conditions de concurrence lors de l’appel des commandes Web SDK lors du chargement de la page.
* **Chargeur de bibliothèque** : charge l’intégralité de la bibliothèque JavaScript.

Ajoutez le bloc de code suivant aussi haut que possible dans la balise `<head>`, avant tout script pouvant appeler le SDK Web :

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

Si vous souhaitez charger le SDK Web de manière synchrone, vous pouvez supprimer l’attribut `async` lors du chargement de la bibliothèque. La suppression de l’attribut `async` bloque l’analyse d’HTML pendant que le navigateur récupère et exécute la bibliothèque. Ce délai supplémentaire avant d’afficher le contenu principal aux utilisateurs et utilisatrices est généralement découragé, mais il peut s’avérer logique selon les besoins de votre entreprise.
