---
title: targetMigrationEnabled
description: Permet au SDK Web de lire et d’écrire des cookies Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 051374def898d3797711525c5343e0a8454970a2
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# `targetMigrationEnabled`

La propriété `targetMigrationEnabled` est une valeur booléenne qui permet à Web SDK de lire et d’écrire les cookies [`mbox` et `mboxEdgeCluster`](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/cookies/web-sdk) utilisés par les bibliothèques Adobe Target 1.x et 2.x. Cette option vous permet de conserver le profil du visiteur entre les pages à l’aide des implémentations précédentes d’Adobe Target et les pages utilisant le SDK Web.

Définissez la valeur booléenne `targetMigrationEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, elle est définie par défaut sur `false`. Définissez cette valeur sur `true` si certaines pages utilisent toujours les bibliothèques Adobe Target 1.x ou 2.x.

Lors de l’utilisation de cette propriété, veillez à activer également le [`overrideMboxEdgeServer`](https://experienceleague.adobe.com/fr/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) dans `targetGlobalSettings()` dans votre implémentation Adobe Target.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Activer la migration de Target à l’aide de l’extension de balise Web SDK

Ce paramètre peut être configuré dans l’extension de balise Web SDK à l’aide des paramètres de configuration de [Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
