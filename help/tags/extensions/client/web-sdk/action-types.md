---
title: Types d’action dans l’extension SDK Web Adobe Experience Platform
description: Découvrez les différents types d’actions fournis par l’extension de balise du SDK Web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: fb9f7757d77b221c733bbed5124fa576a6b02ed2
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---


# Types d’actions

Après avoir configuré l’ [extension de balise du SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md), vous devez configurer vos types d’actions.

Cette page décrit les types d’actions pris en charge par l’ [extension de balise SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md).


## Appliquer la réponse {#apply-response}

Utilisez le type d’action **[!UICONTROL Appliquer la réponse]** lorsque vous souhaitez effectuer diverses actions en fonction d’une réponse de l’Edge Network. Ce type d’action est généralement utilisé dans les déploiements hybrides où le serveur effectue un appel initial vers l’Edge Network, puis ce type d’action prend la réponse de cet appel et initialise le SDK Web dans le navigateur.

L’utilisation de ce type d’action peut réduire les temps de chargement des clients pour les cas d’utilisation de personnalisation hybride.

![Image de l&#39;interface utilisateur Experience Platform montrant le type d&#39;action Appliquer la réponse.](assets/apply-response.png)

Ce type d’action prend en charge les options de configuration suivantes :

* **[!UICONTROL Instance]** : sélectionnez l’instance du SDK Web que vous utilisez.
* **[!UICONTROL En-têtes de réponse]** : sélectionnez l’élément de données qui renvoie un objet contenant les clés d’en-tête et les valeurs renvoyées par l’appel serveur Edge Network.
* **[!UICONTROL Corps de la réponse]** : sélectionnez l’élément de données qui renvoie l’objet contenant la charge utile JSON fournie par la réponse de l’Edge Network.
* **[!UICONTROL Rendre les décisions de personnalisation visuelle]** : activez cette option pour effectuer automatiquement le rendu du contenu de personnalisation fourni par l’Edge Network et pré-masquer le contenu pour empêcher le scintillement.

## Envoyer un événement {#send-event}

Envoie un événement à l’Adobe [!DNL Experience Platform] afin que Adobe Experience Platform puisse collecter les données que vous envoyez et agir sur la base de ces informations. Sélectionnez une instance (si vous en avez plusieurs). Toutes les données que vous souhaitez envoyer peuvent être envoyées dans le champ **[!UICONTROL XDM Data]**. Utilisez un objet JSON conforme à la structure de votre schéma XDM. Cet objet peut être créé sur votre page ou par l’intermédiaire d’un **** **[!UICONTROL élément de données]**.

D’autres champs du type d’action Envoyer l’événement peuvent également être utiles en fonction de votre implémentation. Ces champs sont tous facultatifs.

* **Type :** Ce champ vous permet de spécifier un type d’événement qui sera enregistré dans votre schéma XDM. Voir [`type`](/help/web-sdk/commands/sendevent/type.md) dans la commande `sendEvent` pour plus d’informations.
* **Données :** Les données qui ne correspondent pas à un schéma XDM peuvent être envoyées à l’aide de ce champ. Ce champ est utile si vous essayez de mettre à jour un profil Adobe Target ou d’envoyer des attributs Recommendations Target. Voir [`data`](/help/web-sdk/commands/sendevent/data.md) dans la commande `sendEvent` pour plus d’informations.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **Identifiant du jeu de données :** Si vous devez envoyer des données à un jeu de données autre que celui que vous avez spécifié dans votre flux de données, vous pouvez spécifier cet identifiant de jeu de données ici.
* **Le document se décharge :** Si vous souhaitez vous assurer que les événements atteignent le serveur même si l’utilisateur quitte la page, cochez la case **[!UICONTROL Le document se décharge]** . Cela permet aux événements d’atteindre le serveur, mais les réponses sont ignorées.
* **Rendre les décisions de personnalisation visuelle :** Si vous souhaitez effectuer le rendu du contenu personnalisé sur votre page, cochez la case **[!UICONTROL Render Visual personalization Decisions]** . Vous pouvez également spécifier des portées de décision et/ou des surfaces si nécessaire. Pour plus d’informations sur le rendu du contenu personnalisé, consultez la [documentation de personnalisation](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) .

## Définition du consentement {#set-consent}

Une fois que vous avez reçu le consentement de votre utilisateur, ce consentement doit être communiqué au SDK Web de Adobe Experience Platform à l’aide du type d’action &quot;Définir le consentement&quot;. Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Voir [Prise en charge des préférences de consentement du client](../../../../web-sdk/commands/setconsent.md). Lors de l’utilisation d’Adobe version 2.0, seule une valeur d’élément de données est prise en charge. Vous devez créer un élément de données qui résout l’objet de consentement.

Dans cette action, vous recevez également un champ facultatif pour inclure une carte des identités afin que les identités puissent être synchronisées une fois le consentement reçu. La synchronisation est utile lorsque le consentement est configuré comme &quot;En attente&quot; ou &quot;Sortie&quot;, car l’appel de consentement est probablement le premier appel à se déclencher.

## Mettre à jour la variable {#update-variable}

Utilisez cette action pour modifier un objet XDM suite à un événement. Cette action est destinée à créer un objet qui peut être référencé ultérieurement à partir d’une action **[!UICONTROL Envoyer l’événement]**, pour enregistrer l’objet XDM d’événement.

Pour utiliser ce type d’action, vous devez avoir défini un élément de données [variable](data-element-types.md#variable) . Une fois que vous avez choisi un élément de données de variable à modifier, un éditeur s’affiche, semblable à l’éditeur de l’élément de données [objet XDM](data-element-types.md#xdm-object) .

![](assets/update-variable.png)

Le schéma XDM utilisé pour l’éditeur est le schéma sélectionné sur l’élément de données [!UICONTROL variable] . Vous pouvez définir une ou plusieurs propriétés de l’objet en cliquant sur l’une des propriétés de l’arborescence à gauche, puis en modifiant la valeur à droite. Par exemple, dans la capture d’écran ci-dessous, la propriété producBy est définie sur l’élément de données &quot;Produit par l’élément de données&quot;.

![](assets/update-variable-set-property.png)

Il existe des différences entre l’éditeur dans l’action de mise à jour de variable et l’éditeur dans l’élément de données de l’objet XDM. Tout d’abord, l’action de mise à jour de variable comporte un élément de niveau racine intitulé &quot;xdm&quot;. Si vous cliquez sur cet élément, vous pouvez spécifier un élément de données à utiliser pour définir l’objet entier. Deuxièmement, l’action de mise à jour de variable comporte des cases à cocher pour effacer les données de l’objet xdm. Cliquez sur l’une des propriétés à gauche, puis cochez la case à droite pour effacer la valeur. Cela permet d’effacer la valeur actuelle avant de définir des valeurs sur la variable.

## Envoyer un événement multimédia {#send-media-event}

Envoie un événement multimédia à Adobe Experience Platform et/ou Adobe Analytics. Cette action est utile lorsque vous effectuez le suivi des événements multimédia sur votre site web. Sélectionnez une instance (si vous en avez plusieurs). L’action nécessite un `playerId` qui représente un identifiant unique pour une session multimédia trackée. Elle nécessite également une **[!UICONTROL qualité de l’expérience]** et un élément de données `playhead` lors du démarrage d’une session multimédia.

![Image de l’interface utilisateur de la plateforme montrant l’écran d’événement de média envoyé.](assets/send-media-event.png)

Le type d’action **[!UICONTROL Envoyer un événement multimédia]** prend en charge les propriétés suivantes :

* **[!UICONTROL Instance]** : instance du SDK Web utilisée.
* **[!UICONTROL Type d’événement multimédia]** : type de l’événement multimédia suivi.
* **[!UICONTROL ID du lecteur]** : identifiant unique de la session multimédia.
* **[!UICONTROL Curseur de lecture]** : position actuelle de la lecture du média, en secondes.
* **[!UICONTROL Détails de la session multimédia]** : lors de l’envoi d’un événement de démarrage du média, les détails requis de la session multimédia doivent être spécifiés.
* **[!UICONTROL Détails du chapitre]** : dans cette section, vous pouvez spécifier les détails du chapitre lors de l’envoi d’un événement multimédia de début de chapitre.
* **[!UICONTROL Détails Advertising]** : lors de l’envoi d’un événement `AdBreakStart`, vous devez spécifier les détails publicitaires requis.
* **[!UICONTROL Détails de la capsule Advertising]** : détails de la capsule publicitaire lors de l’envoi d’un événement `AdStart`.
* **[!UICONTROL Détails de l’erreur]** : détails sur l’erreur de lecture qui est suivie.
* **[!UICONTROL Détails de mise à jour de l’état]** : état du lecteur mis à jour.
* **[!UICONTROL Métadonnées personnalisées]** : métadonnées personnalisées de l’événement multimédia en cours de suivi.
* **[!UICONTROL Qualité de l’expérience]** : qualité multimédia des données d’expérience suivies.

## Obtention du suivi de Media Analytics {#get-media-analytics-tracker}

Cette action est utilisée pour obtenir l’API Media Analytics héritée. Lors de la configuration de l’action et qu’un nom d’objet est fourni, l’API Media Analytics héritée est exportée vers cet objet de fenêtre. Si aucun fichier n’est fourni, il sera exporté vers `window.Media` comme le fait la bibliothèque Media JS actuelle.

![Image de l’interface utilisateur de la plateforme montrant le type d’action Get Media Analytics Tracker.](assets/get-media-analytics-tracker.png)

## Redirection vers une identité {#redirect-with-identity}

Utilisez ce type d’action pour partager les identités de la page active avec d’autres domaines. Cette action est conçue pour être utilisée avec un type d’événement **[!UICONTROL click]** et une condition de comparaison de valeurs. Voir [Ajout d’une identité à une URL à l’aide de l’extension SDK Web](../../../../web-sdk/commands/appendidentitytourl.md#extension) pour plus d’informations sur l’utilisation de ce type d’action.

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre comment configurer vos actions. Ensuite, découvrez comment [configurer vos types d’éléments de données](data-element-types.md).
