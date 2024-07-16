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

La propriété `renderDecisions` vous permet de forcer le SDK Web à effectuer le rendu de tout contenu personnalisé éligible au rendu automatique.

## Rendu du contenu personnalisé à l’aide de l’extension de balise SDK Web

Cochez la case **[!UICONTROL Render Visual personalization Decisions]** dans les actions d’une règle de balise.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Envoyer l’événement]**.
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Personalization], puis cochez la case **[!UICONTROL Render Visual personalization Decisions]** .
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

## Rendu du contenu personnalisé à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la valeur booléenne `renderDecisions` lors de l’exécution de la commande `sendEvent`. Si cette propriété est omise, elle est définie par défaut sur `false`. Définissez cette propriété sur `true` si vous souhaitez effectuer automatiquement le rendu du contenu personnalisé.

>[!IMPORTANT]
>
>La propriété `renderDecisions` est incompatible avec la propriété [`documentUnloading`](documentunloading.md). Vous ne devez pas définir les deux propriétés sur `true` simultanément.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
