---
title: Interaction avec plusieurs propriétés dans le SDK Web Adobe Experience Platform
description: Découvrez comment interagir avec plusieurs propriétés du SDK Web d’Adobe Experience Platform.
keywords: plusieurs propriétés ; configure;sendEvent;edgeConfigId;orgId ;
translation-type: tm+mt
source-git-commit: b865b7fb940ca2d5f8b44f71eb58e62e3473f52d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 68%

---


# Interaction avec plusieurs propriétés

Dans certains cas, il est possible que vous souhaitiez interagir avec deux propriétés différentes sur une même page. Ces cas comprennent :

* Des entreprises acquises et travaillant à l’intégration de leurs sites web respectifs.
* Des relations de partage de données entre plusieurs entreprises.
* Des clients qui testent de nouvelles solutions Adobe et qui ne souhaitent pas perturber leur implémentation existante.

Le SDK permet de créer une instance distincte pour chaque propriété en ajoutant un autre nom au tableau dans le code de base. L&#39;exemple suivant fournit deux noms, `mycustomname1` et `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Par conséquent, le script crée deux instances du SDK. La fonction globale permettant d’interagir avec la première instance est appelée `mycustomname1` et celle permettant d’interagir avec la seconde instance est appelée `mycustomname2`.

En créant deux instances distinctes, chacune peut être configurée pour une propriété différente. Toute communication ou persistance des données qui survient en raison d&#39;une interaction avec `mycustomname1` est isolée de `mycustomname2`.

En suivant l’exemple ci-dessus, vous pouvez exécuter comme suit des commandes à l’aide de chacune des instances :

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Veillez à exécuter la commande `configure` pour chaque instance avant d’exécuter d’autres commandes sur la même instance.

## Limites

Pour éviter les conflits avec les cookies, une seule instance de Adobe Experience Platform [!DNL Web SDK] dans une page peut avoir un `edgeConfigId` particulier. De même, une seule instance de Adobe Experience Platform [!DNL Web SDK] peut avoir un `orgId` particulier.
