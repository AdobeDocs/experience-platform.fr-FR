---
title: targetMigrationEnabled
description: Permet au SDK Web de lire et d’écrire des cookies Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
TQID: https://experienceleague.adobe.com/F76GzS20NxTKOYF4bR3V-XDAxV-fmR5ZGyJi-x4hJPw
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 171
ht-degree: 0%

---

# `targetMigrationEnabled`

La propriété `targetMigrationEnabled` est une valeur booléenne qui permet à Web SDK de lire et d’écrire les cookies [`mbox` et `mboxEdgeCluster`](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/cookies/web-sdk) utilisés par les bibliothèques Adobe Target 1.x et 2.x. Cette option vous permet de conserver le profil du visiteur entre les pages à l’aide des implémentations précédentes d’Adobe Target et les pages utilisant le SDK Web.

Définissez la valeur booléenne `targetMigrationEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, elle est définie par défaut sur `false`. Définissez cette valeur sur `true` si certaines pages utilisent toujours les bibliothèques Adobe Target 1.x ou 2.x.

Lors de l’utilisation de cette propriété, veillez à activer également le [`overrideMboxEdgeServer`](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) dans `targetGlobalSettings()` dans votre implémentation Adobe Target.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Activer la migration de Target à l’aide de l’extension de balise Web SDK

Ce paramètre peut être configuré dans l’extension de balise Web SDK à l’aide des paramètres de configuration de [Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
