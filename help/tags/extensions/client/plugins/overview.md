---
title: Présentation de l’extension Common Analytics
description: Découvrez l’extension de balises Common Analytics dans Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
TQID: https://experienceleague.adobe.com/mWtMNd7CQAik8cmxeqm92ECFezJs7ATep0jJZAJ62jM
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 362
ht-degree: 85%

---

# Présentation de l’extension de modules externes courants Analytics

Cette référence vous permet d’obtenir plus d’informations sur la configuration de l’extension de modules externes courants Analytics et sur les options disponibles lors de l’utilisation de cette extension pour augmenter l’extension [!DNL Adobe Analytics].

## Configurer l’extension de modules externes courants Analytics

Cette section fournit des informations sur les options disponibles lors de la configuration de l’extension de modules externes courants Analytics.

>[!IMPORTANT]
>
>L’extension de modules externes courants Analytics augmente l’extension [!DNL Adobe Analytics]. L’extension [!DNL Adobe Analytics] doit être installée sur votre propriété pour fonctionner. De plus, vous devez rendre le dispositif de suivi accessible globalement dans l’extension [!DNL Adobe Analytics].

Aucune configuration supplémentaire n’est requise au niveau de l’extension.

## Ajouter des modules externes à l’extension [!DNL Adobe Analytics]

Pour pouvoir utiliser les modules externes proposés dans cette extension, vous devez d’abord initialiser les modules externes que vous prévoyez d’utiliser selon leurs propres règles.

1. Créez une nouvelle règle.
1. Ajoutez l’événement Core - bibliothèque chargée (haut de page).
1. Utilisez l’une des méthodes d’initialisation ci-dessous.

## Types d’action de l’extension de modules externes courants Analytics

Cette section décrit les types d’action disponible dans l’extension de modules externes courants Analytics

L’extension de modules externes courants Analytics propose les actions suivantes :

* [Initialiser](#initialize)
* [Initialiser le module externe](#initialize-plugin)

### Initialiser

>[!IMPORTANT]
>
>Bien que l’implémentation de cette action soit plus facile, Adobe Consulting ne vous recommande pas d’utiliser cette action, car celle-ci augmente le poids du module externe.

Avec cette action, vous pouvez sélectionner chaque module externe que vous souhaitez inclure dans votre implémentation et enregistrer les modifications. Sélectionnez autant ou aussi peu que vous prévoyez d’en utiliser lors de la mise en œuvre.

### Initialiser le module externe

Ces actions initialisent les modules externes spécifiques que vous prévoyez d’utiliser un par un. Pour initialiser l’ensemble des modules externes que vous prévoyez d’utiliser dans votre propriété, ajoutez simplement l’action correspondante à votre règle, puis enregistrez-la. Bien que configurer l’extension de cette manière demande plus d’efforts, elle rend le code plus efficace. Adobe vous recommande donc cette approche.

## Éléments de données de l’extension de modules externes courants Analytics

Les éléments de données suivants sont disponibles dans l’extension de modules externes courants Analytics, qui tire parti des fonctionnalités de balises pour définir et configurer leurs modules externes correspondants dans Analytics :

* `getGeoCoordinates`
* `getNewRepeat`
* `getPageName`
* `getResponsiveLayout`
* `getTimeParting`
* `getTimeSinceLastVisit`
* `getVisitDuration`
* `getVisitNum`

>[!NOTE]
>
>Pour plus d’informations sur les modules externes ci-dessus, consultez la [documentation d’Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=fr).
