---
keywords: présentation des mesures ; Présentation des mesures rtcdp
title: Page d’accueil et tableaux de bord Real-time Customer Data Platform
description: Tableaux de bord, page d’accueil et première expérience client d’Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 63%

---

# [!DNL Real-Time Customer Data Platform] page d’accueil et tableaux de bord

La page d’accueil d’Adobe Real-time Customer Data Platform (Real-Time CDP), qui comprend un tableau de bord de mesures, s’affiche lorsque vous vous connectez à Real-Time CDP.

La page d’accueil n’est qu’un des emplacements où les cartes de mesures apparaissent. Real-Time CDP fournit des cartes de mesure tout au long de votre expérience. Ces mesures indiquent les données, les profils et les audiences de segments du système.

![image](assets/home.png)

Si le système ne contient aucune donnée lorsque vous vous connectez à Real-Time CDP, le tableau de bord de la page d’accueil n’apparaît pas. Dans ce cas, la page d’accueil propose des ressources pédagogiques pour une première expérience client. Au fur et à mesure de la collecte des données (c’est-à-dire au fur et à mesure de la création <!--sources-->des jeux de données, profils, segments et destinations ainsi que de la transmission des données au système), le tableau de bord se met automatiquement à jour pour afficher les informations sur ces données<!-- in metric cards-->.

## Affichage du tableau de bord de la page d’accueil

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

Le tableau de bord se divise en plusieurs parties<!-- two areas.--> :

* **Le tableau de classement** occupe toute la partie supérieure du tableau de bord. Le tableau de classement indique le nombre de jeux de données, de profils, de segments et de destinations du système.

   ![image](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* La section **Éléments récents** répertorie les cinq jeux de données, sources, segments et destinations ajoutés le plus récemment au système.

   ![image](assets/recent.png)

D’autres mesures, par exemple pour les profils et les segments, sont disponibles dans d’autres parties de Real-time Customer Data Platform.

### Jeux de données

Le **[!UICONTROL Jeux de données]** Le compteur affiche le nombre de jeux de données dans le système et la quantité de données dans [!DNL Platform]. Ce compteur est mis à jour lors de la création d’un jeu de données.

Pour plus d’informations sur les jeux de données, consultez la [présentation des jeux de données](../catalog/datasets/overview.md).

### Profils

Le **[!UICONTROL Profils]** count affiche le nombre total de personnes avec des profils dans la variable [!DNL Real-time Customer Profile]. Il n’inclut pas les fragments de profil. Il s’agit de votre audience adressable totale.

Ce compte utilise la [stratégie de fusion](profile/merge-policies.md) par défaut telle que définie dans la configuration de la stratégie de fusion du profil unifié.

Le nombre de profils est mis à jour une fois toutes les 24 heures.

Pour plus d’informations sur les profils, voir [Une vue unifiée de votre client dans Real-Time CDP](profile/profile-overview.md).

### Segments

La section **[!UICONTROL Segments]** indique le nombre total de segments créés pour l’organisation. Ce nombre est mis à jour lors de la création de segments.

Pour plus d’informations sur les segments, consultez [Présentation de Segmentation Service](segmentation/segmentation-overview.md).

### Destinations

La section **[!UICONTROL Destinations]** indique le nombre total de destinations créées pour l’organisation. Ce nombre est mis à jour lors de la création de destinations.

Pour plus d’informations sur les destinations, consultez [Présentation des destinations](destinations/overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Jeux de données récents

La carte **[!UICONTROL Jeux de données récents]** montre les cinq jeux de données créés le plus récemment dans l’entreprise. Cette liste est mise à jour lors de la création d’un jeu de données.

Sélectionnez un jeu de données pour afficher les détails de cet élément, ou **[!UICONTROL Afficher tout]** pour afficher la liste des jeux de données. À partir de là, vous pouvez sélectionner une source spécifique pour plus de détails.

Pour plus d’informations sur les jeux de données, consultez la [présentation des jeux de données](../catalog/datasets/overview.md).

### Sources récentes

La carte de mesure **[!UICONTROL Sources récentes]** montre les cinq sources créées le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’une source.

Sélectionnez une source pour afficher les détails de cet élément, ou **[!UICONTROL Afficher tout]** pour afficher la liste des sources. À partir de là, vous pouvez sélectionner une source spécifique pour plus de détails.

Pour plus d’informations sur les sources, consultez [Présentation des sources](sources/sources-overview.md).

### Segments récents

La carte de mesure **[!UICONTROL Segments récents]** montre les cinq segments créés le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’un segment.

Sélectionnez un segment pour afficher les détails de cet élément, ou **[!UICONTROL Afficher tout]** pour afficher des informations sur d’autres segments.

Pour plus d’informations sur les segments, consultez [Présentation de Segmentation Service](segmentation/segmentation-overview.md).

### Destinations récentes

La carte de mesure **[!UICONTROL Destinations récentes]** montre les cinq destinations créées le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’une destination.

Sélectionnez une destination pour afficher les détails de cet élément, ou **[!UICONTROL Afficher tout]** pour afficher des informations sur d’autres destinations.

Pour plus d’informations sur les destinations, consultez [Présentation des destinations](destinations/overview.md).
