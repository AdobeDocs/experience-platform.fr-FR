---
title: data
description: Découvrez comment envoyer des données non XDM à Adobe.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# data

La variable `data` vous permet d’envoyer des données à un Adobe qui ne correspond pas à un schéma XDM. Elle est utile dans les scénarios autres que XDM, comme la mise à jour d’une [Profil Adobe Target](/help/web-sdk/personalization/adobe-target/target-overview.md). Lorsque les données arrivent à l’Adobe, vous pouvez utiliser l’outil de mappage de flux de données pour affecter des champs XDM à chaque champ dans la variable `data` .

>[!IMPORTANT]
>
>Les données de cette propriété doivent comporter au moins l’une des actions suivantes :
>
>* Un service de la banque de données doit être configuré pour récupérer les données d’une propriété spécifique dans la variable `data` objet
>* Chaque propriété doit être mappée à un champ XDM.
>
>Si un champ donné n’est pas mappé à un champ XDM ou utilisé par un service configuré, ces données sont définitivement perdues.

## Utilisation de la propriété data à l’aide de l’extension de balise du SDK Web

Fournissez un élément de données dans la variable **[!UICONTROL Données]** dans les actions d’une règle de balise.

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Envoyer un événement]**.
1. Fournissez l’élément de données contenant l’objet souhaité dans la variable **[!UICONTROL Données]** champ .
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

## Utilisation de la propriété data à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `data` faisant partie de l’objet JSON dans le paramètre de la propriété `sendEvent` . Pour les données que vous prévoyez de mapper dans la zone de données, vous pouvez structurer cette propriété comme vous le souhaitez. Pour les données utilisées par certains services, assurez-vous que la hiérarchie d’objets correspond à ce que le service attend. Vous pouvez inclure les `data` et la variable [`xdm`](xdm.md) dans le même objet `sendEvent` .

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
