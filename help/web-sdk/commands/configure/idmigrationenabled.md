---
title: idMigrationEnabled
description: Permet au SDK Web de lire les cookies AMCV.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

La variable `idMigrationEnabled` permet au SDK Web de lire les cookies AMCV définis par les mises en oeuvre précédentes de Adobe Experience Cloud. Si votre entreprise met à niveau votre mise en oeuvre vers le SDK Web, ce paramètre permet une transition plus fluide vers le service Adobe Experience Cloud ID actuel. Ce paramètre est utile pour éviter une forte augmentation du nombre de visiteurs uniques lors de la mise à niveau vers le SDK Web.

Si votre entreprise exécute une nouvelle mise en oeuvre du SDK Web, l’activation de ce paramètre n’a aucun impact sur la collecte de données ou l’identification des visiteurs. Il n’y a aucun inconvénient à ce qu’elle soit activée pour toutes les implémentations.

## Activation de la migration des identifiants à l’aide de l’extension de balise SDK Web

Sélectionnez la variable **[!UICONTROL Migration de l’ECID de VisitorAPI vers le SDK web]** , [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Recherchez la variable [!UICONTROL Identité] , puis cochez la case **[!UICONTROL Migration de l’ECID de VisitorAPI vers le SDK web]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Activation de la migration des identifiants à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `idMigrationEnabled` booléen lors de l’exécution de la variable `configure` . Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `true`. Définissez cette propriété si vous souhaitez désactiver la possibilité de lire les cookies AMCV définis par l’API visiteur. La plupart des entreprises n’ont pas besoin de définir cette propriété.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
