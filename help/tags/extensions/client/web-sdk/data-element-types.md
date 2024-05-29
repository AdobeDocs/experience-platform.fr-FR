---
title: Types d’éléments de données dans l’extension SDK Web Adobe Experience Platform
description: Découvrez les différents types d’éléments de données fournis par l’extension de balise du SDK Web de Adobe Experience Platform.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: fbca8a47c500e89d82cf636e8cb639f2bb59c2e6
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---


# Types d’éléments de données

Après avoir défini votre [types d’actions](action-types.md) dans le [Extension de balise SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md), vous devez configurer vos types d’éléments de données. Cette page décrit les types d’éléments de données disponibles.

## Mappage d’identités {#identity-map}

Une carte des identités vous permet d’établir les identités du visiteur de votre page web. Un mappage d’identité se compose d’espaces de noms, tels que `CRMID`, `Phone` ou `Email`, avec chaque espace de noms contenant un ou plusieurs identifiants. Par exemple, si l’individu de votre site web a fourni deux numéros de téléphone, l’espace de noms de votre téléphone doit contenir deux identifiants.

Dans le [!UICONTROL Mappage d’identité] Data, vous fournissez les informations suivantes pour chaque identifiant :

* **[!UICONTROL ID]**: valeur qui identifie le visiteur. Par exemple, si l’identifiant appartient à la variable _phone_ l’espace de noms, [!UICONTROL ID] may _555-555-5555_. Cette valeur est généralement dérivée d’une variable JavaScript ou d’un autre élément de données sur votre page. Il est donc préférable de créer un élément de données qui référence les données de la page, puis de référencer l’élément de données dans la variable [!UICONTROL ID] dans le champ [!UICONTROL Mappage d’identité] élément de données. Si, lors de l’exécution sur votre page, la valeur de l’identifiant est autre qu’une chaîne renseignée, l’identifiant est automatiquement supprimé de la carte d’identité.
* **[!UICONTROL État authentifié]**: sélection indiquant si le visiteur est authentifié.
* **[!UICONTROL Principal]**: sélection indiquant si l’identifiant doit être utilisé comme identifiant principal de l’individu. Si aucun identifiant n’est marqué comme principal, l’ECID est utilisé comme identifiant principal.

![Image de l’interface utilisateur affichant l’écran Modifier l’élément de données .](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe recommande d’envoyer des identités représentant une personne, telles que `Luma CRM Id` comme identité principale.
>
>Si la carte d’identité contient l’identifiant de personne (par exemple, `Luma CRM Id`), l’identifiant de personne deviendra l’identifiant principal. Sinon, `ECID` devient l’identité principale.

Vous ne devez pas fournir un [!DNL ECID] lors de la création d’une carte d’identité. Lors de l’utilisation du SDK, une [!DNL ECID] est généré automatiquement sur le serveur et inclus dans la carte des identités.

L’élément de données de carte d’identité est souvent utilisé conjointement avec la variable [[!UICONTROL Objet XDM] type d’élément de données](#xdm-object) et la variable [[!UICONTROL Définition du consentement] type d&#39;action](action-types.md#set-consent).

En savoir plus sur [Service Adobe Experience Platform Identity](../../../../identity-service/home.md).

## Objet XDM {#xdm-object}

Le formatage de vos données en XDM est plus facile avec l’élément de données de l’objet XDM. La première fois que vous ouvrez cet élément de données, sélectionnez le sandbox et le schéma Adobe Experience Platform appropriés. Après avoir sélectionné votre schéma, vous voyez la structure de votre schéma, que vous pouvez facilement remplir.

![Image de l’interface utilisateur montrant la structure de l’objet XDM.](assets/XDM-object.png)

Notez que lorsque vous ouvrez certains champs de votre schéma, tels que `web.webPageDetails.URL`, certains éléments sont automatiquement collectés. Même si plusieurs éléments sont collectés automatiquement, vous pouvez en remplacer certains, le cas échéant. Toutes les valeurs peuvent être renseignées manuellement ou en utilisant d’autres éléments de données.

>[!NOTE]
>
>Renseignez uniquement les informations que vous souhaitez recueillir. Tout ce qui n’est pas renseigné est omis lorsque les données sont envoyées aux solutions.

## Variable {#variable}

Vous pouvez créer des objets de payload à l’aide de la fonction **[!UICONTROL Variable]** élément de données. Les deux [!UICONTROL XDM] et [!UICONTROL Données] sont pris en charge.

* Lorsque vous sélectionnez [!UICONTROL XDM], sélectionnez une [!UICONTROL Sandbox] et [!UICONTROL Schéma].
* Lorsque vous sélectionnez [!UICONTROL Données], sélectionnez les solutions souhaitées. Les solutions disponibles incluent : [!UICONTROL Adobe Analytics] et [!UICONTROL Adobe Target].

![Image de l’interface utilisateur des balises présentant les options des éléments de données.](assets/variable-data-element.png)

Après avoir créé cet élément de données, vous pouvez utiliser la variable [Mettre à jour la variable](./action-types.md#update-variable) pour la modifier. Une fois prêt, vous pouvez inclure cet élément de données dans la variable [Envoyer un événement](./action-types.md#send-event) Action pour envoyer des données à un flux de données.

## Média : qualité de l’expérience {#quality-experience}

A **[!UICONTROL Qualité d’expérience]** l’élément de données est utile lors de l’envoi d’événements de média en continu à Adobe Experience Platform. Vous pouvez ajouter cet élément lors de la création d’une session multimédia. Les événements multimédia suivants contiendront la mise à jour de la qualité des données d’expérience.

![Image de l’interface utilisateur affichant l’écran Créer une qualité de l’élément de données d’expérience .](assets/qoe-data-element.png)

## Étapes suivantes {#next-steps}

En savoir plus sur des cas d’utilisation spécifiques, tels que [accès à l’ECID](accessing-the-ecid.md).
