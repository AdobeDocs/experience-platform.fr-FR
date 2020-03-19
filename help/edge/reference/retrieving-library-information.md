---
title: Récupération des informations de bibliothèque
seo-title: Récupération des informations de bibliothèque avec le SDK Web d’Adobe Experience Platform
description: Découvrez comment récupérer des informations sur la bibliothèque chargée sur le site Web
seo-description: Découvrez comment récupérer des informations sur la bibliothèque chargée sur le site Web par le kit SDK Adobe Experience Cloud collecte automatiquement les informations
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Récupération des informations de bibliothèque

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Il est souvent utile d’accéder à certains détails de la bibliothèque que vous avez chargée sur votre site Web. Pour ce faire, exécutez la `getLibraryInfo` commande comme suit :

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Actuellement, l’ `libraryInfo` objet fourni contient les propriétés suivantes :

* `version` Il s’agit de la version de la bibliothèque chargée. Par exemple, si la version de la bibliothèque chargée était 1.0.0, la valeur serait `1.0.0`.