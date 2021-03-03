---
title: Types d’action dans l’extension Adobe Experience Platform Web SDK
description: Découvrez les différents types d'action fournis par l'extension Adobe Experience Platform Web SDK à Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 18%

---


# Types d’actions

Après avoir configuré l’[extension du SDK Web de Adobe Experience Platform](web-sdk-extension.md) pour [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configurez vos types d’action.

Cette page décrit les types d&#39;action disponibles.

## Envoyer un événement

Envoie un événement à l&#39;Adobe [!DNL Experience Platform] afin que Adobe Experience Platform puisse collecter les données que vous envoyez et agir en conséquence. Sélectionnez une instance (si vous en avez plusieurs). Si le événement se produit au début d’un chargement de page ou lors d’un changement de vue dans une application d’une seule page, sélectionnez **[!UICONTROL Se produit au début d’une vue]**.

Toutes les données que vous souhaitez envoyer peuvent être envoyées dans le champ **[!UICONTROL Données XDM]**. Utilisez un objet JSON conforme à la structure de votre schéma XDM. Cet objet peut être créé sur votre page ou via un **[!UICONTROL Code personnalisé]** **[!UICONTROL élément de données]**.

## Définir le consentement

Une fois que vous avez reçu le consentement de votre utilisateur, ce consentement doit être communiqué au Adobe Experience Platform Web SDK en utilisant le type d’action &quot;Définir le consentement&quot;. Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Si vous utilisez le standard Adobe, vous pouvez actuellement définir le consentement sur « Entrée », « Sortie » ou vous pouvez le fournir à l’aide d’un élément de données. Si vous utilisez le standard IAB TCF, indiquez la version et la valeur que vous souhaitez utiliser, ainsi que des informations supplémentaires concernant le RGPD.

Dans cette action, un champ facultatif vous est également fourni pour inclure une carte d’identité afin que les identités puissent être synchronisées une fois le consentement reçu. La synchronisation est utile lorsque le consentement est configuré comme &quot;En attente&quot;, car l’appel de consentement est probablement le premier appel à se déclencher.

## Réinitialiser l’identifiant de fusion d’événements

Si vous souhaitez réinitialiser l’ID de fusion de événement sur votre page, vous pouvez le faire avec cette action. Pour réinitialiser votre identifiant, sélectionnez l’identifiant de fusion à réinitialiser et déclenchez l’action selon vos besoins.

## Eléments à suivre

Après avoir défini les types d&#39;action, [configurez vos types d&#39;élément de données](data-element-types.md).