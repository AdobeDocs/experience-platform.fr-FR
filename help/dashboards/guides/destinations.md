---
keywords: Experience Platform ; profil ; profil client en temps réel ; interface utilisateur ; interface utilisateur ; personnalisation ; tableau de bord profil ; tableau de bord
title: Tableau de bord Destinations
description: Adobe Experience Platform fournit un tableau de bord par lequel vous pouvez vue des informations importantes sur les principales destinations de votre entreprise.
topic-legacy: guide
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# (bêta) [!UICONTROL tableau de bord Destinations]

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord décrite dans ce document est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord par lequel vous pouvez vue des informations importantes sur les principales destinations de votre entreprise, telles qu’elles sont capturées au cours d’un instantané quotidien. Ce guide décrit comment accéder au tableau de bord de destination et l’utiliser dans l’interface utilisateur et fournit plus d’informations sur les mesures affichées dans le tableau de bord.

Pour un aperçu des destinations, ainsi qu&#39;un catalogue de toutes les destinations disponibles dans l&#39;Experience Platform, veuillez visiter le [aperçu des destinations](../../destinations/home.md).

## [!UICONTROL Données ] du tableau de bord Destinations  {#destinations-dashboard-data}

Le tableau de bord [!UICONTROL Destinations] affiche un instantané des destinations que votre organisation a activées dans le Profil d’expérience. Les données de l&#39;instantané affichent les données exactement telles qu&#39;elles s&#39;affichent au moment précis où l&#39;instantané a été pris. En d&#39;autres termes, l&#39;instantané n&#39;est pas une approximation ou un échantillon des données et le tableau de bord de destination n&#39;est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis l&#39;instantané ne seront pas répercutées dans le tableau de bord tant que l&#39;instantané suivant n&#39;aura pas été pris.

## Exploration du tableau de bord de destination

Pour accéder au tableau de bord de destinations dans l’interface utilisateur de la plateforme, sélectionnez **[!UICONTROL Destinations]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Aperçu]** pour afficher le tableau de bord.

![](../images/destinations/dashboard-overview.png)

## Widgets disponibles

Experience Platform fournit plusieurs widgets que vous pouvez utiliser pour visualiser différentes mesures liées à vos destinations. Sélectionnez le nom d’un widget ci-dessous pour en savoir plus :

* [[!UICONTROL Destinations les plus utilisées]](#most-used-destinations)
* [[!UICONTROL Destinations récemment créées]](#recently-created-destinations)
* [[!UICONTROL Segments récemment activés]](#recently-activated-segments)

### [!UICONTROL Destinations les plus utilisées] {#most-used-destinations}

Le widget **[!UICONTROL Destinations les plus utilisées]** affiche les principales destinations de votre entreprise par nombre de segments mappés, à partir du dernier instantané. Ce classement permet de savoir quelles destinations sont utilisées tout en montrant celles qui peuvent être sous-utilisées.

Par exemple, si vous avez configuré hier une destination sans y avoir mappé de segments, vous pouvez constater que la destination est actuellement sous-utilisée.

Le nombre de segments mappés affichés dans la colonne Nombre de segments est exact à partir du dernier instantané quotidien. Le mappage d’un nouveau segment à la destination ne met pas à jour le décompte tant que l’instantané suivant n’a pas été effectué.

La sélection du nom d’une destination à partir de la liste affichée sur le widget vous conduit aux détails de destination tels qu’ils sont liés à partir de l’onglet **[!UICONTROL Parcourir]**. Vous pouvez également sélectionner **[!UICONTROL Vue All]** pour accéder à l&#39;onglet **[!UICONTROL Parcourir]**, puis sélectionner le nom d&#39;une destination pour en vue les détails.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinations récemment créées] {#recently-created-destinations}

Le widget **[!UICONTROL Destinations récemment créées]** vous permet d&#39;afficher une liste des destinations de votre entreprise les plus récemment configurées.

La date de création affichée est précise par rapport au dernier instantané quotidien. En d’autres termes, si vous créez une destination, elle n’apparaîtra dans la liste qu’après la prise de l’instantané suivant.

La sélection du nom d’une destination à partir de la liste affichée sur le widget vous conduit aux détails de destination tels qu’ils sont liés à partir de l’onglet **[!UICONTROL Parcourir]**. Vous pouvez également sélectionner **[!UICONTROL Vue All]** pour accéder à l&#39;onglet **[!UICONTROL Parcourir]**, puis sélectionner le nom d&#39;une destination pour en vue les détails.

Pour en savoir plus sur la configuration de types de destinations spécifiques, consultez la [documentation sur les destinations](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segments récemment activés] {#recently-activated-segments}

Le widget **[!UICONTROL Segments récemment activés]** fournit une liste des segments les plus récemment mappés à une destination. Cette liste fournit un instantané des segments et destinations activement utilisés dans le système et peut vous aider à résoudre les problèmes de mappage.

La date mise à jour affichée affiche la dernière fois que le segment a été activé sur la destination et est précise sur le dernier instantané quotidien. En d’autres termes, si vous activez un segment vers la destination, la date mise à jour ne changera pas tant que l’instantané suivant n’aura pas été effectué.

La sélection du nom d’un segment dans la liste affichée sur le widget vous amène aux détails du segment. Vous pouvez également sélectionner **[!UICONTROL Vue tout]** pour accéder à l’onglet de navigation des segments, puis sélectionner le nom d’un segment pour en vue les détails.

Pour plus d&#39;informations sur l&#39;utilisation des segments dans l&#39;Experience Platform, veuillez commencer par lire l&#39;[Présentation du service de segmentation](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant être en mesure de localiser le tableau de bord de destinations et de comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l&#39;utilisation des destinations en Experience Platform, consultez la [documentation sur les destinations](../../destinations/home.md).
