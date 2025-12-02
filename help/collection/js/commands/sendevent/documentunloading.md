---
title: documentUnloading
description: Utilisez l’API sendBeacon de JavaScript pour envoyer des données à Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

La propriété `documentUnloading` vous permet d’utiliser la méthode [`sendBeacon`](https://developer.mozilla.org/fr-FR/docs/Web/API/Navigator/sendBeacon) JavaScript pour envoyer des données à Adobe. Si une requête standard prend trop de temps, le navigateur peut l’annuler. Vous pouvez indiquer au SDK Web d’utiliser `sendBeacon` afin que la requête s’exécute en arrière-plan après avoir quitté la page. Activez cette propriété pour empêcher les requêtes de données d’être annulées par le navigateur lors du déchargement.

Plusieurs navigateurs imposent une limite de 64 Ko à la quantité de données pouvant être envoyées avec `sendBeacon` à la fois. Si le navigateur rejette l’événement en raison d’une payload trop importante, le SDK Web revient à utiliser sa méthode de transport habituelle. Même si un navigateur donné autorise des payloads plus volumineux, les serveurs de collecte de données d’Adobe tronquent les payloads jusqu’à 64 Ko.

Définissez la valeur booléenne `documentUnloading` lors de l’exécution de la commande `sendEvent`. Sa valeur par défaut est `false`. Définissez cette propriété sur `true` si vous souhaitez utiliser la méthode `sendBeacon` pour envoyer des données à Adobe.

>[!IMPORTANT]
>
>La propriété `documentUnloading` est incompatible avec la propriété [`renderDecisions`](renderdecisions.md). Évitez de définir les deux propriétés sur `true` simultanément.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## Déchargement du document à l’aide de l’extension de balise Web SDK

La case à cocher **[!UICONTROL Document will unload]** est disponible lors de la configuration d’une action [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) lors de l’utilisation de l’extension de balise Web SDK.
