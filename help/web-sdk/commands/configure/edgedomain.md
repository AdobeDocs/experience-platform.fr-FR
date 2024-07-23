---
title: edgeDomain
description: Déterminez le domaine racine auquel vous souhaitez envoyer des données.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

La propriété `edgeDomain` vous permet de modifier le domaine dans lequel le SDK Web envoie des données. Cette propriété est fréquemment utilisée par les organisations qui utilisent des [cookies propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr). Les données sont envoyées au domaine de l’organisation, puis un enregistrement CNAME les transfère vers l’Adobe.

Votre entreprise détermine la valeur correcte de cette propriété lors de la configuration de [cookies propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr). Une organisation utilise généralement un sous-domaine dédié à cette fin. Par exemple, si vous utilisez le domaine `example.com`, vous pouvez configurer des cookies propriétaires sur `data.example.com`.

## Configuration d’un domaine Edge à l’aide de l’extension de balise SDK Web

Définissez le champ de texte **[!UICONTROL Domaine Edge]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Recherchez le champ de texte **[!UICONTROL Domaine Edge]**, puis saisissez la valeur souhaitée.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Configuration d’un domaine Edge à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la chaîne `edgeDomain` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK, elle est définie par défaut sur `edge.adobedc.net`. Définissez cette valeur si vous souhaitez remplacer le domaine auquel le SDK Web envoie des données.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```
