---
keywords: présentation des mesures ; Présentation des mesures rtcdp
title: Page d’accueil et tableaux de bord Real-time Customer Data Platform
description: Tableaux de bord, page d’accueil et première expérience client d’Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 8ea657e379248616d3140bc0a7b0c25a918bc857
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 17%

---

# [!DNL Real-Time Customer Data Platform] page d&#39;accueil

La page d’accueil d’Adobe Real-time Customer Data Platform (Real-Time CDP) est la première page qui s’affiche une fois connecté à Real-Time CDP.

La page d’accueil de Real-Time CDP comprend un widget de prise en main qui vous permet d’accéder rapidement à plusieurs fonctionnalités différentes et une section de mesures qui affiche des informations à jour sur les données de votre entreprise.

Ce document présente la page d’accueil de Real-Time CDP et le tableau de bord des mesures.

![Page d’accueil de l’interface utilisateur de Platform.](assets/platform-home/home.png)

## Widget de prise en main

Le [!UICONTROL Prise en main de Real-time Customer Profile] Le widget est divisé en quatre sections :

* **Ingestion de données dans Platform**: Ce widget vous dirige vers le catalogue de sources. Utilisez le catalogue de sources pour sélectionner une source et ingérer vos données vers Experience Platform. Pour plus d’informations, reportez-vous à la section [présentation des sources](../sources/home.md)
* **Structures de données de modèle**: Ce widget vous dirige vers la présentation des schémas. Utilisez la présentation des schémas pour rechercher des schémas existants ou créer des blocs de création qui décrivent la structure de vos données. Pour plus d’informations, reportez-vous à la section [présentation des schémas](../xdm/home.md).
* **Segmenter les audiences**: Ce widget vous dirige vers le [!DNL Segment Builder] dans l’interface utilisateur. Utilisez la variable [!DNL Segment Builder] pour interagir avec les éléments de données Profile et définir des règles pour vos segments. Pour plus d’informations, reportez-vous à la section [Présentation de Segmentation Service](../segmentation/home.md).
* **Envoi de données vers des destinations**: Ce widget vous dirige vers le catalogue des destinations. Utilisez le catalogue des destinations pour sélectionner une destination à laquelle vous pouvez vous connecter et envoyer des segments. Pour plus d’informations, reportez-vous à la section [présentation des destinations](../destinations/home.md)

![Page d’accueil de l’interface utilisateur de Platform affichant le widget de prise en main](assets/platform-home/getting-started-widget.png)

## Tableau de bord des mesures

Le tableau de bord des mesures affiche des informations à jour sur les données de votre Experience Platform. Le tableau de bord est divisé en deux sections :

### Tableau de classement

Le tableau de classement indique le nombre total actuel de schémas, de jeux de données, de profils et de segments dans votre organisation, ainsi que leur date de mise à jour la plus récente.

![La section du tableau de classement de la page d’accueil de l’interface utilisateur de Platform.](assets/platform-home/leaderboard.png)

* **Schémas totaux**: Le **Total des schémas** compteur affiche le nombre de schémas dans le système. Ce compteur est mis à jour lors de la création d’un schéma. Pour plus d’informations, reportez-vous à la section [présentation des schémas](../xdm/home.md).
* **Nombre total de jeux de données**: Le **Jeux de données totaux** Le compteur affiche le nombre de jeux de données dans le système et la quantité de données dans [!DNL Platform]. Ce compteur est mis à jour lors de la création d’un jeu de données. Pour plus d’informations sur les jeux de données, consultez la [présentation des jeux de données](../catalog/datasets/overview.md).
* **Profils totaux**: Le **Profils** count affiche le nombre total de personnes avec des profils dans la variable [!DNL Real-Time Customer Profile]. Il n’inclut pas les fragments de profil. Il s’agit de votre audience adressable totale. Ce compte utilise la [politique de fusion](profile/merge-policies.md) par défaut telle que définie dans la configuration de la politique de fusion du profil unifié. Le nombre de profils est mis à jour une fois toutes les 24 heures. Pour plus d’informations sur les profils, consultez la [Présentation de Real-Time Customer Profile](../profile/home.md).
* **Segments totaux**: **Segments** affiche le nombre total de segments créés pour l’organisation. Ce nombre est mis à jour lors de la création de segments. Pour plus d’informations sur les segments, consultez la [Présentation de Segmentation Service](../segmentation/home.md).

### Éléments récents

La section Éléments récents répertorie les modifications les plus récentes apportées à votre organisation. Dans l’exemple ci-dessous, les modifications les plus récentes concernent les jeux de données, les sources, les segments et les destinations.

![Section des éléments récents de la page d’accueil de l’interface utilisateur de Platform.](assets/platform-home/recent-items.png)

* **Jeux de données récents**: Le **[!UICONTROL Jeux de données récents]** affiche les cinq jeux de données créés le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’un jeu de données. Sélectionnez un jeu de données pour afficher les détails de cet élément ou sélectionnez **[!UICONTROL Afficher tout]** pour une liste de jeux de données. À partir de là, vous pouvez sélectionner une source spécifique pour plus de détails. Pour plus d’informations sur les jeux de données, consultez la [présentation des jeux de données](../catalog/datasets/overview.md).
* **Sources récentes**: Le **[!UICONTROL Sources récentes]** la carte de mesure affiche les cinq sources créées le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’une source. Sélectionnez une source pour afficher les détails de cet élément ou sélectionnez **[!UICONTROL Afficher tout]** pour une liste de sources. À partir de là, vous pouvez sélectionner une source spécifique pour plus de détails. Pour plus d’informations sur les sources, consultez [Présentation des sources](../sources/home.md).
* **Segments récents**: Le **[!UICONTROL Segments récents]** la carte de mesure affiche les cinq segments créés le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’un segment. Sélectionnez un segment pour afficher les détails de cet élément ou sélectionnez **[!UICONTROL Afficher tout]** pour une liste de segments. Pour plus d’informations sur les segments, consultez [Présentation de Segmentation Service](../segmentation/home.md).
* **Destinations récentes**: Le **[!UICONTROL Destinations récentes]** la carte de mesure affiche les cinq destinations créées le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’une destination. Sélectionnez une destination pour afficher les détails de cet élément ou sélectionnez **[!UICONTROL Afficher tout]** pour une liste de destinations. Pour plus d’informations, reportez-vous à la section [présentation des destinations](../destinations/home.md).

## Ressources

Enfin, le widget Ressources fournit des ressources de documentation supplémentaires auxquelles vous pouvez vous référer. Ces cas comprennent notamment :

![La section Ressources de la page d’accueil de l’interface utilisateur de Platform.](assets/platform-home/resources.png)

* [Compréhension des schémas](../xdm/schema/composition.md)
* [Connexion à des sources](../sources/home.md)
* [Comment renseigner votre profil client en temps réel](../profile/home.md)
* [Connexion des destinations](../destinations/home.md)
* [Gérer l’accès](../access-control/abac/overview.md)

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
