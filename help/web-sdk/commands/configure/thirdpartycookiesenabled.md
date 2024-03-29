---
title: thirdPartyCookiesEnabled
description: Permet l’utilisation de cookies tiers pour identifier les visiteurs.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

>[!IMPORTANT]
>
>Google [hasannonce](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) prévoit d’interrompre la prise en charge des cookies tiers par Chrome au cours du deuxième semestre 2024. Par conséquent, les cookies tiers ne seront plus pris en charge dans aucun des principaux navigateurs.
>
>Une fois cette modification mise en oeuvre, l’Adobe arrêtera la prise en charge de la variable `demdex` cookie actuellement pris en charge dans le SDK Web.


La variable `thirdPartyCookiesEnabled` est une valeur booléenne qui détermine si le SDK Web définit les cookies dans un contexte tiers. L’activation de cette option s’avère utile si vous souhaitez identifier les visiteurs entre les sous-domaines ou les domaines dont votre entreprise est propriétaire. Cependant, de nombreux navigateurs modernes limitent la définition et l’expiration des cookies tiers.

Lorsque cette option est activée, le SDK Web utilise Adobe Audience Manager pour identifier un visiteur. Lorsque cette option est désactivée, l’appel à l’Audience Manager est désactivé. Voir [Signification des appels vers le domaine Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=fr) pour plus d’informations, voir le guide d’utilisation d’Audience Manager .

## Activation des cookies tiers à l’aide de l’extension de balise SDK Web

Sélectionnez la variable **[!UICONTROL Utilisation de cookies tiers]** , [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Identité] , puis cochez la case **[!UICONTROL Utilisation de cookies tiers]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Activation des cookies tiers à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `thirdPartyCookiesEnabled` booléen lors de l’exécution de la variable `configure` . Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `true`. Définissez cette valeur sur `false` si vous ne souhaitez pas que le SDK Web utilise l’Audience Manager pour identifier les visiteurs.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
