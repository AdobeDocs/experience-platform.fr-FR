---
title: onBeforeLinkClickSend
description: Rappel qui s’exécute juste avant l’envoi des données de suivi des liens.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

La variable `onBeforeLinkClickSend` callback vous permet d’enregistrer une fonction JavaScript qui peut modifier les données de suivi des liens que vous envoyez juste avant l’envoi de ces données à Adobe. Ce rappel vous permet de manipuler la variable `xdm` ou `data` , y compris la possibilité d’ajouter, de modifier ou de supprimer des éléments. Vous pouvez également annuler de manière conditionnelle l’envoi de données, par exemple avec le trafic de robots côté client détecté. Elle est prise en charge sur le SDK Web 2.15.0 ou version ultérieure.

Ce rappel ne s’exécute que lorsque [`clickCollectionEnabled`](clickcollectionenabled.md) est activée. If `clickCollectionEnabled` est désactivé, ce rappel ne s’exécute pas. Si les deux `onBeforeEventSend` et `onBeforeLinkClickSend` contiennent des fonctions enregistrées, l’objet `onBeforeLinkClickSend` s’exécute en premier. Une fois que la variable `onBeforeLinkClickSend` se termine, la fonction `onBeforeEventSend` puis s’exécute.

>[!WARNING]
>
>Ce rappel permet l’utilisation de code personnalisé. Si un code que vous incluez dans le rappel renvoie une exception non interceptée, le traitement de l’événement est interrompu. Les données ne sont pas envoyées à Adobe.

## Avant le lien, cliquez sur Send callback à l’aide de l’extension de balise SDK Web.

Sélectionnez la variable **[!UICONTROL Fournir avant le code de rappel d’événement de clic sur les liens]** lorsque [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Ce bouton ouvre une fenêtre modale dans laquelle vous pouvez insérer le code de votre choix.

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Collecte de données] , puis cochez la case **[!UICONTROL Activer la collecte de données de clic]**.
1. Sélectionnez le bouton intitulé **[!UICONTROL Fournir avant le code de rappel d’événement de clic sur les liens]**.
1. Ce bouton ouvre une fenêtre modale avec un éditeur de code. Insérez le code souhaité, puis cliquez sur **[!UICONTROL Enregistrer]** pour fermer la fenêtre modale.
1. Cliquez sur **[!UICONTROL Enregistrer]** sous paramètres d’extension, puis publiez vos modifications.

Dans l’éditeur de code, vous pouvez ajouter, modifier ou supprimer des éléments dans le `content` . Cet objet contient la payload envoyée à Adobe. Vous n’avez pas besoin de définir la variable `content` ou placer tout code dans une fonction. Toute variable définie en dehors de `content` peuvent être utilisées, mais ne sont pas incluses dans la payload envoyée à Adobe.

>[!TIP]
>
>Les objets `content.xdm`, `content.data`, et `content.clickedElement` sont toujours définis dans ce contexte. Il n’est donc pas nécessaire de vérifier s’ils existent. Certaines variables de ces objets dépendent de votre mise en oeuvre et de votre couche de données. Adobe recommande de rechercher les valeurs non définies dans ces objets afin d’éviter les erreurs JavaScript.

Par exemple, supposons que vous souhaitiez effectuer les actions suivantes :

* Modifier l’URL de la page active
* Capture de l’élément sur lequel l’utilisateur a cliqué dans un eVar Adobe Analytics
* Remplacez le type de lien &quot;other&quot; par &quot;download&quot;.

Le code équivalent dans la fenêtre modale serait le suivant :

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

De la même manière que [`onBeforeEventSend`](onbeforeeventsend.md), vous pouvez `return true` pour terminer immédiatement la fonction ; ou `return false` pour annuler immédiatement l’envoi de données. Si vous annulez l’envoi de données dans `onBeforeLinkClickSend` lorsque les deux `onBeforeEventSend` et `onBeforeLinkClickSend` contiennent des fonctions enregistrées, l’objet `onBeforeEventSend` ne s’exécute pas.

## Avant le lien, cliquez sur Envoyer le rappel à l’aide de la bibliothèque JavaScript SDK Web

Enregistrez le `onBeforeLinkClickSend` rappel lors de l’exécution de la fonction `configure` . Vous pouvez modifier la variable `content` nom de la variable à n’importe quelle valeur en modifiant la variable de paramètre dans la fonction intégrée.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to immediately complete the function
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": lastChanceLinkLogic
});    
```
