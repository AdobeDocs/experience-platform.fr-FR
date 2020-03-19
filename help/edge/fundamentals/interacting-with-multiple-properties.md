---
title: Interaction avec plusieurs propriétés
seo-title: Adobe Experience Platform Web SDK Interaction avec plusieurs propriétés
description: Découvrez comment interagir avec plusieurs propriétés du SDK Web de plateforme d’expérience
seo-description: Découvrez comment interagir avec plusieurs propriétés du SDK Web de plateforme d’expérience
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Interaction avec plusieurs propriétés

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Il peut arriver que vous souhaitiez interagir avec deux propriétés différentes sur la même page. Notamment : 

*  acquis et travaillant à l&#39;intégration de leurs sites Web
* Relations de partage de données entre plusieurs 
* Clients qui testent de nouvelles solutions Adobe et qui ne souhaitent pas perturber leur implémentation existante

Le SDK vous permet de créer une instance distincte pour chaque propriété en ajoutant un autre nom au tableau dans le code de base. Dans l&#39;exemple suivant, nous avons fourni deux noms, `mycustomname1` et `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Par conséquent, le script crée deux instances du SDK. La fonction globale permettant d’interagir avec la première instance est nommée `mycustomname1` et la fonction globale permettant d’interagir avec la seconde instance est nommée `mycustomname2`.

En créant deux instances distinctes, chacune peut être configurée pour une propriété différente. Toute communication ou persistance de données résultant d’une interaction avec `mycustomname1` est isolée de `mycustomname2` et inversement.

En suivant l’exemple ci-dessus, vous pouvez exécuter des commandes à l’aide de chacune des instances, comme suit :

```javascript
mycustomname1("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("event", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "configId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("event", {
  "data": {
    "key": "value"
  }
});
```

Veillez à exécuter la `configure` commande pour chaque instance avant d’exécuter d’autres commandes sur la même instance.

## Limites

Pour éviter tout conflit avec les cookies, une seule instance du SDK Web d’Adobe Experience Platform dans une page peut avoir une instance particulière `configId`.  De même, une seule instance du SDK Web d’Adobe Experience Platform peut avoir une instance particulière `orgId`.
