---
title: orgId
description: La propriété orgId est une chaîne qui indique à Adobe à quelle organisation ces données sont envoyées.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

La propriété `orgId` est une chaîne qui indique à Adobe à quelle organisation les données sont envoyées. **Cette propriété est requise pour toutes les données envoyées à l’aide de Web SDK.**

Pour localiser votre `orgID` :

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. N’importe où dans le Adobe Experience Cloud, appuyez sur **`[Ctrl]`** + **`[I]`**. Une fenêtre de [!UICONTROL User Data Debugger] s’ouvre.
1. Cliquez sur **[!UICONTROL Copy]** ![Copier](../../assets/copy.png) en regard de la [!UICONTROL Current Org ID], ou cliquez sur l’onglet **[!UICONTROL Assigned Orgs]** pour afficher d’autres ID d’organisation auxquels vous pouvez accéder.
1. Lorsque vous avez fini de localiser les informations souhaitées, cliquez sur **[!UICONTROL Close]**.

Les identifiants d’organisation sont toujours des chaînes alphanumériques de 24 caractères et se terminent toujours par `@AdobeOrg`.

Définissez la chaîne de `orgId` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, Web SDK renvoie une erreur de console et les données ne sont pas envoyées à Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## Définir l’ID d’organisation à l’aide de l’extension de balise Web SDK

Ce paramètre peut être configuré dans l’extension de balise Web SDK à l’aide des paramètres de configuration de l’instance SDK [](/help/tags/extensions/client/web-sdk/configure/general.md). Le champ est automatiquement renseigné en fonction de l’organisation sous laquelle la propriété de balise a été créée.
