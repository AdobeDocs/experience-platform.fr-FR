---
title: idMigrationEnabled
description: Permet au SDK Web de lire les cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

La propriété `idMigrationEnabled` permet au SDK Web de lire les cookies AMCV définis par les mises en oeuvre précédentes de Adobe Experience Cloud. Si votre entreprise met à niveau votre mise en oeuvre vers le SDK Web, ce paramètre permet une transition plus fluide vers le service Adobe Experience Cloud ID actuel. Ce paramètre est utile pour éviter une forte augmentation du nombre de visiteurs uniques lors de la mise à niveau vers le SDK Web.

Si votre entreprise exécute une nouvelle mise en oeuvre du SDK Web, l’activation de ce paramètre n’a aucun impact sur la collecte de données ou l’identification des visiteurs. Il n’y a aucun inconvénient à ce qu’elle soit activée pour toutes les implémentations.

## Activation de la migration des identifiants à l’aide de l’extension de balise SDK Web

Cochez la case **[!UICONTROL Migrer l’ECID de VisitorAPI vers le SDK Web]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Recherchez la section [!UICONTROL Identité] , puis cochez la case **[!UICONTROL Migrer l’ECID de VisitorAPI vers le SDK Web]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Activation de la migration des identifiants à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la valeur booléenne `idMigrationEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `true`. Définissez cette propriété si vous souhaitez désactiver la possibilité de lire les cookies AMCV définis par l’API visiteur. La plupart des entreprises n’ont pas besoin de définir cette propriété.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
