---
title: Présentation de l’extension Meta Pixel
description: Découvrez l’extension de balise Meta Pixel dans Adobe Experience Platform.
source-git-commit: 87376172f89858bfa883084461544a2c50ba5009
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 2%

---

# [!DNL Meta Pixel] présentation de l’extension

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) est un outil d’analyse JavaScript qui vous permet de suivre l’activité des visiteurs sur votre site web. Les actions des visiteurs dont vous effectuez le suivi (appelées conversions) sont envoyées à [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) où ils peuvent être utilisés pour mesurer l’efficacité de vos publicités, campagnes, entonnoirs de conversion, etc.

Le [!DNL Meta Pixel] l’extension de balise vous permet d’exploiter [!DNL Pixel] fonctionnalités de vos bibliothèques de balises côté client. Ce document explique comment installer l’extension et utiliser ses fonctionnalités dans une [règle](../../../ui/managing-resources/rules.md).

<!-- (To include when Conversions API extension doc is published)
>[!NOTE]
>
>If you are trying to send server-side events to [!DNL Meta] rather than from the client side, use the [[!DNL Meta Conversions API] extension](../../server/meta/overview.md) instead.
-->

## Conditions préalables

Pour utiliser l’extension, vous devez disposer d’un [!DNL Meta] compte avec accès à [!DNL Ads Manager]. Plus précisément, vous devez [créer [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) et copiez ses [!DNL Pixel ID] l’extension peut donc être configurée sur votre compte. Si vous disposez déjà d’une [!DNL Meta Pixel], vous pouvez utiliser son identifiant à la place.

## Installer l’extension

Pour installer le [!DNL Meta Pixel] , accédez à l’interface utilisateur de la collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Catalogue]** . Recherchez le [!UICONTROL Meta Pixel] carte, puis sélectionnez **[!UICONTROL Installer]**.

![Le [!UICONTROL Installer] sélectionné pour l’option [!UICONTROL Meta Pixel] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/client/meta/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir la variable [!DNL Pixel] ID que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou sélectionner un élément de données existant à la place.

>[!TIP]
>
>L’utilisation d’un élément de données vous donne la possibilité de modifier dynamiquement la variable [!DNL Pixel] ID utilisé en fonction d’autres facteurs, tels que l’environnement de génération. Voir la section de l’annexe sur [en utilisant différents [!DNL Pixel] ID pour différents environnements](#id-data-element) pour plus d’informations.

Vous pouvez également éventuellement fournir un ID d’événement à associer à l’extension. Elle permet de dédupliquer des événements identiques entre les [!DNL Meta Pixel] et le [!DNL Meta Conversions API]. Voir [!DNL Meta] documentation sur [gestion des doublons [!DNL Pixel] et [!DNL Conversions API] events](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/) pour plus d’informations.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**

![Le [!DNL Pixel] ID fourni en tant qu’élément de données dans la vue de configuration de l’extension.](../../../images/extensions/client/meta/configure.png)

L’extension est installée et vous pouvez désormais utiliser ses différentes actions dans vos règles de balises.

## Configuration d’une règle de balise {#rule}

[!DNL Meta Pixel] accepte un jeu prédéfini [événements standard](https://www.facebook.com/business/help/402791146561655), chacun avec son propre contexte et ses propriétés acceptées. Les actions de règle fournies par la variable [!DNL Pixel] l’extension est en corrélation avec ces types d’événements, ce qui vous permet de classer et de configurer facilement l’événement envoyé à [!DNL Meta] selon son type.

À des fins de démonstration, cette section explique comment créer une règle qui envoie un événement de page vue à [!DNL Meta].

Commencez à créer une règle de balise et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Meta Pixel]** pour l’extension, puis sélectionnez **[!UICONTROL Envoyer la page vue]** pour le type d’action.

![Le [!UICONTROL Envoyer la page vue] type d’action sélectionné pour une règle dans l’interface utilisateur de la collecte de données.](../../../images/extensions/client/meta/select-action.png)

Aucune autre configuration n’est requise pour la variable [!UICONTROL Envoyer la page vue] action. Sélectionner **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez une nouvelle balise. [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Confirmez que [!DNL Meta] reçoit des données

Une fois la version mise à jour déployée sur votre site web, vous pouvez confirmer si les données sont envoyées comme prévu en générant certains événements de conversion sur votre navigateur et en vérifiant si ces événements apparaissent dans [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Meta] en utilisant la variable [!DNL Meta Pixel] extension de balise. Pour plus d’informations sur les balises en Experience Platform, reportez-vous à la section [présentation des balises](../../../home.md).

## Annexe : Utilisez différentes [!DNL Pixel] ID pour différents environnements {#id-data-element}

Si vous souhaitez tester votre mise en oeuvre dans des environnements de développement ou d’évaluation tout en conservant votre production [!DNL Meta Pixel] analytics intact, vous pouvez utiliser un élément de données pour choisir de manière dynamique un élément approprié. [!DNL Pixel] Identifiant en fonction de l’environnement utilisé.

Pour ce faire, utilisez une [!UICONTROL Code personnalisé] élément de données (fourni par [[!UICONTROL Core] extension](../core/overview.md)) en combinaison avec la fonction [`turbine` variable libre](../../../extension-dev/turbine.md). Dans le code JavaScript de l’élément de données, utilisez la variable `turbine` pour trouver l’étape d’environnement actuelle, puis renvoyer une [!DNL Pixel] ID en fonction du résultat.

L’exemple suivant renvoie un faux identifiant de production. `exampleProductionKey` lorsqu’il est utilisé dans l’environnement de production, et un identifiant différent `exampleTestKey` lorsque tout autre environnement est utilisé. Lors de l’implémentation de ce code, remplacez chaque valeur par votre production et votre test réels. [!DNL Pixel] ID.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```

