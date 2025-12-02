---
title: xdm
description: Découvrez comment envoyer des données à Adobe par le biais de l’objet aligné sur un schéma XDM.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

L’objet `xdm` contient la payload de données envoyée à Adobe. Les champs définis dans cet objet mappent directement aux éléments définis dans le schéma du jeu de données.

Adobe Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus facile de leur donner du sens et, par conséquent, d’en tirer profit.

Définissez l’objet `xdm` lors de l’exécution de la commande `sendEvent`. Assurez-vous que la hiérarchie de cet objet correspond au schéma du jeu de données configuré. Vous pouvez inclure l’objet `xdm` et l’objet [`data`](data.md) dans la même commande `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

L’exemple suivant utilise le groupe de champs de schéma Détails de Commerce [&#128279;](/help/xdm/field-groups/event/commerce-details.md) :

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```

## Utiliser l’objet `xdm` à l’aide de l’extension de balise Web SDK

L’objet `xdm` est disponible sous la forme d’un [élément de données de variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) ou d’un [élément de données d’objet XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) lors de l’utilisation de l’extension de balise Web SDK. Adobe recommande dans la plupart des cas l’utilisation d’un élément de données variable.
