---
title: Présentation de l’extension Common Analytics
description: Découvrez l’extension de balises Common Analytics dans Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 100%

---

# Présentation de l’extension de modules externes courants Analytics

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

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

Avec cette action, vous pouvez sélectionner chaque module externe que vous souhaitez inclure dans votre implémentation et enregistrer les modifications. Sélectionnez tout ou partie des modules externes que vous prévoyez d’utiliser au cours de cette implémentation. Vous trouverez des liens renvoyant vers la documentation d’utilisation et une description rapide de chaque module externe dans l’[aperçu des modules externes](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=fr) d’Analytics.

### Initialiser le module externe

Ces actions initialisent les modules externes spécifiques que vous prévoyez d’utiliser un par un. Pour initialiser l’ensemble des modules externes que vous prévoyez d’utiliser dans votre propriété, ajoutez simplement l’action correspondante à votre règle, puis enregistrez-la. Bien que configurer l’extension de cette manière demande plus d’efforts, elle rend le code plus efficace. Adobe vous recommande donc cette approche.

## Éléments de données de l’extension de modules externes courants Analytics

Cette section décrit les éléments de données disponibles dans l’extension de modules externes courants Analytics.

### getGeoCoordinates

Permet aux utilisateurs d’utiliser l’interface utilisateur native de la collecte de données d’Adobe Experience Platform pour configurer le plug-in getGeoCoordinates.

### getNewRepeat

Permet aux utilisateurs de tirer profit de l’interface utilisateur native de la collecte de données pour définir et configurer le plug-in getNewRepeat.

### getPageName

Permet aux utilisateurs de tirer profit de l’interface utilisateur native de la collecte de données pour définir et configurer le plug-in getPageName.

### getResponsiveLayout

Permet aux utilisateurs de tirer profit de l’interface utilisateur native de la collecte de données pour définir et configurer le plug-in getResponsiveLayout.

### getTimeParting

Permet aux utilisateurs de tirer profit de l’interface utilisateur native de collecte de données pour définir et configurer le plug-in getTimeParting.

### getTimeSinceLastVisit

Permet aux utilisateurs de tirer profit de l’interface utilisateur native de la collecte de données pour définir et configurer le plug-in getTimeSinceLastVisit.

### getVisitDuration

Permet aux utilisateurs de tirer profit de l’interface utilisateur native de la collecte de données pour définir et configurer le plug-in getVisitDuration.

### getVisitNum

Permet aux utilisateurs de tirer profit de l’interface utilisateur native de la collecte de données pour définir et configurer le plug-in getVisitNum.
