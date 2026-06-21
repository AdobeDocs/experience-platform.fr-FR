---
title: Présentation de l’extension Meta Pixel
description: Découvrez l’extension de balise Meta Pixel dans Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
TQID: https://experienceleague.adobe.com/0B6N5yvE4O-P6O6HyWMtkY0iU-0IXR6QUmHclhiss2o
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ae2cba0e-54f2-464b-a3b3-ad371e8a886a
  - id: b64298cc-90cc-46b7-8917-ee391f1c7516
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1c
  - id: df312454-73c4-43f6-a90e-18f5043f074c
  - id: f6ff4d13-7b5c-4533-8556-95e76673d4cb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 843
ht-degree: 0%

---

# Présentation de l’extension [!DNL Meta Pixel]

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) est un outil d’analyse basé sur JavaScript qui vous permet d’effectuer le suivi de l’activité des visiteurs sur votre site web. Les actions du visiteur que vous suivez (appelées conversions) sont envoyées à [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) où elles peuvent être utilisées pour mesurer l’efficacité de vos annonces, campagnes, entonnoirs de conversion, etc.

L’extension de balise [!DNL Meta Pixel] vous permet d’exploiter [!DNL Pixel] fonctionnalités dans vos bibliothèques de balises côté client. Ce document explique comment installer l’extension et utiliser ses fonctionnalités dans une [règle](../../../ui/managing-resources/rules.md).

## Conditions préalables

Pour utiliser l’extension, vous devez disposer d’un compte [!DNL Meta] valide avec un accès à [!DNL Ads Manager]. Plus précisément, vous devez [créer un nouveau [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) et copier son [!DNL Pixel ID] afin que l’extension puisse être configurée sur votre compte. Si vous disposez déjà d’un [!DNL Meta Pixel], vous pouvez utiliser son identifiant à la place.

Il est vivement recommandé d’utiliser [!DNL Meta Pixel] en combinaison avec le [!DNL Meta Conversions API] pour partager et envoyer les mêmes événements côté client et côté serveur, respectivement, car cela peut aider à récupérer les événements qui n’ont pas été récupérés par [!DNL Meta Pixel]. Consultez le guide sur l’[[!DNL Meta Conversions API] extension pour le transfert d’événement](../../client/meta/overview.md) pour savoir comment l’intégrer dans vos implémentations côté serveur. Notez que votre organisation doit avoir accès au [transfert d’événement](../../../ui/event-forwarding/overview.md) pour utiliser l’extension côté serveur.

## Installation l’extension

Pour installer l’extension [!DNL Meta Pixel], accédez à l’interface utilisateur de la collecte de données ou d’Experience Platform et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez-en une nouvelle.

Une fois la propriété sélectionnée ou créée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Recherchez la carte [!UICONTROL Meta Pixel], puis sélectionnez **[!UICONTROL Installer]**.

![Le bouton [!UICONTROL Installer] sélectionné pour l’extension [!UICONTROL Meta Pixel] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/client/meta/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir l’identifiant [!DNL Pixel] que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou sélectionner un élément de données existant à la place.

>[!TIP]
>
>L’utilisation d’un élément de données vous donne la possibilité de modifier de manière dynamique l’identifiant de [!DNL Pixel] utilisé en fonction d’autres facteurs, tels que l’environnement de création. Pour plus d’informations, consultez la section annexe sur [Utilisation  [!DNL Pixel]  différents ID pour différents environnements](#id-data-element).

Vous pouvez également fournir un identifiant d’événement à associer à l’extension. Il est utilisé pour dédupliquer des événements identiques entre [!DNL Meta Pixel] et le [!DNL Meta Conversions API]. Pour plus d’informations, consultez la section sur la [déduplication des événements](../../server/meta/overview.md#event-deduplication) dans la présentation de l’extension [!DNL Conversions API].

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**

![Identifiant [!DNL Pixel] fourni en tant qu’élément de données dans la vue de configuration de l’extension.](../../../images/extensions/client/meta/configure.png)

L’extension est installée et vous pouvez maintenant utiliser ses différentes actions dans vos règles de balise.

## Configuration d’une règle de balise {#rule}

[!DNL Meta Pixel] accepte un ensemble d’événements [standard](https://www.facebook.com/business/help/402791146561655) prédéfinis, chacun ayant ses propres contextes et propriétés acceptées. Les actions de règle fournies par l’extension [!DNL Pixel] sont corrélées à ces types d’événements, ce qui vous permet de classer et de configurer facilement l’événement envoyé à [!DNL Meta] en fonction de son type.

À des fins de démonstration, cette section montre comment créer une règle qui envoie un événement de page vue à [!DNL Meta].

Commencez à créer une règle de balise et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Meta Pixel]** pour l’extension, puis sélectionnez **[!UICONTROL Envoyer la page vue]** pour le type d’action.

![Type d’action [!UICONTROL &#x200B; Envoyer la page vue &#x200B;] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](../../../images/extensions/client/meta/select-action.png)

Aucune configuration supplémentaire n’est requise pour l’action [!UICONTROL &#x200B; Envoyer la page vue &#x200B;]. Sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous convient, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez une nouvelle balise [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Confirmer que [!DNL Meta] reçoit des données

Une fois votre version mise à jour déployée sur votre site web, vous pouvez vérifier si les données sont envoyées comme prévu en générant des événements de conversion sur votre navigateur et en vérifiant si ces événements apparaissent dans [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Meta] à l’aide de l’extension de balise [!DNL Meta Pixel]. Si vous prévoyez d’envoyer également des événements côté serveur à [!DNL Meta], vous pouvez maintenant procéder à l’installation et à la configuration de l’extension de transfert d’événement [[!DNL Conversions API] event](../../server/meta/overview.md).

Pour plus d’informations sur les balises dans Experience Platform, consultez la [présentation des balises](../../../home.md).

## Annexe : utilisation de différents identifiants de [!DNL Pixel] pour différents environnements {#id-data-element}

Si vous souhaitez tester votre mise en œuvre dans des environnements de développement ou d’évaluation tout en préservant l’intégrité de vos analyses de [!DNL Meta Pixel] de production, vous pouvez utiliser un élément de données pour choisir de manière dynamique un identifiant d’[!DNL Pixel] approprié en fonction de l’environnement utilisé.

Pour ce faire, vous pouvez utiliser un élément de données [!UICONTROL Code personnalisé] (fourni par l’extension [[!UICONTROL Core]](../core/overview.md)) en combinaison avec la variable libre [`turbine`](../../../extension-dev/turbine.md). Dans le code JavaScript de l’élément de données, utilisez l’objet `turbine` pour rechercher l’étape d’environnement actuelle, puis renvoyez un identifiant d’[!DNL Pixel] approprié en fonction du résultat.

L’exemple suivant renvoie un `exampleProductionKey` d’ID de production factice lorsqu’il est utilisé dans l’environnement de production et un `exampleTestKey` d’ID différent lorsqu’un autre environnement est utilisé. Lors de l’implémentation de ce code, remplacez chaque valeur par vos ID de [!DNL Pixel] de production et de test réels.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
