---
title: Utilisation de plusieurs instances de SDK Web
description: Découvrez comment interagir avec plusieurs propriétés du SDK Web Experience Platform.
keywords: plusieurs propriétés;configurer;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 63%

---

# Utilisation de plusieurs instances de SDK Web

Dans certains cas, il est possible que vous souhaitiez interagir avec deux propriétés différentes sur une même page. Ces cas incluent :

* Des entreprises acquises et travaillant à l’intégration de leurs sites web respectifs.
* Des relations de partage de données entre plusieurs entreprises.
* Des clients qui testent de nouvelles solutions Adobe et qui ne souhaitent pas perturber leur implémentation existante.

Le SDK permet de créer une instance distincte pour chaque propriété en ajoutant un autre nom au tableau dans le code de base. L’exemple suivant fournit deux noms : `titanium` et `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Par conséquent, le script crée deux instances du SDK. La fonction globale permettant d’interagir avec la première instance est appelée `titanium` et celle permettant d’interagir avec la seconde instance est appelée `copper`.

En créant deux instances distinctes, chacune peut être configurée pour une propriété différente. Toute communication ou persistance des données résultant d’une interaction avec `titanium` est isolé de `copper`.

En suivant l’exemple ci-dessus, vous pouvez exécuter des commandes à l’aide de chaque instance :

```javascript
titanium("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  "data": {
    "key": "value"
  }
});

copper("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Veillez à exécuter la commande `configure` pour chaque instance avant d’exécuter d’autres commandes sur la même instance.

>[!IMPORTANT]
>
>Pour éviter tout conflit avec les cookies, chaque instance du SDK Web doit avoir sa propre `edgeConfigId` et son propre `orgId`.
