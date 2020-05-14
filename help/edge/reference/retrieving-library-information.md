---
title: Récupération des informations sur la bibliothèque
seo-title: Récupération des informations sur la bibliothèque avec le SDK Web d’Adobe Experience Platform
description: Découvrez comment récupérer des informations sur la bibliothèque chargée sur le site web
seo-description: Découvrez comment récupérer des informations sur la bibliothèque chargée sur le site web
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 100%

---


# Récupération des informations sur la bibliothèque

Il est souvent utile d’accéder à certains détails de la bibliothèque que vous avez chargée sur votre site web. Pour cela, exécutez la commande `getLibraryInfo` de la manière suivante :

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Actuellement, l’objet `libraryInfo` fourni contient les propriétés suivantes :

* `version` Il s’agit de la version de la bibliothèque chargée. Par exemple, si la version de la bibliothèque chargée est 1.0.0, la valeur est `1.0.0`.