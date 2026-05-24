---
title: Présentation de l’extension Snap Pixel
description: Découvrez comment utiliser l’extension de balise Snap Pixel pour capturer de précieuses interactions utilisateur dans Adobe Experience Platform.
last-substantial-update: 2025-09-17T00:00:00.000Z
exl-id: 786fc3fd-29c8-4ca0-be6d-38b420de31ae
TQID: https://experienceleague.adobe.com/nnICZBpLeGMWPyf9zf3ZMcXKzXz9ozS1wMEpPaqzYOU
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: dfc56824-e8b9-499e-85d4-21aedb507314id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: ae2cba0e-54f2-464b-a3b3-ad371e8a886aid: b64298cc-90cc-46b7-8917-ee391f1c7516id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1cid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 634
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

Pour installer l’extension [!DNL Snap Pixel], accédez à l’interface utilisateur de la collecte de données ou d’Experience Platform et sélectionnez **[!UICONTROL Tags]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez-en une nouvelle.

Une fois la propriété sélectionnée ou créée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalog]** . Recherchez la carte [!UICONTROL Snap Pixel], puis sélectionnez **[!UICONTROL Install]**.

![Le bouton [!UICONTROL Install] sélectionné pour l’extension [!UICONTROL Snap Pixel] dans l’interface utilisateur de collecte de données.](./images/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir l’identifiant de pixel que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou sélectionner un élément de données existant à la place.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]**.

![Identifiant [!DNL Pixel] fourni en tant qu’élément de données dans la vue de configuration de l’extension.](./images/configure.png)

L’extension est installée et vous pouvez maintenant utiliser ses différentes actions dans vos règles de balise.

## Configuration d’une règle de balise {#rule}

[!DNL Snap Pixel] prend en charge un ensemble d’événements standard prédéfinis, chacun avec des contextes spécifiques et des paramètres acceptés. Les actions de règle disponibles dans l’extension [!DNL Snap Pixel] s’alignent sur ces types d’événements, ce qui facilite la classification et la configuration des événements envoyés aux [!DNL Snap] en fonction de leur type.

À des fins de démonstration, cette section montre comment créer une règle qui envoie un événement d’achat à [!DNL Snap].

Pour commencer, créez une règle de balise et définissez les conditions selon vos besoins. Lors de la configuration des actions de la règle, choisissez [!DNL Snap Pixel] comme extension, puis sélectionnez **[!UICONTROL Send Purchase Event]** comme type d’action.

Une fois la configuration de l’action [!UICONTROL Send Purchase Event] terminée, sélectionnez **[!UICONTROL Keep Changes]** pour l’ajouter à la configuration de votre règle.

![Type d’action [!UICONTROL Send Purchase Event] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](./images/action-type.png)

Lorsque vous êtes satisfait(e) de la configuration globale des règles, sélectionnez **[!UICONTROL Save to Library]**.

Pour appliquer vos mises à jour, publiez une nouvelle balise [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Confirmer que [!DNL Snap] reçoit des données {#confirm}

Une fois votre version mise à jour déployée sur votre site web, vous pouvez vérifier que les données sont envoyées comme prévu en déclenchant des événements de conversion dans votre navigateur et en vérifiant qu’elles apparaissent dans [[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager).

## Étapes suivantes {#next-steps}

Ce guide explique comment envoyer des données à [!DNL Snap] à l’aide de l’extension de balise [!DNL Snap Pixel]. Si vous prévoyez également d’envoyer des événements côté serveur à [!DNL Snap], vous pouvez procéder à l’installation et à la configuration du [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md).
