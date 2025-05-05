---
title: data
description: Découvrez comment envoyer des données non XDM à Adobe par le biais de l’objet de données.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

L’objet `data` vous permet d’envoyer une payload à l’Adobe qui ne correspond pas à un schéma XDM. Elle s’avère utile dans les scénarios autres que XDM, tels que l’envoi direct de données à Adobe Analytics, Adobe Target ou Adobe Audience Manager. Lorsque les données arrivent au niveau du flux de données, vous pouvez utiliser le [mappage de préparation de données](/help/data-prep/ui/mapping.md) pour affecter des champs XDM à chaque champ de l’objet `data`.

>[!IMPORTANT]
>
>Les données de cet objet doivent comporter au moins l’une des actions suivantes :
>
>* Un service de la banque de données doit être configuré pour récupérer les données d’une propriété donnée dans l’objet `data`.
>* La propriété donnée doit être mappée à un champ XDM à l’aide de la préparation des données.
>
>Si une propriété donnée n’est pas mappée à un champ XDM ou utilisée par un service configuré, ces données sont définitivement perdues.

## Utilisation de l’objet `data` via l’extension de balise du SDK Web {#tag-extension}

Fournissez un élément de données dans le champ **[!UICONTROL Data]** dans les actions d’une règle de balise.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Envoyer l’événement]**.
1. Fournissez l’élément de données contenant l’objet souhaité dans le champ **[!UICONTROL Data]**.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

## Utilisation de l’objet `data` via la bibliothèque JavaScript du SDK Web {#library}

Définissez l’objet `data` dans le cadre de l’objet JSON au sein du paramètre de la commande `sendEvent`. Pour les données que vous prévoyez de mapper dans la zone de données, vous pouvez structurer cet objet comme vous le souhaitez. Pour les données utilisées par certains services, assurez-vous que la hiérarchie d’objets correspond à ce que le service attend. Vous pouvez inclure l’objet `data` et l’objet [`xdm`](xdm.md) dans la même commande `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Utilisation de l’objet `data` avec Adobe Analytics {#analytics}

Vous pouvez utiliser l’objet `data` avec Adobe Analytics pour envoyer des données à une suite de rapports sans schéma XDM. Les variables sont configurées pour utiliser la même syntaxe que les variables [!DNL AppMeasurement], ce qui simplifie le processus de mise à niveau vers le SDK Web. Pour plus d’informations, voir [Mappage des variables d’objet de données vers Adobe Analytics](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/data-var-mapping) dans le guide de mise en oeuvre d’Adobe Analytics.
