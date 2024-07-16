---
title: orgId
description: La propriété orgId est une chaîne qui indique à l’Adobe à quelle organisation les données sont envoyées.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

La propriété `orgId` est une chaîne qui indique à l’Adobe à quelle organisation les données sont envoyées. **Cette propriété est requise pour toutes les données envoyées à l’aide du SDK Web.**

Pour localiser votre `orgID` :

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. N’importe où dans Adobe Experience Cloud, appuyez sur **`[Ctrl]`** + **`[I]`**. Une fenêtre [!UICONTROL User Data Debugger] s’ouvre.
1. Cliquez sur **[!UICONTROL Copier]** ![Copier](../../assets/copy.png) en regard de l’ [!UICONTROL ID d’organisation actuel] ou cliquez sur l’onglet **[!UICONTROL Organisation affectée]** pour afficher les autres ID d’organisation auxquels vous avez accès.
1. Lorsque vous avez terminé de trouver les informations souhaitées, cliquez sur **[!UICONTROL Fermer]**.

Les identifiants d’organisation sont toujours des chaînes alphanumériques de 24 caractères et se terminent toujours par `@AdobeOrg`.

## Configuration d’un `orgID` à l’aide de l’extension de balise SDK Web

Saisissez l’ID d’organisation dans le champ de texte **[!UICONTROL Identifiant de l’organisation IMS]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Saisissez l’ID d’organisation de votre choix dans le champ de texte [!UICONTROL Identifiant d’organisation IMS] près du haut.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Configuration d’un `orgID` à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la chaîne `orgId` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK Web, le SDK Web renvoie une erreur de console et les données ne sont pas envoyées à Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
