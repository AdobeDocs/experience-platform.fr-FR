---
keywords: Experience Platform;home;popular topics;Adobe Experience Platform;user guide;ui guide;platform ui guide;introduction to platform;dashboard;
solution: Experience Platform
title: Guide de l’interface utilisateur Adobe Experience Platform
topic: ui guide
description: 'Adobe Experience Platform '
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 0%

---


# Guide de l’interface utilisateur Adobe Experience Platform

Ce guide présente l’utilisation de l’interface utilisateur de Adobe Experience Platform, explique les différents composants utilisés et fournit des liens vers d’autres documents pour plus d’informations.

Pour en savoir plus sur Adobe Experience Platform, veuillez lire la présentation [](./home.md)Experience Platform.

## Ecran d’accueil

Après vous être connecté à Adobe Experience Platform, vous accédez à la page d’ [!UICONTROL accueil] , qui comprend le tableau de bord des mesures, les données récentes et les sections d’apprentissage recommandées.

![](images/user-guide/homepage.png)

### Tableau de bord de mesures

Le tableau de bord de mesures fournit des cartes qui vous donnent des informations sur les jeux de données, les profils, les segments et les destinations au sein de votre organisation.

![](images/user-guide/homepage-dashboard.png)

La section **[!UICONTROL Jeux de données]** indique le nombre de jeux de données au sein de votre organisation IMS. Ce numéro est mis à jour lorsqu&#39;un nouveau jeu de données est créé. Vous trouverez plus d&#39;informations sur les jeux de données dans l&#39;aperçu [des](../catalog/datasets/overview.md)jeux de données.

La section **[!UICONTROL Profils]** indique le nombre total de personnes ayant des profils au sein de votre organisation IMS, à l’exclusion des fragments de profil. Ce nombre total de personnes représente l’audience adressable totale et est mis à jour une fois toutes les 24 heures. Pour plus d’informations sur les profils, consultez la présentation [du Profil client en temps](../profile/home.md)réel.

La section **[!UICONTROL Segments]** affiche le nombre total de segments créés dans votre organisation IMS. Ce numéro est mis à jour lorsqu’un nouveau segment est créé. Vous trouverez plus d’informations sur les segments dans la présentation [du service](../segmentation/home.md)de segmentation.

The **[!UICONTROL Destinations]** section shows the total number of destinations created for the IMS Organization. Ce numéro est mis à jour lorsqu’une nouvelle destination est créée. Vous trouverez plus d’informations sur les destinations dans l’aperçu [des](../destinations/home.md)destinations.

### Données récentes

Le tableau de bord de données récent fournit des informations sur les jeux de données, les sources, les segments et les destinations récemment créés.

![](images/user-guide/homepage-recent.png)

La section Jeu de données **** récents liste les cinq derniers jeux de données créés au sein de votre organisation IMS. Cette liste est mise à jour chaque fois qu&#39;un nouveau jeu de données est créé. Vous pouvez sélectionner un jeu de données de la liste à la vue pour plus d&#39;informations sur le jeu de données spécifié ou sélectionner **[!UICONTROL Vue all]** pour afficher une liste de tous les jeux de données créés. Vous trouverez plus d&#39;informations sur les jeux de données dans l&#39;aperçu [des](../catalog/datasets/overview.md)jeux de données.

La section Sources **** récentes liste les cinq connecteurs source les plus récents au sein de votre organisation IMS. Cette liste est mise à jour chaque fois qu&#39;un nouveau connecteur source est créé. Vous pouvez sélectionner une connexion source de la liste à la vue plus d&#39;informations sur le connecteur spécifié ou sélectionner **[!UICONTROL Vue toutes]** pour afficher une liste de toutes les connexions source créées. Vous trouverez plus d&#39;informations sur les sources dans l&#39;aperçu [des](../sources/home.md)sources.

La section Segments **** récents liste les cinq définitions de segment créées le plus récemment au sein de votre organisation IMS. Cette liste est mise à jour chaque fois qu’une nouvelle définition de segment est créée. Vous pouvez sélectionner une définition de segment de la liste à la vue plus d&#39;informations sur la définition de segment spécifiée ou sélectionner **[!UICONTROL Vue all]** pour afficher une liste de toutes les définitions de segment créées. Vous trouverez plus d’informations sur les segments dans la présentation [du service](../segmentation/home.md)de segmentation.

La section Destinations **** récentes liste les cinq destinations les plus récemment créées au sein de votre organisation IMS. Cette liste est mise à jour chaque fois qu’une nouvelle destination est créée. Vous pouvez sélectionner une destination de la liste à la vue plus d&#39;informations sur la destination spécifiée ou sélectionner **[!UICONTROL Vue toutes]** pour afficher une liste de toutes les destinations créées. Vous trouverez plus d’informations sur les destinations dans l’aperçu [des](../destinations/home.md)destinations.

### Apprentissage recommandé

La section **[!UICONTROL Apprentissage]** recommandé contient des liens vers une documentation utile pour commencer à utiliser Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barre de navigation supérieure

La barre de navigation supérieure de l’interface utilisateur de la plate-forme affiche l’organisation IMS dans laquelle vous êtes actuellement connecté et fournit plusieurs contrôles importants.

Sur le côté gauche de la barre de navigation se trouve le logo Adobe Experience Platform. Si vous sélectionnez cette option, vous revenez à l’écran d’accueil de l’interface utilisateur de la plate-forme.

![](./images/user-guide/homepage-top-nav-bar.png)

### Commutateur d&#39;organisation IMS

Le premier élément sur le côté droit de la barre de navigation est le commutateur **Organisation** IMS.

![](./images/user-guide/homepage-ims-org.png)

Si vous sélectionnez le sélecteur, un menu déroulant des organisations IMS auxquelles vous avez accès s&#39;affiche, le cas échéant. Sélectionnez une option répertoriée pour passer à cette organisation IMS.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Changement d’application

L&#39;élément suivant sur la droite est le sélecteur **d&#39;** applications, représenté par l&#39;icône du sélecteur ![d&#39;](./images/user-guide/app-switcher-icon.png) applications. Lorsque vous sélectionnez cette icône, vous pouvez basculer entre Experience Platform, Ressources, Exchange et Lancement.

### Aide

À droite du sélecteur d’applications se trouve le menu **d’** aide et d’assistance, qui est représenté par l’icône ![point d’interrogation/aide](./images/user-guide/help-icon.png) . Lorsque vous sélectionnez cette icône, un menu contextuel s’affiche, contenant plusieurs ressources d’aide et d’assistance. L’onglet **[!UICONTROL Aide]** affiche une liste de la documentation pertinente pour la page sur laquelle vous vous trouvez actuellement. L&#39;onglet **[!UICONTROL Assistance]** vous permet de créer un ticket d&#39;assistance auprès de l&#39;équipe d&#39;assistance Adobe. L’onglet **[!UICONTROL Commentaires]** vous permet d’envoyer des commentaires sur la plateforme à l’Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notifications et annonces

Après le menu d&#39;aide et d&#39;assistance se trouve la section **** Notifications, qui est représentée par l&#39;icône ![bell/Notifications et Annonces](images/user-guide/notification-icon.png) . L’onglet **[!UICONTROL Notifications]** affiche des informations importantes sur le produit et d’autres mises à jour pertinentes, tandis que l’onglet **[!UICONTROL Annonces]** affiche des notifications sur la maintenance du service.

### Profil utilisateur

Le dernier élément de la barre de navigation supérieure est les paramètres **** utilisateur, qui sont représentés par l’icône Paramètres ![utilisateur/Profil](images/user-guide/profile-icon.png) utilisateur. Sélectionnez cette icône pour modifier vos préférences ou vous déconnecter.

### Environnements de test

Immédiatement sous la barre de navigation supérieure se trouve la barre de sandbox. Cette barre indique le sandbox que vous utilisez actuellement pour Platform. Vous trouverez plus d&#39;informations sur les sandbox dans l&#39;aperçu [des](../sandboxes/home.md)sandbox.

## Navigation de gauche {#left-nav}

La navigation sur le côté gauche de l’écran liste tous les différents services pris en charge dans l’interface utilisateur de la plate-forme.

>[!IMPORTANT]
>
>Il se peut que certaines sections de la barre de navigation de gauche n’apparaissent pas ou ne soient pas grisées. Ceci est dû au fait que vous n’avez pas accès à ces fonctionnalités. Si vous pensez avoir accès à ces sections, contactez votre administrateur système.

![](images/user-guide/homepage-left.png)

La section **[!UICONTROL Accueil]** vous permet de revenir à la page d’accueil de l’interface utilisateur de la plate-forme.

La section **[!UICONTROL Workflows]** présente une liste de workflows à plusieurs étapes pour effectuer des opérations dans la Plateforme. Pour plus d&#39;informations sur les workflows, consultez la présentation [des](./workflows.md)workflows.

### [!UICONTROL Connexions]

La section **[!UICONTROL Sources]** vous permet de créer, de mettre à jour et de supprimer des connexions source, ce qui vous permet d&#39;assimiler des données provenant de sources externes dans la plate-forme. Vous trouverez plus d&#39;informations sur les sources dans l&#39;aperçu [des](../sources/home.md)sources.

La section **[!UICONTROL Destinations]** vous permet de créer, de mettre à jour et de supprimer des destinations, ce qui vous permet d’exporter des données de la plate-forme vers de nombreuses destinations externes. Vous trouverez plus d’informations sur les destinations dans l’aperçu [des](../destinations/home.md)destinations.

### [!UICONTROL Informations     ]

La section **[!UICONTROL Profils]** vous permet de parcourir les profils client, les mesures de profil de vue, de créer et de gérer des stratégies de fusion et les schémas d’union de vue. Pour en savoir plus sur l&#39;utilisation de la section [!UICONTROL Profils] , veuillez lire le guide [[!DNL Profile] ](../profile/ui/user-guide.md)d&#39;utilisation. Pour plus d’informations sur le Profil client en temps réel, consultez la présentation [du Profil client en temps](../profile/home.md)réel.

La section **[!UICONTROL Segments]** vous permet de créer et de gérer des définitions de segment. Pour en savoir plus sur l’utilisation de la section [!UICONTROL Segments] , consultez le guide [d’utilisation de la](../segmentation/ui/overview.md)segmentation. Pour plus d’informations sur le service de segmentation, consultez la présentation [du service de](../segmentation/home.md)segmentation.

La section **[!UICONTROL Identités]** vous permet de créer et de gérer des espaces de nommage d&#39;identité. Pour plus d&#39;informations sur la section [!UICONTROL Identités] , y compris des informations sur les espaces de nommage d&#39;identité et comment utiliser les identités dans l&#39;interface utilisateur de la plateforme, reportez-vous à la présentation [de l&#39;espace de nommage d&#39;](../identity-service/namespaces.md)identité.

### [!UICONTROL Confidentialité]

La section **[!UICONTROL Stratégies]** vous permet de créer et de gérer des stratégies d’utilisation des données. Pour en savoir plus sur l’utilisation de la section Stratégies, consultez le guide [d’utilisation des stratégies](../data-governance/policies/user-guide.md)d’utilisation des données. Vous trouverez plus d’informations sur les stratégies d’utilisation des données dans l’aperçu [des stratégies](../data-governance/policies/overview.md)d’utilisation des données.

La section **[!UICONTROL Demandes]** vous permet de créer et de gérer des demandes de confidentialité. Veuillez noter que vous devez être placé sur la liste autorisée pour avoir accès à l&#39;interface utilisateur du Privacy Service. Pour en savoir plus sur l&#39;utilisation de la section Demandes, veuillez lire le guide [d&#39;utilisation du](../privacy-service/ui/user-guide.md)Privacy Service. Vous trouverez plus d’informations sur le Privacy Service dans la présentation [du](../privacy-service/home.md)Privacy Service.

### [!UICONTROL Science des données]

La section **[!UICONTROL Ordinateurs portables]** donne accès à JupyterLab, un environnement de développement interactif qui vous permet d&#39;explorer, d&#39;analyser et de modéliser vos données. Pour en savoir plus sur l&#39;utilisation de la section Ordinateurs portables, veuillez lire le guide [d&#39;utilisation de](../data-science-workspace/jupyterlab/overview.md)JupyterLab. Pour plus d’informations sur l’Espace de travail Data Science, consultez la présentation de l’Espace de travail [Data Science.](../data-science-workspace/home.md)

La section **[!UICONTROL Modèles]** vous permet d&#39;exploiter l&#39;apprentissage automatique et l&#39;intelligence artificielle pour créer, développer, former et ajuster des modèles afin de faire des prédictions. Vous trouverez plus d&#39;informations sur la section Modèles dans le didacticiel sur la [formation et l&#39;évaluation d&#39;un modèle](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

La section **[!UICONTROL Services]** vous permet de gérer vos modèles publiés pour une formation et un score planifiés, ou de tirer parti des services intelligents d’Adobe, un ensemble de services d’IA qui offrent des expériences client personnalisées en temps réel. Pour plus d’informations sur la section Services, consultez le didacticiel [](../data-science-workspace/models-recipes/publish-model-service-ui.md)Publication d’un modèle en tant que service.

### [!UICONTROL Gestion des données]

La section **[!UICONTROL Schémas]** vous permet de créer et de gérer des schémas. Pour en savoir plus sur l&#39;utilisation de la section Schémas, veuillez lire le tutoriel sur la [création d&#39;un schéma](../xdm/tutorials/create-schema-ui.md). Vous trouverez plus d’informations sur le modèle de données d’expérience (XDM) dans l’aperçu [de](../xdm/home.md)XDM.

La section **[!UICONTROL Jeu de données]** vous permet de créer et de gérer des jeux de données. Pour plus d&#39;informations sur la section Jeux de données, consultez le guide [d&#39;utilisation](../catalog/datasets/user-guide.md)des jeux de données.

La section **[!UICONTROL Requêtes]** vous permet de créer et de gérer des requêtes, de consigner les requêtes SQL effectuées par Requête Service et de vue de vos informations d&#39;identification PostgreSQL. Pour plus d&#39;informations sur la section Requêtes, consultez le guide [d&#39;utilisation de](../query-service/ui/overview.md)Requête Service.

La section **[!UICONTROL Surveillance]** vous permet de surveiller l’assimilation par lots et en flux continu. Pour plus d&#39;informations sur la section Surveillance, consultez le guide [d&#39;utilisateur d&#39;assimilation des données de](../ingestion/quality/monitor-data-flows.md)surveillance.

## Étapes suivantes

En lisant ce guide, vous avez maintenant été initié à la page d&#39;accueil et aux principaux éléments de navigation de l&#39;interface utilisateur de la plate-forme. Pour plus d&#39;informations sur le fonctionnement de l&#39;interface utilisateur, reportez-vous à la documentation de chaque service de plateforme. Les liens vers cette documentation sont fournis dans la section de navigation [de](#left-nav) gauche qui se trouve plus haut dans ce document.