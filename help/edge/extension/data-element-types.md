---
title: Types d’éléments de données dans l’extension SDK Web Adobe Experience Platform
description: Découvrez les différents types d’éléments de données fournis par l’extension de balise du SDK Web de Adobe Experience Platform.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 13912d8f5488aaa9ffa79021b67607fe5eec0732
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 6%

---


# Types d’éléments de données

Après avoir défini votre [types d’actions](action-types.md) dans le [Extension de balise SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md), vous devez configurer vos types d’éléments de données. Cette page décrit les types d’éléments de données disponibles.

## Mappage d’identités {#identity-map}

Une carte des identités vous permet d’établir les identités du visiteur de votre page web. Un mappage d’identité se compose d’espaces de noms, tels que _phone_ ou _email_, avec chaque espace de noms contenant un ou plusieurs identifiants. Par exemple, si l’individu de votre site web a fourni deux numéros de téléphone, l’espace de noms de votre téléphone doit contenir deux identifiants.

Dans le [!UICONTROL Mappage d’identités] vous fournissez les informations suivantes pour chaque identifiant :

* **[!UICONTROL ID]**: Valeur identifiant le visiteur. Par exemple, si l’identifiant appartient à la variable _phone_ l’espace de noms, [!UICONTROL ID] may _555-555-5555_. Cette valeur est généralement dérivée d’une variable JavaScript ou d’un autre élément de données sur votre page. Il est donc préférable de créer un élément de données qui référence les données de la page, puis de référencer l’élément de données dans la variable [!UICONTROL ID] dans le champ [!UICONTROL Mappage d’identités] élément de données. Si, lors de l’exécution sur votre page, la valeur de l’identifiant est autre qu’une chaîne renseignée, l’identifiant est automatiquement supprimé de la carte d’identité.
* **[!UICONTROL État authentifié]**: Sélection indiquant si le visiteur est authentifié.
* **[!UICONTROL Principal]**: Sélection indiquant si l’identifiant doit être utilisé comme identifiant Principal de l’individu. Si aucun identifiant n’est marqué comme Principal, l’ECID est utilisé comme identifiant Principal.

![Image de l’interface utilisateur affichant l’écran Modifier l’élément de données .](./assets/identity-map-data-element.png)

Vous ne devez pas fournir un [!DNL ECID] lors de la création d’une carte d’identité. Lors de l’utilisation du SDK, une [!DNL ECID] est généré automatiquement sur le serveur et inclus dans la carte des identités.

L’élément de données de carte d’identité est souvent utilisé conjointement avec la variable [[!UICONTROL Objet XDM] type d’élément de données](#xdm-object) et le [[!UICONTROL Définition du consentement] type d&#39;action](action-types.md#set-consent).

En savoir plus sur [Service Adobe Experience Platform Identity](../../identity-service/home.md).

## Objet XDM {#xdm-object}

Le formatage de vos données en XDM est plus facile avec l’élément de données de l’objet XDM. La première fois que vous ouvrez cet élément de données, sélectionnez le sandbox et le schéma Adobe Experience Platform appropriés. Après avoir sélectionné votre schéma, vous voyez la structure de votre schéma, que vous pouvez facilement remplir.

![Image de l’interface utilisateur montrant la structure de l’objet XDM.](assets/XDM-object.png)

Notez que lorsque vous ouvrez certains champs de votre schéma, tels que `web.webPageDetails.URL`, certains éléments sont automatiquement collectés. Même si plusieurs éléments sont collectés automatiquement, vous pouvez en remplacer certains, si nécessaire. Toutes les valeurs peuvent être renseignées manuellement ou en utilisant d’autres éléments de données.

>[!NOTE]
>
>Renseignez uniquement les informations que vous souhaitez recueillir. Tout ce qui n’est pas renseigné est omis lorsque les données sont envoyées aux solutions.

## Variable {#variable}

>[!IMPORTANT]
>
>Il s’agit actuellement d’une fonctionnalité bêta qui peut être modifiée. Les versions futures peuvent contenir des modifications entraînant des ruptures.

Une autre méthode de création d’objets XDM consiste à utiliser la propriété **[!UICONTROL Variable]** élément de données. Bien que l’élément de données de l’objet XDM soit créé lorsqu’il est référencé, par exemple dans une balise `sendEvent` , la commande **[!UICONTROL Variable]** l’élément de données peut être mis à jour via [!UICONTROL Mettre à jour la variable] actions. Pour utiliser l’élément de données, sélectionnez l’environnement de test et le schéma Adobe Experience Platform appropriés.

![Image de l’interface utilisateur affichant l’écran Créer un élément de données .](assets/variable-data-element.png)

Une fois que vous avez créé cet élément de données, vous pouvez utiliser [Mettre à jour la variable](./action-types.md#update-variable) actions permettant de modifier l’élément de données. Ensuite, dans les actions d’événement d’envoi, utilisez l’élément de données de variable pour l’option XDM.

## Étapes suivantes {#next-steps}

En savoir plus sur des cas d’utilisation spécifiques, tels que [accès à l’ECID](accessing-the-ecid.md).
