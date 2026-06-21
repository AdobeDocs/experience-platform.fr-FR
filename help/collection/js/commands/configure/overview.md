---
title: Configuration de Adobe Experience Platform Web SDK
description: Utilisez la commande de configuration pour définir les paramètres requis lors de l’utilisation de Web SDK.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
TQID: https://experienceleague.adobe.com/MPrJXWHz2aG1iXNg5JmrGTS9MDSGeHJCtwJkjHMwLZE
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e43347a8-f2c5-4aa4-8623-6f13875d7e3aid: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ceid: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 82
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
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints", "oneTimeAnalyticsReferrer"],
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
  conversation: {
    stickyConversationSession: false
  },
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
