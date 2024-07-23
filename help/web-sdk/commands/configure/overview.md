---
title: Configuration du SDK Web de Adobe Experience Platform
description: Utilisez la commande configure pour définir les paramètres requis lors de l’utilisation du SDK Web.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Configuration du SDK Web de Adobe Experience Platform

La configuration du SDK Web est effectuée à l’aide de la commande `configure`. La configuration du SDK Web est une étape essentielle et requise qui doit se produire chaque fois que la bibliothèque ou l’extension de balise est utilisée.

## Configuration du SDK Web à l’aide de l’extension de balise {#configure-tag-extension}

Suivez les étapes ci-dessous pour configurer le SDK Web via l’extension de balise.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Accédez à la [page de configuration de l’extension de balise SDK Web](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) pour plus d’informations sur toutes les options de configuration.

Ces paramètres de configuration sont définis chaque fois que vous utilisez l’extension pour envoyer des données à Adobe.

## Configuration du SDK Web à l’aide de la bibliothèque JavaScript {#configure-js}

Exécutez la commande `configure`. Cette commande est requise avant que vous ne puissiez appeler d’autres commandes du SDK Web, telles que [`sendEvent`](../sendevent/overview.md).

Les propriétés [`datastreamId`](datastreamid.md) et [`orgId`](orgid.md) sont requises. Toutes les autres propriétés sont facultatives, selon les exigences de mise en oeuvre de votre entreprise.

Consultez la table des matières de ce guide d’utilisation pour plus d’informations sur chacune des commandes prises en charge.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
