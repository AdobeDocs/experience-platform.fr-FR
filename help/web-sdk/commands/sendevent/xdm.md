---
title: xdm
description: Découvrez comment envoyer des données à Adobe par le biais de l’objet aligné sur le schéma XDM.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# `xdm`

La variable `xdm` contient la payload de données envoyée à Adobe. Les champs définis dans cet objet sont directement associés aux éléments définis dans le schéma du jeu de données.

Adobe Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il devient plus facile de conserver un sens et, par conséquent, d’en tirer profit.

Cet objet est limité à 32 Ko au maximum.

## Configuration de l’objet XDM à l’aide de l’extension SDK Web

Définissez la variable **[!UICONTROL XDM]** dans les actions d’une règle de balise. La variable [Objet XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) fournit une interface intuitive pour mapper d’autres éléments de données à leurs champs XDM respectifs.

1. Connexion à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Envoyer un événement]**.
1. Fournissez l’élément de données contenant l’objet souhaité dans la variable **[!UICONTROL XDM]** champ .
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

## Configuration de l’objet XDM à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `xdm` lors de l’exécution de l’objet `sendEvent` . Assurez-vous que la hiérarchie de cet objet correspond au schéma du jeu de données configuré. Vous pouvez inclure les `xdm` et la variable [`data`](data.md) dans le même objet `sendEvent` .

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

L’exemple suivant utilise la méthode [Groupe de champs de schéma Détails du Commerce](/help/xdm/field-groups/event/commerce-details.md):

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
