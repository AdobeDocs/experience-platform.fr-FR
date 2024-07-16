---
title: prehideStyle
description: Créez une définition CSS qui permet au contenu personnalisé de se charger sans scintillement.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

La propriété `prehidingStyle` vous permet de définir un sélecteur CSS pour masquer le contenu personnalisé jusqu’à son chargement. Cette propriété est utile dans les implémentations synchrones du SDK Web pour éviter le scintillement. Adobe recommande d’utiliser le [fragment de code de masquage préalable](../../personalization/manage-flicker.md) pour les implémentations asynchrones du SDK Web.

Les sélecteurs CSS que vous définissez dans cette propriété commencent à masquer le contenu lorsque vous exécutez la première commande [`sendEvent`](../sendevent/overview.md) sur une page. Le contenu est démasqué lorsqu’une réponse d’Adobe est reçue, qui inclut généralement du contenu personnalisé. Le contenu est également démasqué si la commande `sendEvent` échoue ou expire.

Si vous incluez `prehidingStyle` et le fragment de code de masquage préalable dans votre mise en oeuvre, le fragment de code de masquage préalable est prioritaire sur cette propriété de configuration.

## Prémasquage du style à l’aide de l’extension de balise SDK Web

Sélectionnez le bouton **[!UICONTROL Fournir un style de prémasquage]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Personalization], puis sélectionnez le bouton **[!UICONTROL Fournir un style de prémasquage]**.
1. Ce bouton ouvre une fenêtre modale avec un éditeur CSS. Insérez le sélecteur CSS et le bloc de déclaration de votre choix, puis cliquez sur **[!UICONTROL Enregistrer]** pour fermer la fenêtre modale.
1. Cliquez sur **[!UICONTROL Enregistrer]** sous les paramètres d’extension, puis publiez vos modifications.

## Prémasquage du style à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la chaîne `prehidingStyle` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK Web, rien n’est masqué lors de l’exécution de la première commande `sendEvent` sur une page. Définissez cette valeur sur le sélecteur CSS souhaité et le bloc de déclaration pour les bibliothèques chargées de manière synchrone.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
