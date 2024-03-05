---
title: edgeDomain
description: Déterminez le domaine racine auquel vous souhaitez envoyer des données.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

La variable `edgeDomain` vous permet de modifier le domaine dans lequel le SDK Web envoie des données. Cette propriété est fréquemment utilisée par les organisations qui utilisent [cookies propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr). Les données sont envoyées au domaine de l’organisation, puis un enregistrement CNAME les transfère vers l’Adobe.

Votre entreprise détermine la valeur correcte de cette propriété lors de la configuration. [cookies propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr). Une organisation utilise généralement un sous-domaine dédié à cette fin. Par exemple, si vous utilisez le domaine `example.com`, vous pouvez configurer des cookies propriétaires sur `data.example.com`.

## Configuration d’un domaine Edge à l’aide de l’extension de balise SDK Web

Définissez la variable **[!UICONTROL Domaine Edge]** Champ de texte lorsque [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Localisation du champ de texte **[!UICONTROL Domaine Edge]**, puis saisissez la valeur souhaitée.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Configuration d’un domaine Edge à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `edgeDomain` chaîne lors de l’exécution de la variable `configure` . Si vous omettez cette propriété lors de la configuration du SDK, elle est définie par défaut sur `edge.adobedc.net`. Définissez cette valeur si vous souhaitez remplacer le domaine auquel le SDK Web envoie des données.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
