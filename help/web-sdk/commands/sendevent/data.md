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

La variable `data` vous permet d’envoyer une payload à un Adobe qui ne correspond pas à un schéma XDM. Elle s’avère utile dans les scénarios autres que XDM, tels que l’envoi direct de données à Adobe Analytics, Adobe Target ou Adobe Audience Manager. Lorsque des données arrivent au niveau du flux de données, vous pouvez utiliser [Mappage de la préparation des données](/help/data-prep/ui/mapping.md) pour affecter des champs XDM à chaque champ dans `data` .

>[!IMPORTANT]
>
>Les données de cet objet doivent comporter au moins l’une des actions suivantes :
>
>* Un service dans le flux de données doit être configuré pour récupérer les données d’une propriété donnée dans la variable `data` .
>* La propriété donnée doit être mappée à un champ XDM à l’aide de la préparation des données.
>
>Si une propriété donnée n’est pas mappée à un champ XDM ou utilisée par un service configuré, ces données sont définitivement perdues.

## Utilisez la variable `data` par le biais de l’extension de balise SDK Web {#tag-extension}

Fournissez un élément de données dans la variable **[!UICONTROL Données]** dans les actions d’une règle de balise.

1. Connexion à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Envoyer un événement]**.
1. Fournissez l’élément de données contenant l’objet souhaité dans la variable **[!UICONTROL Données]** champ .
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

## Utilisez la variable `data` par le biais de la bibliothèque JavaScript du SDK Web {#library}

Définissez la variable `data` faisant partie de l’objet JSON dans le paramètre de la fonction `sendEvent` . Pour les données que vous prévoyez de mapper dans la zone de données, vous pouvez structurer cet objet comme vous le souhaitez. Pour les données utilisées par certains services, assurez-vous que la hiérarchie d’objets correspond à ce que le service attend. Vous pouvez inclure les `data` et la variable [`xdm`](xdm.md) dans le même objet `sendEvent` .

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Utilisez la variable `data` avec Adobe Analytics {#analytics}

Vous pouvez utiliser la variable `data` avec Adobe Analytics pour envoyer des données à une suite de rapports sans schéma XDM. Les variables sont configurées pour utiliser la même syntaxe que [!DNL AppMeasurement] , ce qui simplifie le processus de mise à niveau vers le SDK Web. Voir [Mappage des variables d’objet de données vers Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) pour plus d’informations, voir le guide de mise en oeuvre d’Adobe Analytics .
