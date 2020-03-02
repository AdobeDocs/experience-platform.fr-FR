---
title: Page d’accueil et tableaux de bord de la plateforme de données client en temps réel
seo-title: Page d’accueil et tableaux de bord de la plateforme de données client en temps réel
description: Tableaux de bord, page d’accueil et première expérience client d’Adobe Experience Platform
seo-description: Tableaux de bord, page d’accueil et première expérience client d’Adobe Experience Platform
translation-type: ht
source-git-commit: 6dde6c90fe9073c50c0a9d3dd43ef045730d1e13

---


# Présentation des mesures de la plateforme de données client en temps réel

La page d’accueil de la plateforme de données client (CDP) en temps réel d’Adobe inclut un tableau de bord de mesures et s’affiche lorsque vous vous connectez à la plateforme CDP en temps réel.

La page d’accueil n’est qu’un des emplacements où les cartes de mesures apparaissent. La plateforme CDP en temps réel fournit des cartes de mesure tout au long de votre expérience. Ces mesures indiquent les données, les profils et les audiences de segments du système.

![image](assets/home2.jpg)

Si le système ne contient aucune donnée lorsque vous vous connectez à la plateforme CDP en temps réel, le tableau de bord de la page d’accueil n’apparaît pas. Dans ce cas, la page d’accueil propose des ressources pédagogiques pour une première expérience client. Au fur et à mesure de la collecte des données (c’est-à-dire au fur et à mesure de la création <!--sources-->des jeux de données, profils, segments et destinations ainsi que de la transmission des données au système), le tableau de bord se met automatiquement à jour pour afficher les informations sur ces données<!-- in metric cards-->.

## Affichage du tableau de bord de la page d’accueil

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

Le tableau de bord se divise en plusieurs parties<!-- two areas.--> :

* **Le tableau de classement** occupe toute la partie supérieure du tableau de bord. Le tableau de classement indique le nombre de jeux de données, de profils, de segments et de destinations du système.

   ![image](assets/home-leaderboard2.jpg)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* La section **Éléments récents** répertorie les cinq jeux de données, sources, segments et destinations ajoutés le plus récemment au système.

   ![image](assets/home-recent.jpg)

D’autres mesures, par exemple pour les profils et les segments, sont disponibles dans d’autres parties de la plateforme de données client en temps réel.

### Jeux de données

Le compteur **[!UICONTROL Jeux de données]** indique le nombre de jeux de données du système et la quantité de données de la plateforme. Ce compteur est mis à jour lors de la création d’un jeu de données.

Pour plus d’informations sur les jeux de données, consultez [Ingestion de données dans Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md).

### Profils

Le compte **[!UICONTROL Profils]** indique le nombre total de personnes disposant de profils dans le profil client en temps réel. Il n’inclut pas les fragments de profil. Il s’agit de votre audience adressable totale.

Ce compte utilise la [stratégie de fusion](profile/merge-policies.md) par défaut telle que définie dans la configuration de la stratégie de fusion du profil unifié.

Le nombre de profils est mis à jour une fois toutes les 24 heures.

Pour plus d’informations sur les profils, consultez [Une vue unifiée de votre client dans la plateforme CDP en temps réel](profile/profile-overview.md).

### Segments

La section **[!UICONTROL Segments]** indique le nombre total de segments créés pour l’organisation. Ce nombre est mis à jour lors de la création de segments.

Pour plus d’informations sur les segments, consultez [Présentation du service de segmentation](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segmentation.md).

### Destinations

La section **[!UICONTROL Destinations]** indique le nombre total de destinations créées pour l’organisation. Ce nombre est mis à jour lors de la création de destinations.

Pour plus d’informations sur les destinations, consultez [Présentation des destinations](destinations/destinations-overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Click **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Click **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Click **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Jeux de données récents

La carte **[!UICONTROL Jeux de données récents]** montre les cinq jeux de données créés le plus récemment dans l’entreprise. Cette liste est mise à jour lors de la création d’un jeu de données.

Cliquez sur un jeu de données pour afficher les détails de cet élément ou sur **[!UICONTROL Afficher tout]** pour afficher la liste des jeux de données. Vous pouvez ensuite cliquer sur une source spécifique pour afficher plus de détails.

Pour plus d’informations sur les jeux de données, consultez [Ingestion de données dans Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md).

### Sources récentes

La carte de mesure **[!UICONTROL Sources récentes]** montre les cinq sources créées le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’une source.

Cliquez sur une source pour afficher les détails de cet élément ou sur **[!UICONTROL Afficher tout]** pour afficher la liste des sources. Vous pouvez ensuite cliquer sur une source spécifique pour afficher plus de détails.

Pour plus d’informations sur les sources, consultez [Présentation des sources](sources/sources-overview.md).

### Segments récents

La carte de mesure **[!UICONTROL Segments récents]** montre les cinq segments créés le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’un segment.

Cliquez sur un segment pour afficher les détails de cet élément ou sur **[!UICONTROL Afficher tout]** pour afficher les informations sur plus de segments.

Pour plus d’informations sur les segments, consultez [Présentation du service de segmentation](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segmentation.md).

### Destinations récentes

La carte de mesure **[!UICONTROL Destinations récentes]** montre les cinq destinations créées le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’une destination.

Cliquez sur une destination pour afficher les détails de cet élément ou sur **[!UICONTROL Afficher tout]** pour afficher les informations sur plus de destinations.

Pour plus d’informations sur les destinations, consultez [Présentation des destinations](destinations/destinations-overview.md).
