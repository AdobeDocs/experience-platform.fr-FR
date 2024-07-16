---
title: Méthodes de débogage
description: Découvrez comment activer/désactiver les fonctionnalités de débogage dans le SDK Web.
keywords: débogage du sdk web;débogage;configurer;commande de configuration;commande de débogage;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Méthodes de débogage

Lorsque le débogage est activé, le SDK Web envoie des messages à la console du navigateur qui peuvent s’avérer utiles pour déboguer votre implémentation. Le débogage est utile lorsque vous souhaitez comprendre le comportement du SDK en fonction des règles et des éléments de données que vous avez définis.

Le débogage est désactivé par défaut, mais peut être activé de quatre manières différentes. Vous pouvez utiliser n’importe quelle combinaison de ces méthodes pour activer ou désactiver le débogage qui convient le mieux à votre workflow de développement.

## Utilisez `debugEnabled` dans la commande `configure`

Définissez la valeur booléenne `debugEnabled` sur true lors de la configuration de l’extension. Cette option est généralement utilisée pour les environnements de développement, car elle active le débogage pour tous les visiteurs d’une page de votre site :

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

Voir [`debugEnabled`](../commands/configure/debugenabled.md) pour plus d’informations.

## Utilisation de la commande `setDebug`

À l’instar de la valeur booléenne ci-dessus, cette commande active le débogage pour tous les visiteurs de la page.

```js
alloy("setDebug", {"enabled": true});
```

Pour plus d’informations, voir la commande [`setDebug`](../commands/setdebug.md) .

## Définition d’un paramètre de chaîne de requête

Vous pouvez activer le débogage en ajoutant la chaîne de requête `?alloy_debug=true` à la fin de n’importe quelle URL. Par exemple :

`http://example.com/?alloy_debug=true`

Cette méthode s’applique uniquement à votre ordinateur local, ce qui vous permet de déboguer des sites web de production sans activer le débogage pour tous. L’activation du débogage de cette manière reste activée pour le reste de la session de navigation ou jusqu’à ce que vous la désactivez.

## Utilisation de l’Adobe Experience Platform Debugger

L’Adobe Experience Platform Debugger est un outil puissant qui examine vos pages web et vous aide à déboguer votre implémentation des produits Experience Cloud. Vous pouvez activer le débogage à partir de l’onglet de configuration de la section SDK Web AEP.

![Activer le débogueur](../assets/enable-debugging.png)

Pour plus d’informations, voir [Aperçu de l’Adobe Experience Platform Debugger](/help/debugger/home.md) .
