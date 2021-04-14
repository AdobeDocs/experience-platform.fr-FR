---
title: Types d’éléments de données dans l’extension Adobe Experience Platform Web SDK
description: Découvrez les différents types d’éléments de données fournis par l’extension Adobe Experience Platform Web SDK à Adobe Experience Platform Launch.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
translation-type: tm+mt
source-git-commit: 3f7808a08d033c5940d2115006c269b8c4079822
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 47%

---

# Types d’éléments de données

Après avoir défini vos [types d’action](action-types.md) dans l’[extension du SDK Web de Adobe Experience Platform](web-sdk-extension.md) pour [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configurez vos types d’éléments de données.

Cette page décrit les types d’éléments de données disponibles.

## Identifiant de fusion d’événement

Lorsque cet élément de données est utilisé, il fournit un identifiant de fusion d’événements. Aucune configuration n’est nécessaire pour cet élément de données. L’élément de données fourni reste le même jusqu’à ce que le visiteur quitte la page ou jusqu’à ce que le type d’action « Réinitialiser l’identifiant de fusion d’événements » soit utilisé.

## Mappage d’identités

L’élément de données de carte Identité vous permet de créer des identités à partir d’autres éléments de données ou d’autres valeurs que vous spécifiez. Toutes les identités que vous créez doivent être liées à un espace de noms correspondant. Cet élément de données fournit une liste déroulante qui affiche tous les espaces de nommage par défaut, ainsi que tous ceux que vous avez créés.

![](./assets/identity-map-data-element.png)

## Objet XDM {#xdm-object}

Utilisez le format XDM pour envoyer toutes les données au Adobe Experience Platform Web SDK. Le formatage de vos données est plus facile avec l’élément de données d’objet XDM. La première fois que vous ouvrez cet élément de données, sélectionnez le sandbox et le schéma Adobe Experience Platform appropriés. Après avoir sélectionné votre schéma, vous voyez la structure de votre schéma, que vous pouvez facilement remplir.

![](./assets/XDM-object.png)

Veuillez noter que lorsque vous ouvrez certains champs de votre schéma, par exemple `web.webPageDetails.URL`, certains éléments sont automatiquement collectés. Bien que plusieurs éléments soient automatiquement collectés, vous pouvez en remplacer certains, si nécessaire. Toutes les valeurs peuvent être renseignées manuellement ou en utilisant d’autres éléments de données.

>[!NOTE]
>
>Renseignez uniquement les informations que vous souhaitez recueillir. Tout élément non renseigné est omis lorsque les données sont envoyées aux solutions.
