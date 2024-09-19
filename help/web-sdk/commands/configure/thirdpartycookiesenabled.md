---
title: thirdPartyCookiesEnabled
description: Permet l’utilisation de cookies tiers pour identifier les visiteurs.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

La propriété `thirdPartyCookiesEnabled` est une valeur booléenne qui détermine si le SDK Web définit les cookies dans un contexte tiers. L’activation de cette option s’avère utile si vous souhaitez identifier les visiteurs entre les sous-domaines ou les domaines dont votre entreprise est propriétaire. Cependant, de nombreux navigateurs modernes limitent la définition et l’expiration des cookies tiers.

La propriété `thirdPartyCookiesEnabled` contrôle également si un [`CORE ID`](../../identity/overview.md#tracking-coreid-web-sdk) peut être demandé sur des appels [`getIdentity`](../getidentity.md).

Lorsque cette option est activée, le SDK Web utilise Adobe Audience Manager pour identifier un visiteur. Lorsque cette option est désactivée, l’appel à l’Audience Manager est désactivé. Pour plus d’informations, voir [Comprendre les appels au domaine Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=fr) dans le guide d’utilisation de l’Audience Manager.

## Activation des cookies tiers à l’aide de l’extension de balise SDK Web

Cochez la case **[!UICONTROL Utiliser des cookies tiers]** lors de la [ configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Identité], puis cochez la case **[!UICONTROL Utiliser des cookies tiers]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Activation des cookies tiers à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la valeur booléenne `thirdPartyCookiesEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `true`. Définissez cette valeur sur `false` si vous ne souhaitez pas que le SDK Web utilise l’Audience Manager pour identifier les visiteurs.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```
