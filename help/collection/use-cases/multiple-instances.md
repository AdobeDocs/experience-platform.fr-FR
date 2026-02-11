---
title: Utilisation de plusieurs instances Web SDK
description: Découvrez comment interagir avec plusieurs propriétés Experience Platform Web SDK.
keywords: plusieurs propriétés
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 23%

---

# Utilisation de plusieurs instances Web SDK

Dans certains cas, il est possible que vous souhaitiez interagir avec deux propriétés différentes sur une même page. Les scénarios possibles sont les suivants :

* Des entreprises acquises et travaillant à l’intégration de leurs sites web respectifs.
* Des relations de partage de données entre plusieurs entreprises.
* Les clients qui testent de nouvelles solutions Adobe et qui ne souhaitent pas interrompre leur implémentation existante

Le SDK vous permet de créer une instance distincte pour chaque propriété en ajoutant un autre nom au tableau dans le [code de base](../js/install/base-code.md). L’exemple suivant fournit deux noms, `titanium` et `copper`.

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

Par conséquent, le script crée deux fonctions globales (`titanium` et `copper` dans l’exemple ci-dessus) qui deviennent deux instances SDK lors de l’initialisation de la bibliothèque. Chaque instance conserve sa propre configuration et son propre état ; toute commande qui utilise `titanium` est isolée des `copper`.

>[!TIP]
>
>Si vous utilisez le code de base avec des balises, assurez-vous que tous les noms d’instance définis correspondent à tous les [noms d’instance SDK](/help/tags/extensions/client/web-sdk/configure/general.md) lors de la configuration de l’extension de balise.

En suivant l’exemple de modèle de dénomination de `titanium` et `copper` en tant qu’instances Web SDK, vous pouvez exécuter des commandes indépendamment :

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

Veillez à exécuter la commande [`configure`](../js/commands/configure/overview.md) pour chaque instance avant d’exécuter d’autres commandes sur la même instance.

>[!IMPORTANT]
>
>Pour éviter les conflits avec les cookies, chaque instance de Web SDK doit avoir son propre `datastreamId` unique et son propre `orgId` unique.
