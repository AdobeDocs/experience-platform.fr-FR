---
title: clickCollectionEnabled
description: Déterminez si les données de clic sur les liens sont automatiquement collectées.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# `clickCollectionEnabled`

La variable `clickCollectionEnabled` est une valeur booléenne qui détermine si le SDK Web collecte automatiquement les données de lien. Cette propriété est utile lorsque vous préférez effectuer un suivi manuel des données de lien.

Si elle n’est pas désactivée, les éléments XDM suivants sont automatiquement renseignés avec des données :

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

## Logique de suivi des liens automatique

Le SDK Web effectue le suivi de tous les clics sur `<a>` et `<area>` Eléments de HTML s’ils ne disposent pas d’un `onClick` attribut. Les clics sont capturés avec une [capture](https://www.w3.org/TR/uievents/#capture-phase) écouteur d’événement click joint au document. Lorsqu’un utilisateur clique sur un lien valide, la logique suivante est exécutée dans l’ordre :

1. Si le lien correspond à des critères basés sur des valeurs dans [`downloadLinkQualifier`](downloadlinkqualifier.md), ou si le lien contient un `download` attribut de HTML, `xdm.web.webInteraction.type` est défini sur `"download"`.
1. Si le domaine cible du lien diffère de l’actif `window.location.hostname`, `xdm.web.webInteraction.type` est défini sur `"exit"`.
1. Si le lien ne remplit pas les conditions suivantes : `"download"` ou `"exit"`, `xdm.web.webInteraction.type` est défini sur `"other"`.

Dans tous les cas, `xdm.web.webInteraction.name` est défini sur le libellé du texte du lien et `xdm.web.webInteraction.URL` est définie sur l’URL de destination du lien. Si vous souhaitez également définir le nom du lien sur l’URL, vous pouvez remplacer ce champ XDM à l’aide de [`onBeforeLinkClickSend`](onbeforelinkclicksend.md).

## Activation du suivi automatique des liens à l’aide de l’extension de balise SDK Web

Sélectionnez la variable **[!UICONTROL Activer la collecte de données de clic]** , [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Collecte de données] , puis cochez la case **[!UICONTROL Activer la collecte de données de clic]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Activation du suivi automatique des liens à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `clickCollectionEnabled` booléen lors de l’exécution de la variable `configure` . Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `true`. Définissez cette valeur sur `false` si vous préférez définir manuellement `xdm.web.webInteraction.type` et `xdm.web.webInteraction.value`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false
});
```
