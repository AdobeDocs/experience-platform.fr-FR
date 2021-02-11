---
title: Types d'action de l'extension SDK Web de plate-forme
description: Types d’action d’extension du SDK Web Adobe Experience Platform dans Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 54%

---


# Types d’actions

Après avoir configuré l’[extension du SDK Web de Adobe Experience Platform](web-sdk-extension.md) pour [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configurez vos types d’action.

Cette page décrit les types d&#39;action disponibles.

## Envoyer un événement

Envoie un événement à l&#39;Adobe [!DNL Experience Platform] afin que Adobe Experience Platform puisse collecter les données que vous envoyez et agir en conséquence. Vous devez sélectionner une instance (si vous en avez plusieurs). Si le événement se produit au début d’un chargement de page ou lors d’un changement de vue dans une application d’une seule page, sélectionnez **[!UICONTROL Se produit au début d’une vue]**.

Toutes les données que vous souhaitez envoyer peuvent être envoyées dans le champ **[!UICONTROL Données XDM]**. Il doit s’agir d’un objet JSON conforme à la structure de votre schéma XDM. Cet objet peut être créé sur votre page ou via un **[!UICONTROL Code personnalisé]** **[!UICONTROL élément de données]**.

## Définir le consentement

Une fois que vous avez reçu le consentement de votre utilisateur, celui-ci doit être communiqué au Adobe Experience Platform Web SDK. Pour ce faire, utilisez le type d’action « Définir le consentement ». Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Si vous utilisez le standard Adobe, vous pouvez actuellement définir le consentement sur « Entrée », « Sortie » ou vous pouvez le fournir à l’aide d’un élément de données. Si vous utilisez le standard IAB TCF, indiquez la version et la valeur que vous souhaitez utiliser, ainsi que des informations supplémentaires concernant le RGPD.

Dans cette action, un champ facultatif vous est également présenté afin d’inclure une carte Identité de sorte que les identités puissent être synchronisées une fois le consentement reçu. Cela peut s’avérer utile lorsque le consentement est configuré comme « En attente », parce que l’appel de consentement sera probablement le premier à se déclencher.

## Réinitialiser l’identifiant de fusion d’événements

Si vous souhaitez réinitialiser l’identifiant de fusion d’événements sur votre page, vous pouvez le faire avec cette action. Pour réinitialiser votre identifiant, vous devez sélectionner l’identifiant de fusion que vous souhaitez réinitialiser et déclencher l’action selon vos besoins.

## Eléments à suivre

Après avoir défini les types d&#39;action, [configurez vos types d&#39;élément de données](data-element-types.md).