---
title: prehideStyle
description: Créez une définition CSS qui permet au contenu personnalisé de se charger sans scintillement.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

La variable `prehidingStyle` vous permet de définir un sélecteur CSS pour masquer le contenu personnalisé jusqu’à son chargement. Cette propriété est utile dans les implémentations synchrones du SDK Web pour éviter le scintillement. Adobe recommande d’utiliser la variable [prémasquage du fragment de code](../../personalization/manage-flicker.md) pour les mises en oeuvre asynchrones du SDK Web.

Les sélecteurs CSS que vous définissez dans cette propriété commencent à masquer le contenu lors de la première exécution. [`sendEvent`](../sendevent/overview.md) sur une page. Le contenu est démasqué lorsqu’une réponse d’Adobe est reçue, qui inclut généralement du contenu personnalisé. Le contenu est également démasqué si la variable `sendEvent` échoue ou expire.

Si vous incluez les deux `prehidingStyle` et le fragment de code de masquage préalable dans votre implémentation, le fragment de code de masquage préalable est prioritaire sur cette propriété de configuration.

## Prémasquage du style à l’aide de l’extension de balise SDK Web

Sélectionnez la variable **[!UICONTROL Fournir un style de préremplissage]** lorsque [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Personnalisation] , puis cliquez sur le bouton **[!UICONTROL Fournir un style de préremplissage]**.
1. Ce bouton ouvre une fenêtre modale avec un éditeur CSS. Insérez le sélecteur CSS souhaité et le bloc de déclaration, puis cliquez sur **[!UICONTROL Enregistrer]** pour fermer la fenêtre modale.
1. Cliquez sur **[!UICONTROL Enregistrer]** sous paramètres d’extension, puis publiez vos modifications.

## Prémasquage du style à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `prehidingStyle` chaîne lors de l’exécution de la variable `configure` . Si vous omettez cette propriété lors de la configuration du SDK Web, rien n’est masqué lors de l’exécution de la première `sendEvent` sur une page. Définissez cette valeur sur le sélecteur CSS souhaité et le bloc de déclaration pour les bibliothèques chargées de manière synchrone.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
