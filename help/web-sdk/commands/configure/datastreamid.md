---
title: datastreamId
description: Déterminez l’identifiant de flux de données auquel vous souhaitez envoyer des données.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# `datastreamId`

La propriété `datastreamId` est une chaîne qui détermine à quel [datastream](../../../datastreams/overview.md) dans Adobe Experience Platform vous souhaitez envoyer des données. Cette propriété est requise lors de l’envoi de données à Adobe. Les versions 2.20.0 ou antérieures du SDK Web utilisent `edgeConfigId` à la place.

Pour localiser un identifiant de flux de données :

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Datastreams]**.
1. Utilisez le champ de recherche pour localiser la banque de données souhaitée, puis sélectionnez **[!UICONTROL Copier]** ![Copier](../../assets/copy.png) en regard de l’ID de la banque de données.

Vous pouvez également sélectionner le nom de la banque de données de votre choix et l’identifiant de la banque de données apparaît dans la colonne de droite pour que vous puissiez le copier.

## Sélectionnez l’identifiant de la banque de données à l’aide de l’extension de balise SDK Web.

Faites votre choix dans une liste de jeux de données disponibles ou saisissez un identifiant de flux de données directement lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Recherchez la section [!UICONTROL Datastreams] , puis sélectionnez la méthode souhaitée pour déterminer le flux de données.
   * Si vous effectuez un choix dans une liste, sélectionnez l’environnement de test et le flux de données dans chaque liste déroulante correspondante.
   * Si vous saisissez des valeurs, saisissez l’identifiant de la banque de données de votre choix.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

Vous pouvez envoyer des données à différents groupes de données pour des environnements de balises de production, d’évaluation et de développement.

## Sélectionner l’identifiant de la banque de données à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la propriété de chaîne `datastreamID` lors de l’exécution de la commande `configure`. Cette propriété est requise pour toutes les mises en oeuvre du SDK Web. Si vous omettez cette propriété, le SDK Web ne sait pas à quel flux de données envoyer les données, ce qui entraîne la perte définitive de ces données.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Si vous configurez plusieurs instances du SDK Web sur une seule page, vous devez configurer un `datastreamId` différent pour chaque instance.
