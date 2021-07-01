---
title: Types d’action dans l’extension SDK Web Adobe Experience Platform
description: Découvrez les différents types d’actions fournis par l’extension SDK Web Adobe Experience Platform dans Adobe Experience Platform Launch.
solution: Experience Platform
feature: SDK Web
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 17ebf50965136f2c075f21eb3ecdcb1ce6da0b7d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 3%

---

# Types d’actions

Après avoir configuré l’[extension du SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md) pour [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configurez vos types d’actions.

Cette page décrit les types d’actions disponibles.

## Envoyer un événement

Envoie un événement à l’Adobe [!DNL Experience Platform] afin que Adobe Experience Platform puisse collecter les données que vous envoyez et agir en fonction de ces informations. Sélectionnez une instance (si vous en avez plusieurs). Toutes les données que vous souhaitez envoyer peuvent être envoyées dans le champ **[!UICONTROL Données XDM]**. Utilisez un objet JSON conforme à la structure de votre schéma XDM. Cet objet peut être créé sur votre page ou par l’intermédiaire d’un **[!UICONTROL Code personnalisé]** **[!UICONTROL élément de données]**.

D’autres champs du type d’action Envoyer l’événement peuvent également être utiles en fonction de votre implémentation. Ces champs sont tous facultatifs.

- **Type :** ce champ vous permet de spécifier un type d’événement qui sera enregistré dans votre schéma XDM. Pour plus d’informations sur les types d’événement par défaut, voir la [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) .
- **Données :** les données qui ne correspondent pas à un schéma XDM peuvent être envoyées à l’aide de ce champ. Ce champ est utile si vous essayez de mettre à jour un profil Adobe Target ou d’envoyer des attributs Recommendations Target. Pour obtenir des exemples, consultez notre [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).
- **ID de fusion :** si vous souhaitez spécifier un  [ID de ](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/merging-event-data.html?lang=en#fundamentals) fusion pour votre événement, vous pouvez le faire dans ce champ. Notez que les solutions en aval ne peuvent pas fusionner vos données d’événement pour le moment.
- **Identifiant du jeu de données :** si vous devez envoyer des données à un jeu de données autre que celui que vous avez spécifié dans votre flux de données, vous pouvez spécifier cet identifiant de jeu de données ici.
- **Le document se décharge :** si vous souhaitez vous assurer que les événements atteignent le serveur même si l’utilisateur quitte la page, cochez la case  **[!UICONTROL Le document se]** décharge. Cela permet aux événements d’atteindre le serveur, mais les réponses sont ignorées.
- **Rendre les décisions de personnalisation visuelle :** si vous souhaitez effectuer le rendu du contenu personnalisé sur votre page, cochez la case  **[!UICONTROL Rendre les]** décisions de personnalisation visuelle . Vous pouvez également spécifier des portées de décision si nécessaire. Pour plus d’informations sur le rendu du contenu personnalisé, consultez la [documentation sur la personnalisation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) .

## Définir le consentement

Une fois que vous avez reçu le consentement de votre utilisateur, ce consentement doit être communiqué au SDK Web de Adobe Experience Platform à l’aide du type d’action &quot;Définir le consentement&quot;. Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Voir [Prise en charge des préférences de consentement du client](../consent/supporting-consent.md). Lors de l’utilisation d’Adobe version 2.0, seule une valeur d’élément de données est prise en charge. Vous devez créer un élément de données qui résout l’objet de consentement.

Dans cette action, vous recevez également un champ facultatif pour inclure une carte des identités afin que les identités puissent être synchronisées une fois le consentement reçu. La synchronisation est utile lorsque le consentement est configuré comme &quot;En attente&quot; ou &quot;Sortie&quot;, car l’appel de consentement est probablement le premier appel à se déclencher.

## Réinitialiser l’identifiant de fusion d’événements

Si vous souhaitez réinitialiser votre ID de fusion d’événements sur votre page, vous pouvez le faire avec cette action. Pour réinitialiser votre ID, sélectionnez l’ID de fusion que vous souhaitez réinitialiser et déclenchez l’action selon vos besoins.

## Étapes suivantes

Une fois vos actions définies, [configurez vos types d’éléments de données](data-element-types.md).
