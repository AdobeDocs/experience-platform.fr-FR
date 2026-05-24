---
title: xdm
description: Découvrez comment envoyer des données à Adobe par le biais de l’objet aligné sur un schéma XDM.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
TQID: https://experienceleague.adobe.com/DO-YHT1JYbAdu6HIOmUEN4cNKE3ZSEtFhFWb4XXEhcA
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: eadea719-cf89-469b-a6fd-a236a7138047id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 158
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

L’exemple suivant utilise le groupe de champs de schéma Détails de Commerce [](/help/xdm/field-groups/event/commerce-details.md) :

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
