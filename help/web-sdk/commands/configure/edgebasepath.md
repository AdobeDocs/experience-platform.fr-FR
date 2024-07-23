---
title: edgeBasePath
description: Chemin d’accès de base du point de terminaison utilisé pour interagir avec les services Adobe.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

La propriété `edgeBasePath` modifie le chemin de destination lorsque vous interagissez avec les services Adobe. La plupart des entreprises n’ont pas besoin de définir ou de modifier cette propriété.

## Chemin d’accès de base Edge à l’aide de l’extension de balise SDK Web

Saisissez le texte de votre choix dans le champ de texte **[!UICONTROL Chemin d’accès de base Edge]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Paramètres avancés], puis saisissez la valeur souhaitée dans le champ de texte **[!UICONTROL Chemin d’accès de base Edge]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Chemin d’accès de base Edge à l’aide de la bibliothèque JavaScript SDK Web

Définissez le champ de texte `edgeBasePath` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété, elle prend par défaut la valeur `ee`. Adobe recommande d’ignorer cette propriété dans la plupart des configurations.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```
