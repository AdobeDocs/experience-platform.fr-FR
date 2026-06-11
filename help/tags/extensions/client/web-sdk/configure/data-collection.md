---
title: Paramètres de configuration de la collecte de données
description: Configurez les paramètres de collecte de données dans l’extension de balise Web SDK.
exl-id: 88c34545-9a58-4d49-a939-36edaa9a46be
TQID: https://experienceleague.adobe.com/i1Q45GvFU8S73NBxDsGPKyLU8S-EdzbKyys2-7DNchs
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: f6ff4d13-7b5c-4533-8556-95e76673d4cb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 827
ht-degree: 3%

---

# Paramètres de configuration de la collecte de données {#data-collection}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_datacollection"
>title="Collecte de données"
>abstract="Déterminez les données à collecter et la manière dont elles sont collectées dans l’extension de balises."

Cette section de configuration vous permet de déterminer comment les données sont collectées dans l’extension.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Collecte de données]**.

![Image montrant les paramètres de collecte de données de l’extension de balise Web SDK dans l’interface utilisateur des balises.](../assets/web-sdk-ext-collection.png)

Les options disponibles sont les suivantes :

## [!UICONTROL &#x200B; Activé avant le rappel d’envoi d’événement &#x200B;]

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

## [!UICONTROL Collecter les clics sur les liens internes]

Case à cocher permettant la collecte de données de suivi des liens internes à votre site ou propriété. Cette case à cocher correspond à la balise [`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) dans la bibliothèque JavaScript. Lorsque vous activez cette case à cocher, les options de regroupement d&#39;événements s&#39;affichent :

* **[!UICONTROL Aucun regroupement d’événements]** : les données de suivi des liens sont envoyées à Adobe dans des événements distincts. Les clics sur les liens envoyés dans des événements distincts peuvent accroître l’utilisation contractuelle des données envoyées à Adobe Experience Platform.
* **[!UICONTROL Regroupement des événements à l’aide du stockage de session]** : stockez les données de suivi des liens dans le stockage de session jusqu’à l’événement « page vue » suivant. Lors de l’événement suivant considéré comme une « page vue », les données de suivi des liens stockées sont fusionnées avec la payload de l’événement « page vue ». Adobe recommande d’activer ce paramètre lors du suivi des liens internes.
* **[!UICONTROL Regroupement d’événements à l’aide de l’objet local]** : stockez les données de suivi des liens dans un objet local jusqu’à l’événement « page vue » suivant. Si un visiteur accède à une nouvelle page de navigateur, les données de suivi des liens sont perdues. Ce paramètre est particulièrement utile dans le contexte des applications monopages.

La bibliothèque de balises considère un événement donné comme une « page vue » lorsque les éléments suivants sont inclus dans le payload :

* `xdm.web.webPageDetails.name` contient une valeur de chaîne
* `xdm.web.webPageDetails.pageViews.value` est supérieur à `0`

## [!UICONTROL Collecter les clics sur les liens externes]

Case à cocher permettant de collecter les liens externes. Cette case à cocher correspond à la balise [`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) dans la bibliothèque JavaScript.

## [!UICONTROL Collecter les clics sur les liens de téléchargement]

Case à cocher permettant de collecter les liens de téléchargement. Cette case à cocher correspond à la balise [`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) dans la bibliothèque JavaScript.

## [!UICONTROL Téléchargement du qualificateur de lien]

Expression régulière qui qualifie une URL de lien comme lien de téléchargement. Cette chaîne est la balise équivalente à [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md) dans la bibliothèque JavaScript.

## [!UICONTROL Propriétés des clics de filtre]

Fonction de rappel permettant d’évaluer et de modifier les propriétés liées aux clics avant la collecte. Cette fonction s’exécute avant le rappel d’envoi d’événement [!UICONTROL Activé avant] et est l’équivalent de la balise [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md) dans la bibliothèque JavaScript. Dans l’éditeur de code, vous avez accès aux variables suivantes :

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
>Le champ **[!UICONTROL Activé avant l’envoi du clic sur le lien]** est un rappel obsolète qui n’est visible que pour les propriétés qui l’ont déjà configuré. Il s’agit de la balise équivalente à [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md) dans la bibliothèque JavaScript. Utilisez le rappel **[!UICONTROL Filtrer les propriétés des clics]** pour filtrer ou ajuster les données de clics, ou utilisez le rappel **[!UICONTROL Activé avant l’envoi de l’événement]** pour filtrer ou ajuster la payload globale envoyée à Adobe. Si les rappels **[!UICONTROL Filtrer les propriétés des clics]** et **[!UICONTROL Activer avant l’envoi du clic sur les liens]** sont définis, seul le rappel **[!UICONTROL Filtrer les propriétés des clics]** s’exécute.

## Paramètres de contexte

Collectez automatiquement les informations sur les visiteurs, qui renseignent des champs XDM spécifiques pour vous. Vous pouvez choisir **[!UICONTROL Toutes les informations contextuelles par défaut]** ou **[!UICONTROL Informations contextuelles spécifiques]**. Il s’agit de la balise équivalente à [`context`](/help/collection/js/commands/configure/context.md) dans la bibliothèque JavaScript.

* **[!UICONTROL Web]** : collecte des informations sur la page active.
* **[!UICONTROL Appareil]** : collecte des informations sur l’appareil de l’utilisateur.
* **[!UICONTROL Environnement]** : collecte des informations sur le navigateur de l’utilisateur.
* **[!UICONTROL Contexte d’emplacement]** : collecte des informations sur l’emplacement de l’utilisateur.
* **[!UICONTROL Indications agent-utilisateur à entropie élevée]** : collecte des informations plus détaillées sur l’appareil de l’utilisateur.
* **[!UICONTROL Envoyer le référent à Adobe Analytics une seule fois par page vue]** : empêchez l’envoi de données de référent en double à Adobe Analytics.
