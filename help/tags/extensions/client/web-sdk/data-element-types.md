---
title: Types d’éléments de données dans l’extension Adobe Experience Platform Web SDK
description: Découvrez les différents types d’éléments de données fournis par l’extension de balises Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 8cb8dcf7217440da98f6856293c530a66d4c3444
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 5%

---

# Types d’éléments de données

Après avoir défini vos [types d’action](actions/actions-overview.md) dans l’extension de balise, vous devez configurer vos types d’éléments de données. Cette page décrit les types d’éléments de données disponibles.

## Mappage d’identités {#identity-map}

Un mappage d’identités vous permet d’établir des identités pour le visiteur de votre page web. Un mappage d’identités se compose d’espaces de noms, tels que `CRMID`, `Phone` ou `Email`, chaque espace de noms contenant un ou plusieurs identifiants. Par exemple, si la personne sur votre site web a fourni deux numéros de téléphone, votre espace de noms de téléphone doit contenir deux identifiants.

Dans l’élément de données [!UICONTROL Identity map], vous fournissez les informations suivantes pour chaque identifiant :

* **[!UICONTROL ID]** : valeur identifiant le visiteur. Par exemple, si l’identifiant appartient à l’espace de noms _phone_, le [!UICONTROL ID] peut être _555-555-5555_. Cette valeur est généralement dérivée d’une variable JavaScript ou d’un autre élément de données sur votre page. Il est donc préférable de créer un élément de données qui référence les données de la page, puis de référencer l’élément de données dans le champ [!UICONTROL ID] de l’élément de données [!UICONTROL Identity map]. Si, lors de l’exécution sur votre page, la valeur de l’identifiant est autre chose qu’une chaîne renseignée, l’identifiant sera automatiquement supprimé du mappage d’identité.
* **[!UICONTROL Authenticated state]** : sélection indiquant si le visiteur est authentifié.
* **[!UICONTROL Primary]** : sélection indiquant si l’identifiant doit être utilisé comme identifiant principal pour l’individu. Si aucun identifiant n’est marqué comme principal, l’ECID est utilisé comme identifiant principal.

![Image de l’interface utilisateur affichant l’écran Modifier l’élément de données.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe recommande d’envoyer des identités qui représentent une personne, telles que `Luma CRM Id` comme identité principale.
>
>Si la carte des identités contient l’identifiant de personne (par exemple, `Luma CRM Id`), l’identifiant de personne devient l’identifiant principal. Dans le cas contraire, `ECID` devient l’identité principale.

Vous ne devez pas fournir de [!DNL ECID] lors de la création d’un mappage d’identités. Lors de l’utilisation du SDK, un [!DNL ECID] est automatiquement généré sur le serveur et inclus dans le mappage d’identité.

L’élément de données de mappage d’identités est souvent utilisé avec l’élément de données [[!UICONTROL Variable]](#variable) et l’action [[!UICONTROL Set consent]](actions/set-consent.md).

En savoir plus sur le service Adobe Experience Platform Identity [&#128279;](/help/identity-service/home.md).

## Objet XDM {#xdm-object}

Le formatage de vos données à XDM est plus facile avec l’élément de données d’objet XDM. La première fois que vous ouvrez cet élément de données, sélectionnez le sandbox et le schéma Adobe Experience Platform appropriés. Après avoir sélectionné votre schéma, vous voyez la structure de votre schéma, que vous pouvez facilement remplir.

![Image de l’interface utilisateur affichant la structure de l’objet XDM.](assets/XDM-object.png)

Notez que lorsque vous ouvrez certains champs de votre schéma, tels que `web.webPageDetails.URL`, certains éléments sont automatiquement collectés. Bien que plusieurs éléments soient automatiquement collectés, vous pouvez les remplacer, si nécessaire. Toutes les valeurs peuvent être renseignées manuellement ou en utilisant d’autres éléments de données.

>[!NOTE]
>
>Ne renseignez que les informations que vous souhaitez recueillir. Tout élément non renseigné est omis lorsque les données sont envoyées aux solutions .

## Variable {#variable}

Vous pouvez créer des objets de payload à l’aide de l’élément de données **[!UICONTROL Variable]**. Les objets [!UICONTROL XDM] et [!UICONTROL Data] sont pris en charge.

* Lorsque vous sélectionnez [!UICONTROL XDM], sélectionnez les [!UICONTROL Sandbox] et [!UICONTROL Schema] de votre choix.
* Lorsque vous sélectionnez [!UICONTROL Data], sélectionnez les solutions de votre choix. Les solutions disponibles comprennent le [!UICONTROL Adobe Analytics] et le [!UICONTROL Adobe Target].

![Image de l’interface utilisateur des balises affichant les options de l’élément de données.](assets/variable-data-element.png)

Après avoir créé cet élément de données, vous pouvez utiliser l’action [Mettre à jour la variable](actions/update-variable.md) pour le modifier. Une fois prêt, vous pouvez inclure cet élément de données dans l’action [Envoyer l’événement](actions/send-event.md) pour envoyer des données à un flux de données.

## Média : qualité de l’expérience {#quality-experience}

Un élément de données **[!UICONTROL Quality of Experience]** est utile lors de l’envoi d’événements de streaming multimédia à Adobe Experience Platform. Vous pouvez ajouter cet élément lors de la création d’une session multimédia et les événements multimédia suivants contiendront des données de qualité d’expérience mises à jour.

![Image de l’interface utilisateur affichant l’écran Créer une qualité d’élément de données d’expérience &#x200B;](assets/qoe-data-element.png).

## Étapes suivantes {#next-steps}

Découvrez les cas d’utilisation spécifiques, tels que l’[accès à l’ECID](accessing-the-ecid.md).
