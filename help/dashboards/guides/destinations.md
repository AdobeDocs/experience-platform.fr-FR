---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;interface utilisateur;personnalisation;tableau de bord du profil;tableau de bord
title: Tableau de bord des destinations
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les destinations principales de votre entreprise.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 8571d86e1ce9dc894e54fe72dea75b9f8fe84f0b
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 5%

---

# [!UICONTROL Destinations] tableau de bord

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les destinations principales de votre entreprise, telles qu’elles sont capturées lors d’un instantané quotidien. Ce guide explique comment accéder au tableau de bord des destinations et l’utiliser dans l’interface utilisateur. Il fournit également des informations supplémentaires sur les mesures affichées dans le tableau de bord.

Pour obtenir un aperçu des destinations, ainsi qu’un catalogue de toutes les destinations disponibles dans Experience Platform, veuillez consulter le [documentation sur les destinations](../../destinations/home.md).

## [!UICONTROL Destinations] données du tableau de bord {#destinations-dashboard-data}

Le [!UICONTROL Destinations] Le tableau de bord affiche un instantané des destinations que votre entreprise a activées dans Experience Platform. Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et le tableau de bord des destinations n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord des destinations

Pour accéder au tableau de bord des destinations dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Destinations]** dans le rail de gauche, puis sélectionnez l’option **[!UICONTROL Présentation]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre entreprise est une nouvelle société qui n’a pas encore de destinations principales, la variable [!UICONTROL Destinations] tableau de bord et [!UICONTROL Présentation] ne sont pas visibles. À la place, sélectionnez [!UICONTROL Destinations] dans le volet de navigation de gauche affiche le [!UICONTROL Catalogue] . Pour en savoir plus sur la variable [!UICONTROL Catalogue] , voir [[!UICONTROL Destinations] guide de workspace](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Modification du tableau de bord des destinations

Vous pouvez modifier l’aspect du tableau de bord des destinations en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord, ainsi que d’accéder au **[!UICONTROL Bibliothèque de widgets]** pour explorer les widgets disponibles et créer des widgets personnalisés pour votre organisation.

Reportez-vous à la section [modification des tableaux de bord](../customize/modify.md) et [Présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

## Widgets standard

Adobe fournit plusieurs widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos destinations. Vous pouvez également créer des widgets personnalisés à partager avec votre organisation à l’aide de la variable [!UICONTROL Bibliothèque de widgets]. Pour en savoir plus sur la création de widgets personnalisés, commencez par lire le [Présentation de la bibliothèque de widgets](../customize/widget-library.md).

Pour en savoir plus sur chacun des widgets standard disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [[!UICONTROL Destinations les plus utilisées]](#most-used-destinations)
* [[!UICONTROL Destinations créées récemment]](#recently-created-destinations)
* [[!UICONTROL Segments récemment activés]](#recently-activated-segments)

### [!UICONTROL Destinations les plus utilisées] {#most-used-destinations}

Le **[!UICONTROL Destinations les plus utilisées]** le widget affiche les principales destinations de votre entreprise par nombre de segments mappés, à partir du dernier instantané. Ce classement permet de savoir quelles destinations sont utilisées, tout en présentant éventuellement celles qui peuvent être sous-utilisées.

Par exemple, si vous avez configuré une destination hier mais que vous ne lui avez mappé aucun segment, vous pouvez constater que la destination est actuellement sous-utilisée.

Le nombre de segments mappés affichés dans la colonne du nombre de segments est précis à partir du dernier instantané quotidien. Le mappage d’un nouveau segment à la destination ne met pas à jour le nombre tant que l’instantané suivant n’a pas été pris.

Si vous sélectionnez le nom d’une destination dans la liste affichée sur le widget, vous accédez aux détails de destination tels que liés à partir de la variable **[!UICONTROL Parcourir]** . Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder au **[!UICONTROL Parcourir]** puis sélectionnez le nom d’une destination pour en afficher les détails.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinations créées récemment] {#recently-created-destinations}

Le **[!UICONTROL Destinations créées récemment]** vous permet d’afficher la liste des destinations configurées le plus récemment par votre entreprise.

La date de création affichée est exacte par rapport au dernier instantané quotidien. En d’autres termes, si vous créez une destination, elle n’apparaîtra pas dans la liste tant que l’instantané suivant n’aura pas été pris.

Si vous sélectionnez le nom d’une destination dans la liste affichée sur le widget, vous accédez aux détails de destination tels que liés à partir de la variable **[!UICONTROL Parcourir]** . Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder au **[!UICONTROL Parcourir]** puis sélectionnez le nom d’une destination pour en afficher les détails.

Pour en savoir plus sur la configuration de types de destinations spécifiques, consultez la page [documentation sur les destinations](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segments récemment activés] {#recently-activated-segments}

Le **[!UICONTROL Segments récemment activés]** fournit une liste des segments mappés le plus récemment à une destination. Cette liste fournit un instantané des segments et des destinations utilisés activement dans le système et peut vous aider à résoudre les problèmes de mappages erronés.

La date mise à jour affichée affiche la dernière fois que le segment a été activé vers la destination et est précis par rapport au dernier instantané quotidien. En d’autres termes, si vous activez un segment vers la destination, la date mise à jour ne changera pas tant que l’instantané suivant n’aura pas été pris.

Si vous sélectionnez le nom d’un segment dans la liste affichée sur le widget, vous accédez aux détails du segment. Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder à l’onglet navigation des segments, sélectionnez ensuite le nom d’un segment afin d’en afficher les détails.

Pour plus d’informations sur l’utilisation des segments dans Experience Platform, commencez par lire le [Présentation de Segmentation Service](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord des destinations et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des destinations dans Experience Platform, reportez-vous à la section [documentation sur les destinations](../../destinations/home.md).
