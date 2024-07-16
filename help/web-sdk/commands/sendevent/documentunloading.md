---
title: documentUnloading
description: Utilisez l’API sendBeacon de JavaScript pour envoyer des données à Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

La propriété `documentUnloading` vous permet d’utiliser la méthode JavaScript [`sendBeacon`](https://developer.mozilla.org/fr-FR/docs/Web/API/Navigator/sendBeacon) pour envoyer des données à Adobe. Si une requête type prend trop de temps, le navigateur peut annuler la requête. Vous pouvez indiquer au SDK Web d’utiliser `sendBeacon` afin que la requête s’exécute en arrière-plan une fois que vous avez quitté la page. Activez cette propriété pour empêcher les demandes de données d’être annulées par le navigateur lors du déchargement.

Plusieurs navigateurs imposent une limite de 64 Ko à la quantité de données pouvant être simultanément envoyées avec `sendBeacon`. Si le navigateur rejette l’événement car la charge utile est trop importante, le SDK Web reprend l’utilisation de sa méthode de transport normale.

## Configuration du déchargement de documents à l’aide de l’extension de balise SDK Web

Activez la case à cocher **[!UICONTROL Le document va se décharger]** dans les actions d’une règle de balise.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Envoyer l’événement]**.
1. Activez la case à cocher **[!UICONTROL Le document va se décharger]** dans la section [!UICONTROL Data] .
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

## Configuration du déchargement des documents à l’aide de la bibliothèque JavaScript SDK Web

Définissez la valeur booléenne `documentUnloading` lors de l’exécution de la commande `sendEvent`. Sa valeur par défaut est `false`. Définissez cette propriété sur `true` si vous souhaitez utiliser la méthode `sendBeacon` pour envoyer des données à Adobe.

>[!IMPORTANT]
>
>La propriété `documentUnloading` est incompatible avec la propriété [`renderDecisions`](renderdecisions.md). Vous ne devez pas définir les deux propriétés sur `true` simultanément.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
