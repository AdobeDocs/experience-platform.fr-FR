---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;interface utilisateur;personnalisation;tableau de bord du profil;tableau de bord
title: Tableau de bord des destinations
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les destinations principales de votre entreprise.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 6%

---

#  Tableau de bord des destinations

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les destinations principales de votre entreprise, telles qu’elles sont capturées lors d’un instantané quotidien. Ce guide explique comment accéder au tableau de bord des destinations et l’utiliser dans l’interface utilisateur. Il fournit également des informations supplémentaires sur les mesures affichées dans le tableau de bord.

Pour obtenir un aperçu des destinations, ainsi qu’un catalogue de toutes les destinations disponibles dans Experience Platform, consultez la [documentation sur les destinations](../../destinations/home.md).

##  Données du tableau de bord Destinations  {#destinations-dashboard-data}

Le tableau de bord [!UICONTROL Destinations] affiche un instantané des destinations que votre entreprise a activées dans Experience Profile. Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et le tableau de bord des destinations n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord des destinations

Pour accéder au tableau de bord des destinations dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Destinations]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Aperçu]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre entreprise est une nouvelle société Experience Platform qui ne possède pas encore de destinations principales, le tableau de bord [!UICONTROL Destinations] et l’onglet [!UICONTROL Aperçu] ne sont pas visibles. À la place, la sélection de [!UICONTROL Destinations] dans le volet de navigation de gauche affiche l’onglet [!UICONTROL Catalogue] . Pour en savoir plus sur l’onglet [!UICONTROL Catalogue], consultez le [[!UICONTROL Guide de l’espace de travail des ] ](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

## Widgets disponibles

Experience Platform fournit plusieurs widgets que vous pouvez utiliser pour visualiser différentes mesures liées à vos destinations. Pour en savoir plus, sélectionnez le nom d’un widget ci-dessous :

* [[!UICONTROL Destinations les plus utilisées]](#most-used-destinations)
* [[!UICONTROL Destinations créées récemment]](#recently-created-destinations)
* [[!UICONTROL Segments récemment activés]](#recently-activated-segments)

### [!UICONTROL Destinations les plus utilisées] {#most-used-destinations}

Le widget **[!UICONTROL Destinations les plus utilisées]** affiche les principales destinations de votre entreprise par nombre de segments mappés, à partir du dernier instantané. Ce classement permet de savoir quelles destinations sont utilisées, tout en présentant éventuellement celles qui peuvent être sous-utilisées.

Par exemple, si vous avez configuré une destination hier mais que vous ne lui avez mappé aucun segment, vous pouvez constater que la destination est actuellement sous-utilisée.

Le nombre de segments mappés affichés dans la colonne du nombre de segments est précis à partir du dernier instantané quotidien. Le mappage d’un nouveau segment à la destination ne met pas à jour le nombre tant que l’instantané suivant n’a pas été pris.

Si vous sélectionnez le nom d’une destination dans la liste affichée sur le widget, vous accédez aux détails de la destination tels que liés à partir de l’onglet **[!UICONTROL Parcourir]** . Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder à l’onglet **[!UICONTROL Parcourir]** , puis sélectionner le nom d’une destination pour afficher ses détails.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinations créées récemment] {#recently-created-destinations}

Le widget **[!UICONTROL Destinations récemment créées]** vous permet d’afficher la liste des destinations configurées le plus récemment par votre entreprise.

La date de création affichée est exacte par rapport au dernier instantané quotidien. En d’autres termes, si vous créez une destination, elle n’apparaîtra pas dans la liste tant que l’instantané suivant n’aura pas été pris.

Si vous sélectionnez le nom d’une destination dans la liste affichée sur le widget, vous accédez aux détails de la destination tels que liés à partir de l’onglet **[!UICONTROL Parcourir]** . Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder à l’onglet **[!UICONTROL Parcourir]** , puis sélectionner le nom d’une destination pour afficher ses détails.

Pour en savoir plus sur la configuration de types de destinations spécifiques, consultez la [documentation sur les destinations](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segments récemment activés] {#recently-activated-segments}

Le widget **[!UICONTROL Segments récemment activés]** fournit une liste des segments mappés le plus récemment à une destination. Cette liste fournit un instantané des segments et des destinations utilisés activement dans le système et peut vous aider à résoudre les problèmes de mappages erronés.

La date mise à jour affichée affiche la dernière fois que le segment a été activé vers la destination et est précis par rapport au dernier instantané quotidien. En d’autres termes, si vous activez un segment vers la destination, la date mise à jour ne changera pas tant que l’instantané suivant n’aura pas été pris.

Si vous sélectionnez le nom d’un segment dans la liste affichée sur le widget, vous accédez aux détails du segment. Vous pouvez également sélectionner **[!UICONTROL Afficher tout]** pour accéder à l’onglet de navigation du segment, puis sélectionner le nom d’un segment pour en afficher les détails.

Pour plus d’informations sur l’utilisation des segments dans Experience Platform, commencez par lire la [présentation de Segmentation Service](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord des destinations et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des destinations en Experience Platform, consultez la [documentation sur les destinations](../../destinations/home.md).
