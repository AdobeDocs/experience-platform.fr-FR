---
title: Types d’action dans l’extension SDK Web Adobe Experience Platform
description: Découvrez les différents types d’actions fournis par l’extension de balise du SDK Web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 3%

---


# Types d’actions

Après avoir configuré la variable [Extension de balise SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md), vous devez configurer les types d’actions.

Cette page décrit les types d’actions pris en charge par le [Extension de balise SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md).

## Envoyer un événement {#send-event}

Envoie un événement à Adobe [!DNL Experience Platform] afin que Adobe Experience Platform puisse collecter les données que vous envoyez et agir en fonction de ces informations. Sélectionnez une instance (si vous en avez plusieurs). Toutes les données que vous souhaitez envoyer peuvent être envoyées dans la variable **[!UICONTROL Données XDM]** champ . Utilisez un objet JSON conforme à la structure de votre schéma XDM. Cet objet peut être créé sur votre page ou au moyen d’un **[!UICONTROL Code personnalisé]** **[!UICONTROL Élément de données]**.

D’autres champs du type d’action Envoyer l’événement peuvent également être utiles en fonction de votre implémentation. Ces champs sont tous facultatifs.

- **Type :** Ce champ vous permet de spécifier un type d’événement qui sera enregistré dans votre schéma XDM. Voir [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=fr#using-the-sendbeacon-api) pour plus d’informations sur les types d’événement par défaut.
- **Données :** Les données qui ne correspondent pas à un schéma XDM peuvent être envoyées à l’aide de ce champ. Ce champ est utile si vous essayez de mettre à jour un profil Adobe Target ou d’envoyer des attributs Recommendations Target. Pour obtenir des exemples, consultez notre [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=fr).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Identifiant du jeu de données :** Si vous devez envoyer des données à un jeu de données autre que celui que vous avez spécifié dans votre flux de données, vous pouvez spécifier cet identifiant de jeu de données ici.
- **Le document se décharge :** Si vous souhaitez vous assurer que les événements atteignent le serveur même si l’utilisateur quitte la page, cochez la case **[!UICONTROL Le document sera déchargé.]** . Cela permet aux événements d’atteindre le serveur, mais les réponses sont ignorées.
- **Rendu des décisions de personnalisation visuelle :** Si vous souhaitez effectuer le rendu du contenu personnalisé sur votre page, cochez la case **[!UICONTROL Rendu des décisions de personnalisation visuelle]** . Vous pouvez également spécifier des portées de décision et/ou des surfaces si nécessaire. Voir [documentation de personnalisation](../../../../edge/personalization/rendering-personalization-content.md#automatically-rendering-content) pour plus d’informations sur le rendu du contenu personnalisé.

## Définition du consentement {#set-consent}

Une fois que vous avez reçu le consentement de votre utilisateur, ce consentement doit être communiqué au SDK Web de Adobe Experience Platform à l’aide du type d’action &quot;Définir le consentement&quot;. Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Voir [Prise en charge des préférences de consentement du client](../../../../edge/consent/supporting-consent.md). Lors de l’utilisation d’Adobe version 2.0, seule une valeur d’élément de données est prise en charge. Vous devez créer un élément de données qui résout l’objet de consentement.

Dans cette action, vous recevez également un champ facultatif pour inclure une carte des identités afin que les identités puissent être synchronisées une fois le consentement reçu. La synchronisation est utile lorsque le consentement est configuré comme &quot;En attente&quot; ou &quot;Sortie&quot;, car l’appel de consentement est probablement le premier appel à se déclencher.

## Mettre à jour la variable {#update-variable}

Utilisez cette action pour modifier un objet XDM suite à un événement. Cette action est destinée à créer un objet qui peut être référencé ultérieurement à partir d’un **[!UICONTROL Envoyer un événement]** pour enregistrer l’objet XDM d’événement.

Pour utiliser ce type d’action, vous devez avoir défini une [variable](data-element-types.md#variable) élément de données. Une fois que vous avez choisi un élément de données de variable à modifier, un éditeur s’affiche, semblable à l’éditeur pour le [Objet XDM](data-element-types.md#xdm-object) élément de données.

![](assets/update-variable.png)

Le schéma XDM utilisé pour l’éditeur est le schéma sélectionné sur la page [!UICONTROL variable] élément de données. Vous pouvez définir une ou plusieurs propriétés de l’objet en cliquant sur l’une des propriétés de l’arborescence à gauche, puis en modifiant la valeur à droite. Par exemple, dans la capture d’écran ci-dessous, la propriété producBy est définie sur l’élément de données &quot;Produit par l’élément de données&quot;.

![](assets/update-variable-set-property.png)

Il existe des différences entre l’éditeur dans l’action de mise à jour de variable et l’éditeur dans l’élément de données de l’objet XDM. Tout d’abord, l’action de mise à jour de variable comporte un élément de niveau racine intitulé &quot;xdm&quot;. Si vous cliquez sur cet élément, vous pouvez spécifier un élément de données à utiliser pour définir l’objet entier. Deuxièmement, l’action de mise à jour de variable comporte des cases à cocher pour effacer les données de l’objet xdm. Cliquez sur l’une des propriétés à gauche, puis cochez la case à droite pour effacer la valeur. Cela permet d’effacer la valeur actuelle avant de définir des valeurs sur la variable.

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre comment configurer vos actions. Ensuite, découvrez comment [configuration des types d’éléments de données](data-element-types.md).
