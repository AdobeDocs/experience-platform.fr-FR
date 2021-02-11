---
title: Types d’éléments de données de l’extension SDK Web Platform
description: Adobe Experience Platform Web SDK Extension Data Element Types dans Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 81%

---


# Types d’élément de données

Après avoir défini vos [types d’action](action-types.md) dans l’[extension du SDK Web de Adobe Experience Platform](web-sdk-extension.md) pour [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configurez vos types d’éléments de données.

Cette page décrit les types d’éléments de données disponibles.

## Identifiant de fusion d’événement

Lorsque cet élément de données est utilisé, il fournit un identifiant de fusion d’événements. Aucune configuration n’est nécessaire pour cet élément de données. L’élément de données fourni reste le même jusqu’à ce que le visiteur quitte la page ou jusqu’à ce que le type d’action « Réinitialiser l’identifiant de fusion d’événements » soit utilisé.

## Mappage d’identités

L’élément de données de carte Identité vous permet de créer des identités à partir d’autres éléments de données ou d’autres valeurs que vous spécifiez. Toutes les identités que vous créez doivent être liées à un espace de noms correspondant. Cet élément de données présente une liste déroulante qui affiche tous les espaces de noms par défaut, ainsi que tous ceux que vous avez créés.

![](./assets/identity-map-data-element.png)

## Objet XDM

Toutes les données envoyées au SDK Web Adobe Experience Platform doivent être au format XDM. Le formatage de vos données est plus facile avec l’élément de données d’objet XDM. La première fois que vous ouvrez cet élément de données, sélectionnez le sandbox et le schéma Adobe Experience Platform appropriés. Quand vous aurez sélectionné votre schéma, vous en verrez la structure et vous pourrez facilement la compléter.

![](./assets/XDM-object.png)

Veuillez noter que lorsque vous ouvrez certains champs de votre schéma, par exemple `web.webPageDetails.URL`, certains éléments sont automatiquement collectés. Bien que plusieurs éléments soient automatiquement collectés, vous avez la possibilité de les remplacer, si nécessaire. Toutes les valeurs peuvent être renseignées manuellement ou en utilisant d’autres éléments de données.

>[!NOTE]
>
>Vous n’avez qu’à remplir les renseignements que vous souhaitez recueillir. Tout ce qui n’est pas renseigné sera omis lorsque les données seront envoyées aux solutions.
