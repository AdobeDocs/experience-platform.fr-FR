---
keywords: présentation des mesures ; présentation des mesures rtcdp
title: Page d’accueil et tableaux de bord Real-time Customer Data Platform
description: Tableaux de bord, page d’accueil et première expérience client d’Adobe Experience Platform
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: d052f307d91890f89d6cb3f18525fe395c116f95
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 10%

---

# [!DNL Real-Time Customer Data Platform] page d&#39;accueil

La page d’accueil d’Adobe Real-time Customer Data Platform (Real-Time CDP) est la première page qui s’affiche une fois connecté à Real-Time CDP.

La page d’accueil de Real-Time CDP comprend un widget de prise en main qui vous permet d’accéder rapidement à plusieurs fonctionnalités différentes et une section de mesures qui affiche des informations à jour sur les données de votre entreprise.

Ce document présente la page d’accueil de Real-Time CDP et le tableau de bord des mesures.

![Page d’accueil de l’interface utilisateur de Platform.](assets/platform-home/home.png)

## Widget de prise en main

La variable [!UICONTROL Prise en main de Real-time Customer Profile] Le widget est divisé en quatre sections :

* **Ingestion de données dans Platform**: ce widget vous dirige vers le catalogue de sources. Utilisez le catalogue de sources pour sélectionner une source et ingérer vos données vers Experience Platform. Sélectionner **[Configuration des sources]** pour accéder au catalogue des sources. Pour plus d’informations, consultez la section [présentation des sources](../sources/home.md).
* **Structures de données de modèle**: ce widget vous dirige vers la présentation des schémas. Utilisez la présentation des schémas pour rechercher des schémas existants ou créez un plan directeur qui décrit la structure de vos données. Sélectionner **[!UICONTROL Créer un schéma]** pour accéder à l’interface de création de schéma. Pour plus d’informations, consultez la section [présentation des schémas](../xdm/home.md).
* **Création d’audiences**: ce widget vous dirige vers le créateur de segments dans l’interface utilisateur. Utilisez le créateur de segments pour interagir avec les éléments de données de profil et définir les critères de votre définition de segment. Sélectionner **[!UICONTROL Créer une audience]** pour accéder au créateur de segments. Pour plus d’informations, consultez la section [Présentation de Segmentation Service](../segmentation/home.md).
* **Envoi de données vers des destinations**: ce widget vous dirige vers le catalogue des destinations. Utilisez le catalogue des destinations pour sélectionner une destination à laquelle vous pouvez vous connecter et envoyer des segments. Sélectionner **[!UICONTROL Configuration des destinations]** pour accéder au catalogue des destinations. Pour plus d’informations, consultez la section [présentation des destinations](../destinations/home.md).

![Page d’accueil de l’interface utilisateur de Platform affichant le widget de prise en main](assets/platform-home/getting-started-widget.png)

## Tableau de bord des mesures {#metrics-dashboard}

>[!CONTEXTUALHELP]
>id="platform_home_metrics_totalProfiles"
>title="Nombre total de profils"
>abstract="Nombre total de profils de votre organisation dans Experience Platform. Ce nombre est basé sur la politique de fusion de votre organisation et n’inclut pas les fragments de profil. Le nombre de profils est mis à jour une fois toutes les 24 heures."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=fr#profile-count" text="En savoir plus dans la documentation."

Le tableau de bord des mesures affiche des informations à jour sur les données de votre Experience Platform. Le tableau de bord est divisé en deux sections :

### Tableau de classement

Le tableau de classement indique le nombre total actuel de schémas, de jeux de données, de profils et de segments dans votre organisation, ainsi que leur date de mise à jour la plus récente.

![La section du tableau de classement de la page d’accueil de l’interface utilisateur de Platform.](assets/platform-home/leaderboard.png)

* **Schémas totaux**: la variable **Schémas totaux** compteur affiche le nombre de schémas dans le système. Ce compteur est mis à jour lors de la création d’un schéma. Pour plus d’informations, consultez la section [présentation des schémas](../xdm/home.md).
* **Nombre total de jeux de données**: la variable **Nombre total de jeux de données** Le compteur indique le nombre de jeux de données dans le système et la quantité de données dans Experience Platform. Ce compteur est mis à jour lors de la création d’un jeu de données. Pour plus d’informations sur les jeux de données, consultez la section [présentation des jeux de données](../catalog/datasets/overview.md).
* **Profils totaux**: la variable **Profils** count indique le nombre total de profils de votre organisation dans Experience Platform. Il n’inclut pas les fragments de profil. Il s’agit de votre audience adressable totale. Ce comptage utilise la valeur par défaut [stratégie de fusion](profile/merge-policies.md) comme défini dans la configuration de la stratégie de fusion de Real-Time Customer Profile. Le nombre de profils est mis à jour une fois toutes les 24 heures. Sélectionner **[!UICONTROL Profils]** pour accéder à la page d’aperçu des profils et afficher toutes vos mesures de profil. Pour plus d’informations sur les profils, consultez la [Présentation de Real-Time Customer Profile](../profile/home.md).
* **Audiences totales**: la variable **Audiences totales** Le compteur indique le nombre total d’audiences créées pour votre organisation. Ce nombre est mis à jour lors de la création de nouvelles audiences. Pour plus d’informations sur les audiences, consultez la [Présentation de Segmentation Service](../segmentation/home.md).

### Éléments récents

La section Éléments récents répertorie les modifications les plus récentes apportées à votre organisation. Dans l’exemple ci-dessous, les modifications les plus récentes concernent les jeux de données, les sources, les segments et les destinations.

![Section des éléments récents de la page d’accueil de l’interface utilisateur de Platform.](assets/platform-home/recent-items.png)

* **Jeux de données récents**: la variable **[!UICONTROL Jeux de données récents]** affiche les cinq jeux de données créés le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’un jeu de données. Sélectionnez un jeu de données pour afficher les détails de cet élément ou sélectionnez **[!UICONTROL Afficher tout]** pour une liste de jeux de données. À partir de là, vous pouvez sélectionner une source spécifique pour plus de détails. Pour plus d’informations sur les jeux de données, consultez la [présentation des jeux de données](../catalog/datasets/overview.md).
* **Sources récentes**: la variable **[!UICONTROL Sources récentes]** la carte de mesure affiche les cinq sources créées le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’une source. Sélectionnez une source pour afficher les détails de cet élément ou sélectionnez **[!UICONTROL Afficher tout]** pour une liste de sources. À partir de là, vous pouvez sélectionner une source spécifique pour plus de détails. Pour plus d’informations sur les sources, consultez [Présentation des sources](../sources/home.md).
* **Segments récents**: la variable **[!UICONTROL Segments récents]** la carte de mesure affiche les cinq segments créés le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’un segment. Sélectionnez un segment pour afficher les détails de cet élément ou sélectionnez **[!UICONTROL Afficher tout]** pour une liste de segments. Pour plus d’informations sur les segments, consultez [Présentation de Segmentation Service](../segmentation/home.md).
* **Destinations récentes**: la variable **[!UICONTROL Destinations récentes]** la carte de mesure affiche les cinq destinations créées le plus récemment dans l’organisation. Cette liste est mise à jour lors de la création d’une destination. Sélectionnez une destination pour afficher les détails de cet élément ou sélectionnez **[!UICONTROL Afficher tout]** pour une liste de destinations. Pour plus d’informations, consultez la section [présentation des destinations](../destinations/home.md).

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
