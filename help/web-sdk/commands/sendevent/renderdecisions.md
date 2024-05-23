---
title: renderDecisions
description: Rendre le contenu personnalisé éligible au rendu automatique.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

La variable `renderDecisions` vous permet de forcer le SDK Web à effectuer le rendu de tout contenu personnalisé éligible au rendu automatique.

## Rendu du contenu personnalisé à l’aide de l’extension de balise SDK Web

Sélectionnez la variable **[!UICONTROL Rendu des décisions de personnalisation visuelle]** dans les actions d’une règle de balise.

1. Connexion à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Envoyer un événement]**.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Personnalisation] , puis sélectionnez l’option **[!UICONTROL Rendu des décisions de personnalisation visuelle]** .
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

## Rendu du contenu personnalisé à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `renderDecisions` booléen lors de l’exécution de la variable `sendEvent` . Si cette propriété est omise, elle prend par défaut la valeur `false`. Définissez cette propriété sur `true` si vous souhaitez effectuer automatiquement le rendu du contenu personnalisé.

>[!IMPORTANT]
>
>La variable `renderDecisions` est incompatible avec la propriété [`documentUnloading`](documentunloading.md) . Ne définissez pas les deux propriétés sur `true` simultanément.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
