---
title: edgeBasePath
description: Chemin d’accès de base du point de terminaison utilisé pour interagir avec les services Adobe.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

La variable `edgeBasePath` modifie le chemin de destination lorsque vous interagissez avec les services Adobe. La plupart des entreprises n’ont pas besoin de définir ou de modifier cette propriété.

## Chemin d’accès de base Edge à l’aide de l’extension de balise SDK Web

Entrez le texte de votre choix dans la **[!UICONTROL Chemin de base Edge]** Champ de texte lorsque [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Paramètres avancés] , puis entrez la valeur souhaitée dans la variable **[!UICONTROL Chemin de base Edge]** Champ de texte.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Chemin d’accès de base Edge à l’aide de la bibliothèque JavaScript SDK Web

Définissez la variable `edgeBasePath` Champ de texte lors de l’exécution de la variable `configure` . Si vous omettez cette propriété, elle prend par défaut la valeur `ee`. Adobe recommande d’ignorer cette propriété dans la plupart des configurations.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
