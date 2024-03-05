---
title: orgId
description: La propriété orgId est une chaîne qui indique à l’Adobe à quelle organisation les données sont envoyées.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

La variable `orgId` est une chaîne qui indique à l’Adobe à quelle organisation les données sont envoyées. **Cette propriété est requise pour toutes les données envoyées à l’aide du SDK Web.**

Pour localiser votre `orgID`:

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. N’importe où dans Adobe Experience Cloud, appuyez sur **`[Ctrl]`** + **`[I]`**. A [!UICONTROL Débogueur de données utilisateur] s’ouvre.
1. Cliquez sur **[!UICONTROL Copier]** ![Copier](../../assets/copy.png) en regard de [!UICONTROL ID d’organisation actuel]ou cliquez sur le bouton **[!UICONTROL Organisation affectée]** pour afficher d’autres ID d’organisation auxquels vous avez accès.
1. Lorsque vous avez terminé de trouver les informations souhaitées, cliquez sur **[!UICONTROL Fermer]**.

Les identifiants d’organisation sont toujours des chaînes alphanumériques de 24 caractères et se terminent toujours par `@AdobeOrg`.

## Configurez une `orgID` utilisation de l’extension de balise SDK Web

Saisissez l’ID d’organisation dans la variable **[!UICONTROL Identifiant de l’organisation IMS]** Champ de texte lorsque [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Saisissez l’ID d’organisation de votre choix dans le [!UICONTROL Identifiant de l’organisation IMS] Champ de texte près du haut.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Configurez une `orgID` utilisation de la bibliothèque JavaScript SDK Web

Définissez la variable `orgId` chaîne lors de l’exécution de la variable `configure` . Si vous omettez cette propriété lors de la configuration du SDK Web, le SDK Web renvoie une erreur de console et les données ne sont pas envoyées à Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
