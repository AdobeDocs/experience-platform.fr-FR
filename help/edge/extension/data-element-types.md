---
title: Types d’éléments de données dans l’extension SDK Web Adobe Experience Platform
description: Découvrez les différents types d’éléments de données fournis par l’extension de balise du SDK Web de Adobe Experience Platform.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 19%

---

# Types d’éléments de données

Après avoir défini vos [types d’actions](action-types.md) dans l’ [extension de balise SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md), configurez vos types d’éléments de données.

Cette page décrit les types d’éléments de données disponibles.


## Identifiant de fusion d’événement

Lorsque cet élément de données est utilisé, il fournit un identifiant de fusion d’événements. Aucune configuration n’est nécessaire pour cet élément de données. L’élément de données fourni reste le même jusqu’à ce que le visiteur quitte la page ou jusqu’à ce que le type d’action « Réinitialiser l’identifiant de fusion d’événements » soit utilisé.

## Mappage d’identités

Une carte des identités vous permet d’établir les identités du visiteur de votre page web. Un mappage d’identité se compose d’espaces de noms, tels que _phone_ ou _email_, chaque espace de noms contenant un ou plusieurs identifiants. Par exemple, si l’individu de votre site web a fourni deux numéros de téléphone, l’espace de noms de votre téléphone doit contenir deux identifiants.

Dans l’élément de données [!UICONTROL carte des identités], vous fournissez les informations suivantes pour chaque identifiant :

* **[!UICONTROL ID]** : Valeur identifiant le visiteur. Par exemple, si l’identifiant appartient à l’espace de noms _phone_ , l’[!UICONTROL ID] peut être _555-555-5555_. Cette valeur est généralement dérivée d’une variable JavaScript ou d’un autre élément de données sur votre page. Il est donc préférable de créer un élément de données qui référence les données de la page, puis de référencer l’élément de données dans le champ [!UICONTROL ID] de l’élément de données [!UICONTROL Identité map] . Si, lors de l’exécution sur votre page, la valeur de l’identifiant est autre qu’une chaîne renseignée, l’identifiant est automatiquement supprimé de la carte d’identité.
* **[!UICONTROL État]** authentifié : Sélection indiquant si le visiteur est authentifié.
* **[!UICONTROL Principal]** : Sélection indiquant si l’identifiant doit être utilisé comme identifiant Principal de l’individu. Si aucun identifiant n’est marqué comme Principal, l’ECID est utilisé comme identifiant Principal.

Vous ne devez pas fournir d’ECID lors de la création d’une carte d’identité. Lors de l’utilisation du SDK, un ECID est automatiquement généré sur le serveur et inclus dans la carte d’identité.

L’élément de données de carte d’identité est souvent utilisé en tandem avec le type d’élément de données [[!UICONTROL Objet XDM] et le type d’action [[!UICONTROL Définir le consentement]](action-types.md#set-consent).](#xdm-object)

En savoir plus sur [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=fr).

![](./assets/identity-map-data-element.png)

## Objet XDM {#xdm-object}

Utilisez le format XDM pour envoyer des données au SDK Web de Adobe Experience Platform. Le formatage de vos données est plus facile avec l’élément de données d’objet XDM. La première fois que vous ouvrez cet élément de données, sélectionnez le sandbox et le schéma Adobe Experience Platform appropriés. Après avoir sélectionné votre schéma, vous voyez la structure de votre schéma, que vous pouvez facilement remplir.

![](./assets/XDM-object.png)

Notez que lorsque vous ouvrez certains champs de votre schéma, tels que `web.webPageDetails.URL`, certains éléments sont automatiquement collectés. Même si plusieurs éléments sont collectés automatiquement, vous pouvez en remplacer certains, si nécessaire. Toutes les valeurs peuvent être renseignées manuellement ou en utilisant d’autres éléments de données.

>[!NOTE]
>
>Renseignez uniquement les informations que vous souhaitez recueillir. Tout ce qui n’est pas renseigné est omis lorsque les données sont envoyées aux solutions.
