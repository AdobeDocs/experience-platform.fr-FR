---
keywords: Experience Platform ; profil ; profil du client en temps réel ; interface utilisateur ; interface utilisateur ; personnalisation ; tableau de bord de profil ; tableau de bord
title: Tableau de bord Destinations
description: Adobe Experience Platform fournit un tableau de bord par lequel vous pouvez afficher des informations importantes sur les destinations actives de votre entreprise.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: a920e8aaccb4da6a3aa08f0d420cee0d1944ab9a
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 5%

---

# [!UICONTROL Destinations] tableau de bord

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord qui vous permet d’afficher des informations importantes sur les destinations actives de votre entreprise, telles qu’elles ont été capturées lors d’un instantané quotidien. Ce guide explique comment accéder au tableau de bord de destinations dans l’interface utilisateur et comment l’utiliser. Il fournit également des informations supplémentaires sur les mesures affichées dans le tableau de bord.

Pour une vue d’ensemble des destinations, ainsi qu’un catalogue de toutes les destinations disponibles dans l’Experience Platform, consultez la page [documentation sur les destinations](../../destinations/home.md).

## [!UICONTROL Destinations] données du tableau de bord {#destinations-dashboard-data}

Le [!UICONTROL Destinations] tableau de bord affiche un instantané des destinations que votre organisation a activées dans l’Experience Platform. Les données de lʼinstantané montrent les données exactement comme elles apparaissent au moment précis où lʼinstantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et le tableau de bord des destinations n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord des destinations

Pour accéder au tableau de bord des destinations dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Destinations]** dans le rail de gauche, puis sélectionnez l’option **[!UICONTROL Présentation]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre entreprise est une entreprise nouvelle à Experience Platform et n’a pas encore de destination active, la [!UICONTROL Destinations] tableau de bord et [!UICONTROL Présentation] ne sont pas visibles. Au lieu de cela, sélectionnez [!UICONTROL Destinations] de la navigation de gauche affiche la [!UICONTROL Catalogue] . Pour en savoir plus sur le [!UICONTROL Catalogue] , reportez-vous à la section [[!UICONTROL Destinations] guide de l’espace de travail](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Modification du tableau de bord des destinations

Vous pouvez modifier l’aspect du tableau de bord de destination en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord, ainsi que d’accéder au **[!UICONTROL Bibliothèque de widgets]** pour explorer les widgets disponibles et créer des widgets personnalisés pour votre entreprise.

Veuillez vous référer au [modification des tableaux de bord](../customize/modify.md) et [présentation de la bibliothèque de widgets](../customize/widget-library.md) pour en savoir plus.

## Widgets standard

Adobe fournit plusieurs widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos destinations. Vous pouvez également créer des widgets personnalisés à partager avec votre organisation à l’aide de la [!UICONTROL Bibliothèque de widgets]. Pour en savoir plus sur la création de widgets personnalisés, lisez d’abord la section [présentation de la bibliothèque de widgets](../customize/widget-library.md).

Pour en savoir plus sur chacun des widgets standard disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [[!UICONTROL Destinations les plus utilisées]](#most-used-destinations)
* [[!UICONTROL Destinations récemment créées]](#recently-created-destinations)
* [[!UICONTROL Segments récemment activés]](#recently-activated-segments)

### [!UICONTROL Destinations les plus utilisées] {#most-used-destinations}

Le **[!UICONTROL Destinations les plus utilisées]** le widget affiche les destinations principales de votre organisation par nombre de segments mappés, à compter du dernier instantané. Ce classement donne un aperçu des destinations utilisées, tout en montrant celles qui pourraient être sous-utilisées.

Par exemple, si vous avez configuré une destination hier mais n’avez mappé aucun segment avec celle-ci, vous pouvez voir que la destination est actuellement sous-utilisée.

Le nombre de segments mappés affiché dans la colonne Nombre de segments est exact à partir du dernier instantané quotidien. Le mappage d’un nouveau segment vers la destination ne met pas à jour le nombre tant que l’instantané suivant n’est pas pris.

Si vous sélectionnez le nom d’une destination dans la liste affichée sur le widget, vous accédez aux détails de destination comme étant liés à partir de la **[!UICONTROL Parcourir]** . Vous pouvez également sélectionner **[!UICONTROL Tout afficher]** pour accéder à la **[!UICONTROL Parcourir]** , puis sélectionnez le nom d’une destination pour afficher ses détails.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinations récemment créées] {#recently-created-destinations}

Le **[!UICONTROL Destinations récemment créées]** vous permet d’afficher la liste des destinations de votre organisation les plus récemment configurées.

La date de création indiquée est exacte pour le dernier instantané quotidien. En d’autres termes, si vous créez une nouvelle destination, elle n’apparaîtra dans la liste qu’une fois l’instantané suivant pris.

Si vous sélectionnez le nom d’une destination dans la liste affichée sur le widget, vous accédez aux détails de destination comme étant liés à partir de la **[!UICONTROL Parcourir]** . Vous pouvez également sélectionner **[!UICONTROL Tout afficher]** pour accéder à la **[!UICONTROL Parcourir]** , puis sélectionnez le nom d’une destination pour afficher ses détails.

Pour en savoir plus sur la configuration de types de destinations spécifiques, consultez la page [documentation sur les destinations](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segments récemment activés] {#recently-activated-segments}

Le **[!UICONTROL Segments récemment activés]** fournit une liste des derniers segments mappés vers une destination. Cette liste fournit un instantané des segments et des destinations activement utilisés dans le système et peut aider à dépanner les mappages erronés.

La date mise à jour affiche la dernière fois que le segment a été activé vers la destination et est exacte au dernier instantané quotidien. En d’autres termes, si vous activez un segment vers la destination, la date mise à jour ne changera pas tant que la prochaine capture d’écran n’aura pas été effectuée.

La sélection du nom d’un segment dans la liste affichée sur le widget vous amène aux détails du segment. Vous pouvez également sélectionner **[!UICONTROL Tout afficher]** pour accéder à l’onglet de navigation des segments, puis sélectionnez le nom d’un segment pour afficher ses détails.

Pour plus d’informations sur l’utilisation des segments dans l’Experience Platform, veuillez commencer par lire la section [Présentation du service de segmentation](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant être en mesure de localiser le tableau de bord des destinations et de comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des destinations dans l’Experience Platform, consultez la section [documentation sur les destinations](../../destinations/home.md).
