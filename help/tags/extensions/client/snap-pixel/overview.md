---
title: Présentation de l’extension Snap Pixel
description: Découvrez comment utiliser l’extension de balise Snap Pixel pour capturer de précieuses interactions utilisateur dans Adobe Experience Platform.
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# Présentation de l’extension [!DNL Snap Pixel]

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about) est un outil d’analyse basé sur JavaScript qui vous permet de capturer des interactions utilisateur importantes sur votre site web. Les actions importantes destinées aux visiteurs, telles que les achats, les inscriptions ou d’autres conversions, sont automatiquement envoyées à votre [Gestionnaire de publicités](http://ads.snapchat.com/), ce qui vous permet de mesurer et d’optimiser les performances de vos publicités, campagnes, chemins de conversion, etc.

L’extension de balise [!DNL Snap Pixel] vous permet d’intégrer [!DNL Snap Pixel] fonctionnalité directement dans vos bibliothèques de balises côté client. Cette documentation décrit comment installer l’extension et implémenter ses fonctionnalités dans vos règles de gestion des balises.

L’extension de balise [!DNL Snap Pixel] simplifie l’intégration de [!DNL Snap Pixel] fonctionnalité dans vos bibliothèques de balises côté client existantes. Cette documentation décrit comment installer l’extension et configurer ses fonctionnalités dans vos [ règles de gestion des balises](../../../ui/managing-resources/rules.md).

## Conditions préalables {#prerequisites}

Pour utiliser l’extension, vous aurez besoin d’un compte [!DNL Snap] valide avec un accès à [!DNL Ads Manager]. Vous devez [créer un nouveau [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about) et copier son Pixel ID pour configurer l’extension de votre compte. Si vous disposez d’un [!DNL Snap Pixel] existant, vous pouvez simplement utiliser son identifiant.

Il est recommandé d’utiliser [!DNL Snap Pixel] avec le [!DNL Snap Conversions API] pour envoyer les mêmes événements du côté client et du côté serveur. Cette approche peut aider à récupérer des événements qui ne peuvent pas être capturés par le seul [!DNL Snap Pixel]. Reportez-vous à la section [[!DNL Snap] Extension de l’API de conversion pour le transfert d’événement](../../server/snap/overview.md) pour savoir comment l’intégrer à vos implémentations côté serveur. Notez que votre organisation doit avoir accès au [transfert d’événement](../../../ui/event-forwarding/overview.md) pour utiliser l’extension côté serveur.

## Installation l’extension {#install}

Pour installer l’extension [!DNL Snap Pixel], accédez à l’interface utilisateur de la collecte de données ou d’Experience Platform et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez-en une nouvelle.

Une fois la propriété sélectionnée ou créée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Recherchez la carte [!UICONTROL Snap Pixel], puis sélectionnez **[!UICONTROL Installer]**.

![Le bouton [!UICONTROL Installer] sélectionné pour l’extension [!UICONTROL Snap Pixel] dans l’interface utilisateur de la collecte de données.](./images/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir l’identifiant de pixel que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou sélectionner un élément de données existant à la place.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Identifiant [!DNL Pixel] fourni en tant qu’élément de données dans la vue de configuration de l’extension.](./images/configure.png)

L’extension est installée et vous pouvez maintenant utiliser ses différentes actions dans vos règles de balise.

## Configuration d’une règle de balise {#rule}

[!DNL Snap Pixel] prend en charge un ensemble d’événements standard prédéfinis, chacun avec des contextes spécifiques et des paramètres acceptés. Les actions de règle disponibles dans l’extension [!DNL Snap Pixel] s’alignent sur ces types d’événements, ce qui facilite la classification et la configuration des événements envoyés aux [!DNL Snap] en fonction de leur type.

À des fins de démonstration, cette section montre comment créer une règle qui envoie un événement d’achat à [!DNL Snap].

Pour commencer, créez une règle de balise et définissez les conditions selon vos besoins. Lors de la configuration des actions de la règle, choisissez [!DNL Snap Pixel] comme extension, puis sélectionnez **[!UICONTROL Envoyer l’événement d’achat]** comme type d’action.

Une fois la configuration de l’action [!UICONTROL Envoyer l’événement d’achat] terminée, sélectionnez **[!UICONTROL Conserver les modifications]** pour l’ajouter à la configuration des règles.

![Type d’action [!UICONTROL &#x200B; Envoyer l’événement d’achat &#x200B;] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](./images/action-type.png)

Lorsque la configuration globale de la règle vous convient, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Pour appliquer vos mises à jour, publiez une nouvelle balise [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Confirmer que [!DNL Snap] reçoit des données {#confirm}

Une fois votre version mise à jour déployée sur votre site web, vous pouvez vérifier que les données sont envoyées comme prévu en déclenchant des événements de conversion dans votre navigateur et en vérifiant qu’elles apparaissent dans [[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager).

## Étapes suivantes {#next-steps}

Ce guide explique comment envoyer des données à [!DNL Snap] à l’aide de l’extension de balise [!DNL Snap Pixel]. Si vous prévoyez également d’envoyer des événements côté serveur à [!DNL Snap], vous pouvez procéder à l’installation et à la configuration du [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md).
