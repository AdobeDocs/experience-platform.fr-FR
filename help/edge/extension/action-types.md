---
title: Types d’action dans l’extension Adobe Experience Platform Web SDK
description: Découvrez les différents types d'action fournis par l'extension Adobe Experience Platform Web SDK à Adobe Experience Platform Launch.
solution: Experience Platform
feature: SDK Web
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 7e87f5b29d388b34681217e392c3f1ae8f2b67ee
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 4%

---

# Types d’actions

Après avoir configuré l’[extension du SDK Web de Adobe Experience Platform](web-sdk-extension.md) pour [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configurez vos types d’action.

Cette page décrit les types d&#39;action disponibles.

## Envoyer un événement

Envoie un événement à l&#39;Adobe [!DNL Experience Platform] afin que Adobe Experience Platform puisse collecter les données que vous envoyez et agir en conséquence. Sélectionnez une instance (si vous en avez plusieurs). Toutes les données que vous souhaitez envoyer peuvent être envoyées dans le champ **[!UICONTROL Données XDM]**. Utilisez un objet JSON conforme à la structure de votre schéma XDM. Cet objet peut être créé sur votre page ou via un **[!UICONTROL Code personnalisé]** **[!UICONTROL élément de données]**.

D’autres champs du type d’action Envoyer le Événement peuvent également s’avérer utiles en fonction de votre implémentation. Veuillez noter que ces champs sont tous facultatifs.

- **Type :** ce champ vous permet de spécifier un type d&#39;événement qui sera enregistré dans votre schéma XDM. Pour plus d’informations sur les types d&#39;événement par défaut, consultez la [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api).
- **Fusionner l’ID :** si vous souhaitez spécifier un  [ID ](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/merging-event-data.html?lang=en#fundamentals) de fusion pour votre événement, vous pouvez le faire dans ce champ. Veuillez noter que les solutions en aval ne peuvent pas fusionner vos données de événement pour le moment.
- **ID de jeu de données :** si vous devez envoyer des données à un jeu de données autre que celui que vous avez spécifié dans votre flux de données, vous pouvez spécifier cet ID de jeu de données ici.
- **Le document se décharge :** si vous souhaitez vous assurer que les événements atteignent le serveur même si l’utilisateur quitte la page, cochez la case  **[!UICONTROL Document qui]** se décharge. Cela permet aux événements d&#39;atteindre le serveur mais les réponses sont ignorées.
- **Rendu des décisions de personnalisation visuelle :** si vous souhaitez rendre du contenu personnalisé sur votre page, cochez la case  **[!UICONTROL Rendu des]** décisions de personnalisation visuelle. Vous pouvez également spécifier des étendues de décision si nécessaire. Voir la [documentation sur la personnalisation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) pour plus d’informations sur le rendu du contenu personnalisé.

## Définir le consentement

Une fois que vous avez reçu le consentement de votre utilisateur, ce consentement doit être communiqué au Adobe Experience Platform Web SDK en utilisant le type d’action &quot;Définir le consentement&quot;. Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Voir [Prise en charge des préférences de consentement du client](../consent/supporting-consent.md). Lorsque vous utilisez Adobe version 2.0, seule une valeur d’élément de données est prise en charge. Vous devez créer un élément de données qui se résout à l’objet de consentement.

Dans cette action, un champ facultatif vous est également fourni pour inclure une carte d’identité afin que les identités puissent être synchronisées une fois le consentement reçu. La synchronisation est utile lorsque le consentement est configuré comme &quot;En attente&quot; ou &quot;Sortie&quot;, car l’appel de consentement est probablement le premier appel à se déclencher.

## Réinitialiser l’identifiant de fusion d’événements

Si vous souhaitez réinitialiser l’ID de fusion de événement sur votre page, vous pouvez le faire avec cette action. Pour réinitialiser votre identifiant, sélectionnez l’identifiant de fusion à réinitialiser et déclenchez l’action selon vos besoins.

## Eléments à suivre

Après avoir défini vos actions, [configurez vos types d’éléments de données](data-element-types.md).
