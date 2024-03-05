---
title: Configuration du SDK Web de Adobe Experience Platform
description: Utilisez la commande configure pour définir les paramètres requis lors de l’utilisation du SDK Web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Configuration du SDK Web de Adobe Experience Platform

La configuration du SDK Web s’effectue à l’aide de la fonction `configure` . La configuration du SDK Web est une étape essentielle et requise qui doit se produire chaque fois que la bibliothèque ou l’extension de balise est utilisée.

## Paramètres de configuration à l’aide de l’extension de balise SDK Web

Accédez au [page de configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.

Ces paramètres de configuration sont définis chaque fois que vous utilisez l’extension pour envoyer des données à Adobe.

## Paramètres de configuration à l’aide de la bibliothèque JavaScript du SDK Web

Exécutez la variable `configure` . Cette commande est nécessaire avant de pouvoir appeler toute autre commande du SDK Web, telle que [`sendEvent`](../sendevent/overview.md). Propriétés [`edgeConfigId`](edgeconfigid.md) et [`orgId`](orgid.md) sont obligatoires. Toutes les autres propriétés sont facultatives, selon les exigences de mise en oeuvre de votre entreprise.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
