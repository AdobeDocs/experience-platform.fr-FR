---
title: targetMigrationEnabled
description: Permet au SDK Web de lire et d’écrire des cookies Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

La propriété `targetMigrationEnabled` est une valeur booléenne qui permet au SDK Web de lire et d’écrire les cookies mbox et mboxEdgeCluster utilisés par les bibliothèques Adobe Target 1.x et 2.x. Cette option vous permet de conserver le profil du visiteur entre les pages qui utilisent les mises en oeuvre précédentes d’Adobe Target et les pages qui utilisent le SDK Web.

## Activation de la migration de Target à partir d’at.js à l’aide de l’extension de balise SDK Web

Cochez la case **[!UICONTROL Migrer Target d’at.js vers le SDK Web]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Personalization], puis cochez la case **[!UICONTROL Migrer Target d’at.js vers le SDK Web]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Activation de la migration de Target à partir d’at.js à l’aide de la bibliothèque JavaScript SDK Web

Définissez la valeur booléenne `targetMigrationEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `false`. Définissez cette valeur sur `true` si certaines pages utilisent toujours les bibliothèques Adobe Target 1.x ou 2.x.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
