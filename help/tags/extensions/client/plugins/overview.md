---
title: Présentation de l’extension Common Analytics
description: Découvrez l’extension de balises Common Analytics dans Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '354'
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
