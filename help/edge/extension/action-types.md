---
title: Types d’action dans l’extension SDK Web Adobe Experience Platform
description: Découvrez les différents types d’actions fournis par l’extension de balise du SDK Web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# Types d’actions

Après avoir configuré la variable [Extension de balise SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md), configurez vos types d’actions.

Cette page décrit les types d’actions disponibles.


## Envoyer un événement

Envoie un événement à Adobe [!DNL Experience Platform] afin que Adobe Experience Platform puisse collecter les données que vous envoyez et agir en fonction de ces informations. Sélectionnez une instance (si vous en avez plusieurs). Toutes les données que vous souhaitez envoyer peuvent être envoyées dans la variable **[!UICONTROL Données XDM]** champ . Utilisez un objet JSON conforme à la structure de votre schéma XDM. Cet objet peut être créé sur votre page ou au moyen d’un **[!UICONTROL Code personnalisé]** **[!UICONTROL Élément de données]**.

D’autres champs du type d’action Envoyer l’événement peuvent également être utiles en fonction de votre implémentation. Ces champs sont tous facultatifs.

- **Type :** Ce champ vous permet de spécifier un type d’événement qui sera enregistré dans votre schéma XDM. Voir [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) pour plus d’informations sur les types d’événement par défaut.
- **Données :** Les données qui ne correspondent pas à un schéma XDM peuvent être envoyées à l’aide de ce champ. Ce champ est utile si vous essayez de mettre à jour un profil Adobe Target ou d’envoyer des attributs Recommendations Target. Pour obtenir des exemples, consultez notre [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Identifiant du jeu de données :** Si vous devez envoyer des données à un jeu de données autre que celui que vous avez spécifié dans votre flux de données, vous pouvez spécifier cet identifiant de jeu de données ici.
- **Le document se décharge :** Si vous souhaitez vous assurer que les événements atteignent le serveur même si l’utilisateur quitte la page, cochez la case **[!UICONTROL Le document sera déchargé.]** . Cela permet aux événements d’atteindre le serveur, mais les réponses sont ignorées.
- **Rendu des décisions de personnalisation visuelle :** Si vous souhaitez effectuer le rendu du contenu personnalisé sur votre page, cochez la case **[!UICONTROL Rendu des décisions de personnalisation visuelle]** . Vous pouvez également spécifier des portées de décision et/ou des surfaces si nécessaire. Voir [documentation de personnalisation](../personalization/rendering-personalization-content.md#automatically-rendering-content) pour plus d’informations sur le rendu du contenu personnalisé.

## Définir le consentement

Une fois que vous avez reçu le consentement de votre utilisateur, ce consentement doit être communiqué au SDK Web de Adobe Experience Platform à l’aide du type d’action &quot;Définir le consentement&quot;. Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Voir [Prise en charge des préférences de consentement du client](../consent/supporting-consent.md). Lors de l’utilisation d’Adobe version 2.0, seule une valeur d’élément de données est prise en charge. Vous devez créer un élément de données qui résout l’objet de consentement.

Dans cette action, vous recevez également un champ facultatif pour inclure une carte des identités afin que les identités puissent être synchronisées une fois le consentement reçu. La synchronisation est utile lorsque le consentement est configuré comme &quot;En attente&quot; ou &quot;Sortie&quot;, car l’appel de consentement est probablement le premier appel à se déclencher.

## Réinitialiser l’identifiant de fusion d’événements

Si vous souhaitez réinitialiser votre ID de fusion d’événements sur votre page, vous pouvez le faire avec cette action. Pour réinitialiser votre ID, sélectionnez l’ID de fusion que vous souhaitez réinitialiser et déclenchez l’action selon vos besoins.

## Étapes suivantes

Après avoir défini vos actions, [configuration des types d’éléments de données](data-element-types.md).
