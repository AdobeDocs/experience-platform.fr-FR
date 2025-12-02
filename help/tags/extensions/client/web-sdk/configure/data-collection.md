---
title: Paramètres de configuration de la collecte de données
description: Configurez les paramètres de collecte de données dans l’extension de balise Web SDK.
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# Paramètres de configuration de la collecte de données

Cette section de configuration vous permet de déterminer comment les données sont collectées dans l’extension.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Data collection]** .

![Image montrant les paramètres de collecte de données de l’extension de balise Web SDK dans l’interface utilisateur des balises.](../assets/web-sdk-ext-collection.png)

Les options disponibles sont les suivantes :

## [!UICONTROL On before event send callback]

Fonction de rappel permettant d’évaluer et de modifier la payload envoyée à Adobe. Dans l’éditeur de code, vous avez accès aux variables suivantes :

* **`content.xdm`** : payload XDM pour l’événement.
* **`content.data`** : payload de l’objet de données pour l’événement.
* **`return true`** : quittez immédiatement le rappel et envoyez les données à Adobe avec les valeurs actuelles dans l’objet `content`.
* **`return false`** : quittez immédiatement le rappel et abandonnez l’envoi de données à Adobe.

Toutes les variables définies en dehors de `content` peuvent être utilisées, mais ne sont pas incluses dans la payload envoyée à Adobe.

>[!WARNING]
>
>Ce rappel permet d’utiliser du code personnalisé. Si un code que vous incluez dans le rappel renvoie une exception non interceptée, le traitement de l’événement s’arrête. **Les données ne sont pas envoyées à Adobe.**

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Évitez de renvoyer des `false` sur le premier événement d’une page. Le renvoi d’`false` sur le premier événement peut avoir un impact négatif sur la personnalisation.

Ce rappel est la balise équivalente à [`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md) dans la bibliothèque JavaScript.

## [!UICONTROL Collect internal link clicks]

Case à cocher permettant la collecte de données de suivi des liens internes à votre site ou propriété. Cette case à cocher correspond à la balise [`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) dans la bibliothèque JavaScript. Lorsque vous activez cette case à cocher, les options de regroupement d&#39;événements s&#39;affichent :

* **[!UICONTROL No event grouping]** : les données de suivi des liens sont envoyées à Adobe dans des événements distincts. Les clics sur les liens envoyés dans des événements distincts peuvent accroître l’utilisation contractuelle des données envoyées à Adobe Experience Platform.
* **[!UICONTROL Event grouping using session storage]** : stockez les données de suivi des liens dans le stockage de session jusqu’à l’événement « page vue » suivant. Lors de l’événement suivant considéré comme une « page vue », les données de suivi des liens stockées sont fusionnées avec la payload de l’événement « page vue ». Adobe recommande d’activer ce paramètre lors du suivi des liens internes.
* **[!UICONTROL Event grouping using local object]** : stockez les données de suivi des liens dans un objet local jusqu’à l’événement « page vue » suivant. Si un visiteur accède à une nouvelle page de navigateur, les données de suivi des liens sont perdues. Ce paramètre est particulièrement utile dans le contexte des applications monopages.

La bibliothèque de balises considère un événement donné comme une « page vue » lorsque les éléments suivants sont inclus dans le payload :

* `xdm.web.webPageDetails.name` contient une valeur de chaîne
* `xdm.web.webPageDetails.pageViews.value` est supérieur à `0`

## [!UICONTROL Collect external link clicks]

Case à cocher permettant de collecter les liens externes. Cette case à cocher correspond à la balise [`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) dans la bibliothèque JavaScript.

## [!UICONTROL Collect download link clicks]

Case à cocher permettant de collecter les liens de téléchargement. Cette case à cocher correspond à la balise [`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) dans la bibliothèque JavaScript.

## [!UICONTROL Download link qualifier]

Expression régulière qui qualifie une URL de lien comme lien de téléchargement. Cette chaîne est la balise équivalente à [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md) dans la bibliothèque JavaScript.

## [!UICONTROL Filter click properties]

Fonction de rappel permettant d’évaluer et de modifier les propriétés liées aux clics avant la collecte. Cette fonction s’exécute avant la [!UICONTROL On before event send callback] et est l’équivalent de la balise [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md) dans la bibliothèque JavaScript. Dans l’éditeur de code, vous avez accès aux variables suivantes :

* **`content.clickedElement`** : élément DOM sur lequel l’utilisateur a cliqué.
* **`content.pageName`** : nom de la page lorsque le clic s’est produit.
* **`content.linkName`** : nom du lien sur lequel l’utilisateur a cliqué.
* **`content.linkRegion`** : région du lien sur lequel l’utilisateur a cliqué.
* **`content.linkType`** : type de lien (sortie, téléchargement ou autre).
* **`content.linkURL`** : URL de destination du lien sur lequel l’utilisateur a cliqué.
* **`return true`** : quittez immédiatement le rappel avec les valeurs de variable actuelles.
* **`return false`** : quittez immédiatement le rappel et abandonnez la collecte des données.
* Toutes les variables définies en dehors de `content` peuvent être utilisées, mais ne sont pas incluses dans la payload envoyée à Adobe.

>[!TIP]
>
>Le champ **[!UICONTROL On before link click send]** est un rappel obsolète qui n’est visible que pour les propriétés qui l’ont déjà configuré. Il s’agit de la balise équivalente à [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md) dans la bibliothèque JavaScript. Utilisez le rappel **[!UICONTROL Filter click properties]** pour filtrer ou ajuster les données de clic, ou utilisez le **[!UICONTROL On before event send callback]** pour filtrer ou ajuster la payload globale envoyée à Adobe. Si le rappel **[!UICONTROL Filter click properties]** et le rappel **[!UICONTROL On before link click send]** sont tous deux définis, seul le rappel **[!UICONTROL Filter click properties]** s’exécute.

## Paramètres de contexte

Collectez automatiquement les informations sur les visiteurs, qui renseignent des champs XDM spécifiques pour vous. Vous pouvez choisir entre **[!UICONTROL All default context information]** ou **[!UICONTROL Specific context information]**. Il s’agit de la balise équivalente à [`context`](/help/collection/js/commands/configure/context.md) dans la bibliothèque JavaScript.

* **[!UICONTROL Web]** : collecte des informations sur la page active.
* **[!UICONTROL Device]** : collecte des informations sur l’appareil de l’utilisateur.
* **[!UICONTROL Environment]** : collecte des informations sur le navigateur de l’utilisateur.
* **[!UICONTROL Place context]** : collecte des informations sur l’emplacement de l’utilisateur.
* **[!UICONTROL High entropy user-agent hints]** : collecte des informations plus détaillées sur l’appareil de l’utilisateur.
