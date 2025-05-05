---
title: Présentation de l’extension Meta Pixel
description: Découvrez l’extension de balise Meta Pixel dans Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Présentation de l’extension [!DNL Meta Pixel]

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) est un outil d’analyse JavaScript qui vous permet de suivre l’activité des visiteurs sur votre site web. Les actions des visiteurs dont vous effectuez le suivi (appelées conversions) sont envoyées à [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) où elles peuvent être utilisées pour mesurer l’efficacité de vos publicités, campagnes, entonnoirs de conversion, etc.

L’extension de balise [!DNL Meta Pixel] vous permet d’exploiter les fonctionnalités [!DNL Pixel] de vos bibliothèques de balises côté client. Ce document explique comment installer l’extension et utiliser ses fonctionnalités dans une [règle](../../../ui/managing-resources/rules.md).

## Conditions préalables

Pour utiliser l’extension, vous devez disposer d’un compte [!DNL Meta] valide ayant accès à [!DNL Ads Manager]. Plus précisément, vous devez [créer un  [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) et copier son [!DNL Pixel ID] afin que l’extension puisse être configurée sur votre compte. Si vous disposez déjà d’un [!DNL Meta Pixel], vous pouvez utiliser son identifiant à la place.

Il est vivement recommandé d’utiliser [!DNL Meta Pixel] conjointement avec [!DNL Meta Conversions API] pour partager et envoyer les mêmes événements du côté client et du côté serveur, respectivement, car cela peut aider à récupérer les événements qui n’ont pas été sélectionnés par [!DNL Meta Pixel]. Consultez le guide sur l’extension [[!DNL Meta Conversions API] pour le transfert d’événement](../../client/meta/overview.md) pour savoir comment l’intégrer à vos mises en oeuvre côté serveur. Notez que votre organisation doit avoir accès au [transfert d’événement](../../../ui/event-forwarding/overview.md) pour utiliser l’extension côté serveur.

## Installation l’extension

Pour installer l’extension [!DNL Meta Pixel], accédez à l’interface utilisateur de collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]** . Recherchez la carte [!UICONTROL Meta Pixel] , puis sélectionnez **[!UICONTROL Install]**.

![Bouton [!UICONTROL Installer] sélectionné pour l’extension [!UICONTROL Meta Pixel] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/client/meta/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir l’ID [!DNL Pixel] que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou sélectionner un élément de données existant à la place.

>[!TIP]
>
>L’utilisation d’un élément de données vous donne la possibilité de modifier dynamiquement l’ID [!DNL Pixel] utilisé en fonction d’autres facteurs tels que l’environnement de création. Pour plus d’informations, reportez-vous à la section de l’annexe sur [l’utilisation d’identifiants  [!DNL Pixel]  différents pour différents environnements](#id-data-element) .

Vous pouvez également éventuellement fournir un ID d’événement à associer à l’extension. Elle est utilisée pour dédupliquer des événements identiques entre [!DNL Meta Pixel] et [!DNL Meta Conversions API]. Pour plus d’informations, reportez-vous à la section sur la [déduplication d’événements](../../server/meta/overview.md#event-deduplication) dans la présentation de l’extension [!DNL Conversions API].

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**

![ ID [!DNL Pixel] fourni en tant qu’élément de données dans la vue de configuration de l’extension.](../../../images/extensions/client/meta/configure.png)

L’extension est installée et vous pouvez désormais utiliser ses différentes actions dans vos règles de balises.

## Configuration d’une règle de balise {#rule}

[!DNL Meta Pixel] accepte un ensemble d’ [événements standard](https://www.facebook.com/business/help/402791146561655) prédéfinis, chacun avec ses propres contextes et ses propriétés acceptées. Les actions de règle fournies par l’extension [!DNL Pixel] sont corrélées à ces types d’événements, ce qui vous permet de classer et de configurer facilement l’événement envoyé à [!DNL Meta] en fonction de son type.

À des fins de démonstration, cette section explique comment créer une règle qui envoie un événement de page vue à [!DNL Meta].

Commencez à créer une règle de balise et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Meta Pixel]** pour l’extension, puis **[!UICONTROL Send Page View]** pour le type d’action.

![Le type d’action [!UICONTROL Envoyer la page vue] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](../../../images/extensions/client/meta/select-action.png)

Aucune autre configuration n’est requise pour l’action [!UICONTROL Envoyer la page vue]. Sélectionnez **[!UICONTROL Keep Changes]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez une nouvelle balise [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Confirmer que [!DNL Meta] reçoit des données

Une fois la version mise à jour déployée sur votre site web, vous pouvez confirmer si les données sont envoyées comme prévu en générant certains événements de conversion sur votre navigateur et en vérifiant si ces événements apparaissent dans [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Meta] à l’aide de l’extension de balise [!DNL Meta Pixel]. Si vous envisagez d’envoyer également des événements côté serveur à [!DNL Meta], vous pouvez maintenant procéder à l’installation et à la configuration de l’ [[!DNL Conversions API] extension de transfert d’événement](../../server/meta/overview.md).

Pour plus d’informations sur les balises en Experience Platform, reportez-vous à la [présentation des balises](../../../home.md).

## Annexe : Utilisation de [!DNL Pixel] ID différents pour différents environnements {#id-data-element}

Si vous souhaitez tester votre mise en oeuvre dans des environnements de développement ou d’évaluation tout en préservant vos analyses de production [!DNL Meta Pixel], vous pouvez utiliser un élément de données pour choisir dynamiquement un ID [!DNL Pixel] approprié en fonction de l’environnement utilisé.

Pour ce faire, vous pouvez utiliser un élément de données [!UICONTROL &#x200B; Custom Code] (fourni par l’ [[!UICONTROL extension Core]](../core/overview.md)) en combinaison avec la [`turbine` free variable](../../../extension-dev/turbine.md). Dans le code JavaScript de l’élément de données, utilisez l’objet `turbine` pour trouver l’étape d’environnement actuelle, puis renvoyez un ID [!DNL Pixel] approprié en fonction du résultat.

L’exemple suivant renvoie un faux ID de production `exampleProductionKey` lorsqu’il est utilisé dans l’environnement de production et un autre ID `exampleTestKey` lorsqu’un autre environnement est utilisé. Lors de l’implémentation de ce code, remplacez chaque valeur par vos identifiants de production et de test réels [!DNL Pixel].

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
