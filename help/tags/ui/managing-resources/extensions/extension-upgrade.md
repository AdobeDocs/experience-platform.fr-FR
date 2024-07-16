---
title: Mises à niveau des extensions
description: Découvrez comment les mises à niveau d’extension sont mises en package et représentées dans le catalogue d’extensions.
exl-id: 4a7e0c5c-4bd1-4fb8-8509-f88a0aa42ac4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 100%

---

# Mises à niveau des extensions

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les développeurs d’extensions ajoutent constamment de nouvelles fonctionnalités à leurs extensions et corrigent fréquemment les bogues. Ces mises à jour sont incluses dans de nouvelles versions d’une extension et mises à disposition dans le catalogue sous forme de mises à niveau.

## Catalogue d’extensions

Lorsqu’un développeur d’extensions a fourni une nouvelle version de l’extension, cette nouvelle version devient disponible dans le catalogue d’extensions. Le catalogue affiche uniquement la version la plus récente d’une extension. Vous ne pouvez pas installer une autre version d’extension que `latest`.

Lorsque vous installez une extension sur votre propriété, la version actuellement disponible est installée et votre propriété demeure avec cette version spécifique à partir de ce moment, même si des versions plus récentes sont ajoutées au catalogue.

## Notifications de mise à niveau

Lorsque vous avez installé une extension sur votre propriété et qu’une nouvelle version est disponible dans le catalogue, un bouton [!UICONTROL Mettre à niveau] s’affiche sur la carte d’extension lorsque vous affichez la page des extensions installées.

Vous remarquerez également un avertissement lorsque vous modifiez des ressources fournies par cette extension.

## Les mises à niveau sont permanentes

Si vous souhaitez effectuer une mise à niveau vers une version plus récente disponible dans le catalogue, vous devez installer cette mise à niveau vous-même. Une mise à niveau est une « modification » qui doit être ajoutée à une bibliothèque, testée et publiée avant d’affecter vos balises déployées.

La mise à niveau ne doit pas être prise à la légère. Vous ne devez pas effectuer de mise à niveau, sauf si vous êtes prêt à tester la nouvelle extension et à la déployer. Une fois la mise à niveau ajoutée à votre propriété, elle doit être incluse dans toutes les bibliothèques. Toute bibliothèque qui n’inclut pas l’extension mise à niveau va échouer au moment de la génération.

Il n’existe actuellement aucune possibilité de rétrograder votre extension vers une version précédente. Une fois que vous avez effectué la mise à niveau (que vous ayez effectué une publication ou non), la nouvelle version de l’extension se trouve sur votre propriété pour y rester.

## Processus de mise à niveau

L’installation d’une mise à niveau est presque identique à l’installation de l’extension pour la première fois.

1. Sélectionnez **[!UICONTROL Mettre à niveau]** pour accéder à l’écran [!UICONTROL Configuration de l’extension].
1. Apportez les modifications de configuration souhaitées.
1. Sélectionnez **[!UICONTROL Enregistrer]**.

La mise à niveau ne s’effectue réellement que lorsque vous appuyez sur **[!UICONTROL Enregistrer]**. Avant cela, vous pouvez cliquer à tout moment sur [!UICONTROL Annuler] et conserver la version installée. Un clic sur **[!UICONTROL Enregistrer]** représente un point de non-retour.

Les mises à niveau d’extension ne sont pas autorisées si vous disposez d’une bibliothèque à l’état `Approved` ou `Submitted`. Cela s’explique par le fait que le build suivant doit contenir la nouvelle version de l’extension. Dans le cas d’une bibliothèque `Approved` ou `Submitted`, le prochain build est le build d’exploitation. Ce build échouerait, car il ne contiendrait pas la dernière version. Le workflow consiste donc à publier ou à rejeter les bibliothèques à l’état `Approved` ou `Submitted`_avant_ la mise à niveau de l’extension.

## Publication d’une mise à niveau

Une fois l’extension mise à niveau installée sur votre propriété, vous devez l’inclure dans toutes les bibliothèques. Un message d’échec de génération s’affiche pour toutes les bibliothèques qui ne l’incluent pas.

En outre, l’ajout de l’extension mise à niveau à votre bibliothèque est identique à [l’ajout de toute autre modification](../../publishing/libraries.md) à une bibliothèque.

Dans l’écran [!UICONTROL Modifier la bibliothèque], vous pouvez utiliser le bouton « [!UICONTROL Ajouter toutes les ressources modifiées] » ou le bouton « [!UICONTROL Ajouter une ressource] » et sélectionner uniquement l’extension mise à niveau.

>[!TIP]
>
>Les développeurs d’extensions peuvent ajouter de nouveaux éléments de configuration à leurs vues d’extension afin d’activer une nouvelle fonctionnalité. Si vous constatez des échecs de génération après la mise à niveau vers une nouvelle version d’extension, et si vous les avez isolés pour cette extension, la première chose à faire est d’accéder à la page Configure (Configurer) de l’extension et de veiller à enregistrer (même si vous n’avez rien modifié). Ajoutez ensuite la nouvelle modification à votre bibliothèque et essayez à nouveau de procéder à la génération.

Une fois que vous avez ajouté la mise à niveau de l’extension à votre bibliothèque, vous pouvez suivre la procédure décrite dans le [flux de publication](../../publishing/publishing-flow.md) pour publier votre bibliothèque jusqu’en production.
