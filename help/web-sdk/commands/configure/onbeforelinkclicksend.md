---
title: onBeforeLinkClickSend
description: Rappel qui s’exécute juste avant l’envoi des données de suivi des liens.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Ce rappel est obsolète. Utilisation [`filterClickDetails`](clickcollection.md) au lieu de .

La variable `onBeforeLinkClickSend` callback vous permet d’enregistrer une fonction JavaScript qui peut modifier les données de suivi des liens que vous envoyez juste avant que ces données ne soient envoyées à Adobe. Ce rappel vous permet de manipuler la variable `xdm` ou `data` , y compris la possibilité d’ajouter, de modifier ou de supprimer des éléments. Vous pouvez également annuler de manière conditionnelle l’envoi de données, par exemple avec le trafic de robots côté client détecté. Elle est prise en charge sur le SDK Web 2.15.0 ou version ultérieure.

Ce rappel ne s’exécute que lorsque [`clickCollectionEnabled`](clickcollectionenabled.md) est activé et [`filterClickDetails`](clickcollection.md) ne contient pas de fonction enregistrée. If `clickCollectionEnabled` est désactivé, ou si `filterClickDetails` contient une fonction enregistrée, puis ce rappel ne s’exécute pas. If `onBeforeEventSend` et `onBeforeLinkClickSend` contiennent tous deux des fonctions enregistrées, `onBeforeLinkClickSend` est exécuté en premier.

>[!WARNING]
>
>Ce rappel permet l’utilisation de code personnalisé. Si un code que vous incluez dans le rappel renvoie une exception non interceptée, le traitement de l’événement est interrompu. Les données ne sont pas envoyées à Adobe.

## Configurez avant le rappel de rappel de clic sur les liens à l’aide de l’extension de balise SDK Web. {#tag-extension}

Sélectionnez la variable **[!UICONTROL Fournir avant le code de rappel d’événement de clic sur les liens]** lorsque [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Ce bouton ouvre une fenêtre modale dans laquelle vous pouvez insérer le code de votre choix.

1. Connexion à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Collecte de données] , puis cochez la case **[!UICONTROL Activer la collecte de données de clic]**.
1. Sélectionnez le bouton intitulé **[!UICONTROL Fournir avant le code de rappel d’événement de clic sur les liens]**.
1. Ce bouton ouvre une fenêtre modale avec un éditeur de code. Insérez le code souhaité, puis cliquez sur **[!UICONTROL Enregistrer]** pour fermer la fenêtre modale.
1. Cliquez sur **[!UICONTROL Enregistrer]** sous paramètres d’extension, puis publiez vos modifications.

Dans l’éditeur de code, vous avez accès aux variables suivantes :

* **`content.clickedElement`**: élément DOM sur lequel l’utilisateur a cliqué.
* **`content.xdm`**: charge utile XDM de l’événement.
* **`content.data`**: charge utile de l’objet de données pour l’événement.
* **`return true`**: quittez immédiatement le rappel avec les valeurs de variable actuelles. La variable `onBeforeEventSend` callback s’exécute s’il contient une fonction enregistrée.
* **`return false`**: quittez immédiatement le rappel et abandonnez l’envoi de données à Adobe. La variable `onBeforeEventSend` callback n’est pas exécuté.

Toute variable définie en dehors de `content` peuvent être utilisées, mais ne sont pas incluses dans la payload envoyée à Adobe.

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

De la même manière que [`onBeforeEventSend`](onbeforeeventsend.md), vous pouvez `return true` pour exécuter immédiatement la fonction ; ou `return false` pour abandonner l’envoi de données à Adobe. Si vous abandonnez l’envoi de données dans `onBeforeLinkClickSend` lorsque les deux `onBeforeEventSend` et `onBeforeLinkClickSend` contiennent des fonctions enregistrées, l’objet `onBeforeEventSend` ne s’exécute pas.

## Configurez avant le rappel de rappel de clic sur les liens à l’aide de la bibliothèque JavaScript SDK Web {#library}

Enregistrez le `onBeforeLinkClickSend` rappel lors de l’exécution de la fonction `configure` . Vous pouvez modifier la variable `content` nom de la variable à n’importe quelle valeur en modifiant la variable de paramètre dans la fonction intégrée.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

Vous pouvez également enregistrer votre propre fonction au lieu d’une fonction intégrée.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
