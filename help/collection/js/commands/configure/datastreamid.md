---
title: datastreamId
description: Déterminez l’identifiant du flux de données auquel vous souhaitez envoyer des données.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---

# `datastreamId`

La propriété `datastreamId` est une chaîne qui détermine le [flux de données](/help/datastreams/overview.md) dans Adobe Experience Platform auquel vous souhaitez envoyer des données. Cette propriété est requise lors de l’envoi de données à Adobe. Les versions 2.20.0 ou antérieures de Web SDK utilisent `edgeConfigId` à la place.

Pour localiser un identifiant de flux de données :

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Utilisez le champ de recherche pour localiser le flux de données de votre choix, puis sélectionnez **[!UICONTROL Copy]** ![Copier](../../assets/copy.png) en regard de l’identifiant du flux de données.

Vous pouvez également sélectionner le nom du flux de données de votre choix et l’identifiant du flux de données s’affiche dans la colonne de droite pour que vous puissiez le copier.

## Exemple de code

Définissez la propriété de chaîne `datastreamID` lors de l’exécution de la commande `configure`. Cette propriété est requise pour toutes les implémentations de Web SDK. Si vous omettez cette propriété, le SDK Web ne sait pas à quel flux de données envoyer des données, ce qui entraîne la perte définitive de ces données.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>Si vous configurez plusieurs instances de Web SDK sur une seule page, vous devez configurer un `datastreamId` différent pour chaque instance.

## Sélectionnez l’identifiant du flux de données à l’aide de l’extension de balise Web SDK

Consultez [&#x200B; Paramètres de configuration des flux de données &#x200B;](/help/tags/extensions/client/web-sdk/configure/datastreams.md) dans la documentation de l’extension de balise Web SDK pour savoir comment définir le flux de données souhaité pour chaque environnement à l’aide de balises. Vous pouvez envoyer des données à différents flux de données pour les environnements de balises de production, d’évaluation et de développement.
