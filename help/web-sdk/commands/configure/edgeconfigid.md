---
title: edgeConfigId
description: Déterminez l’identifiant de flux de données auquel vous souhaitez envoyer des données.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

La variable `edgeConfigId` est une chaîne qui détermine laquelle [datastream](../../../datastreams/overview.md) dans Adobe Experience Platform, vous souhaitez envoyer des données. Cette propriété est requise lors de l’envoi de données à Adobe.

Pour localiser un identifiant de flux de données :

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Datastreams]**.
1. Utilisez le champ de recherche pour localiser le flux de données souhaité, puis sélectionnez **[!UICONTROL Copier]** ![Copier](../../assets/copy.png) en regard de l’identifiant de la banque de données.

Vous pouvez également sélectionner le nom de la banque de données de votre choix. L’identifiant de la banque de données apparaît dans la colonne de droite pour que vous puissiez le copier.

## Sélectionnez l’identifiant de la banque de données à l’aide de l’extension de balise SDK Web.

Effectuez un choix parmi une liste de jeux de données disponibles ou saisissez un identifiant de flux de données directement lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Recherchez la variable [!UICONTROL Datastreams] , puis sélectionnez la méthode souhaitée pour déterminer le flux de données.
   * Si vous effectuez un choix dans une liste, sélectionnez l’environnement de test et le flux de données dans chaque liste déroulante correspondante.
   * Si vous saisissez des valeurs, saisissez l’identifiant de la banque de données de votre choix.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

Vous pouvez envoyer des données à différents groupes de données pour des environnements de balises de production, d’évaluation et de développement.

## Sélectionnez l’identifiant de la banque de données à l’aide de la bibliothèque JavaScript du SDK Web.

Définissez la variable `edgeConfigId` propriété de chaîne lors de l’exécution de la propriété `configure` . Cette propriété est requise pour toutes les mises en oeuvre du SDK Web. Si vous omettez cette propriété, le SDK Web ne sait pas à quel flux de données envoyer les données, ce qui entraîne la perte définitive de ces données.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Si vous configurez plusieurs instances du SDK Web sur une seule page, vous devez configurer un `edgeConfigId` pour chaque instance.
