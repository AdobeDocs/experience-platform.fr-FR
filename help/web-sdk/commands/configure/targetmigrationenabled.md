---
title: targetMigrationEnabled
description: Permet au SDK Web de lire et d’écrire des cookies Adobe Target.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

La variable `targetMigrationEnabled` est une valeur booléenne qui permet au SDK Web de lire et d’écrire les cookies mbox et mboxEdgeCluster utilisés par les bibliothèques Adobe Target 1.x et 2.x. Cette option vous permet de conserver le profil du visiteur entre les pages qui utilisent les mises en oeuvre précédentes d’Adobe Target et les pages qui utilisent le SDK Web.

## Activation de la migration de Target à partir d’at.js à l’aide de l’extension de balise SDK Web

Sélectionnez la variable **[!UICONTROL Migration de Target depuis at.js vers le SDK Web]** , [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Personnalisation] , puis cochez la case **[!UICONTROL Migration de Target depuis at.js vers le SDK Web]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Activation de la migration de Target à partir d’at.js à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `targetMigrationEnabled` booléen lors de l’exécution de la variable `configure` . Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `false`. Définissez cette valeur sur `true` si certaines pages utilisent encore les bibliothèques Adobe Target 1.x ou 2.x.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
