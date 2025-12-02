---
title: Configuration de Adobe Experience Platform Web SDK
description: Utilisez la commande de configuration pour définir les paramètres requis lors de l’utilisation de Web SDK.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Configuration de Adobe Experience Platform Web SDK

La configuration de Web SDK s’effectue avec la commande **`configure`**. Cette commande est requise à chaque chargement de page avant d’appeler toute autre commande Web SDK, telle que [`sendEvent`](../sendevent/overview.md).

**Les propriétés [`datastreamId`](datastreamid.md) et [`orgId`](orgid.md) sont obligatoires.** Toutes les autres propriétés sont facultatives, selon les exigences d’implémentation de votre organisation. L’exemple suivant illustre un objet de configuration utilisant la plupart des propriétés disponibles :

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
    filterClickDetails: function(content) {
      content.linkUrl = "https://example.com/current.html";
    },
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
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
