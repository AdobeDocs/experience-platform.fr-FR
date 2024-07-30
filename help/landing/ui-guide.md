---
keywords: Experience Platform;accueil;rubriques les plus consultées;Adobe Experience Platform;guide de l’utilisateur;guide de l’interface utilisateur de la plateforme;présentation de la plateforme;tableau de bord;
solution: Experience Platform
title: Présentation de l’interface utilisateur de l’Experience Platform
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: 9844a7bf5e7198e7d5112ec924220aba71cdc14b
workflow-type: tm+mt
source-wordcount: '1947'
ht-degree: 3%

---

# Guide de l’interface utilisateur de Adobe Experience Platform

Ce guide présente l’utilisation de l’interface utilisateur de Adobe Experience Platform, explique à quoi servent les différents composants et fournit des liens vers d’autres documents pour plus d’informations.

Pour en savoir plus sur Adobe Experience Platform, commencez par lire la [Présentation dʼExperience Platform](home.md).

## Écran d’accueil

Après vous être connecté à Adobe Experience Platform, vous vous trouvez sur la page [!UICONTROL Accueil], qui comprend les sections [ tableau de bord des mesures](#metrics), [données récentes](#recent-data) et [apprentissage recommandé](#recommended-learning) .

![](images/user-guide/homepage.png)

### Mesures

Le tableau de bord des mesures fournit des cartes qui vous donnent des informations sur les jeux de données, les profils, les segments et les destinations de votre entreprise.

![](images/user-guide/homepage-dashboard.png)

La section **[!UICONTROL Jeux de données]** indique le nombre de jeux de données au sein de votre organisation. Ce nombre est mis à jour lors de la création d’un jeu de données. Vous trouverez plus d’informations sur les jeux de données dans la [présentation des jeux de données](../catalog/datasets/overview.md).

La section **[!UICONTROL Profils]** indique le nombre total de personnes avec des profils au sein de votre organisation, à l’exception des fragments de profil. Ce nombre total de personnes représente l’audience adressable totale et est mis à jour toutes les 24 heures. Vous trouverez plus d’informations sur les profils dans la [présentation de Real-Time Customer Profile](../profile/home.md).

La section **[!UICONTROL Segments]** indique le nombre total de segments créés dans votre organisation. Ce nombre est mis à jour lors de la création d’un segment. Vous trouverez plus d’informations sur les segments dans la [présentation de Segmentation Service](../segmentation/home.md).

La section **[!UICONTROL Destinations]** indique le nombre total de destinations créées pour l’organisation. Ce nombre est mis à jour lors de la création d’une destination. Vous trouverez plus d’informations sur les destinations dans la [présentation des destinations](../destinations/home.md).

### Données récentes

Le tableau de bord de données récent fournit des informations sur les jeux de données, les sources, les segments et les destinations récemment créés.

![](images/user-guide/homepage-recent.png)

La section **[!UICONTROL Jeux de données récents]** répertorie les cinq jeux de données créés le plus récemment au sein de votre organisation. Cette liste est mise à jour chaque fois qu’un nouveau jeu de données est créé. Vous pouvez sélectionner un jeu de données dans la liste pour l’afficher. Vous trouverez plus d’informations sur le jeu de données spécifié ou sélectionner **[!UICONTROL Afficher tout]** pour afficher la liste de tous les jeux de données créés. Vous trouverez plus d’informations sur les jeux de données dans la [présentation des jeux de données](../catalog/datasets/overview.md).

La section **[!UICONTROL Sources récentes]** répertorie les cinq connecteurs source créés le plus récemment au sein de votre organisation. Cette liste est mise à jour chaque fois qu’un nouveau connecteur source est créé. Vous pouvez sélectionner une connexion source dans la liste pour afficher. Vous trouverez plus d’informations sur le connecteur spécifié ou sélectionner **[!UICONTROL Afficher tout]** pour afficher la liste de toutes les connexions source créées. Vous trouverez plus d’informations sur les sources dans la [présentation des sources](../sources/home.md).

La section **[!UICONTROL Segments récents]** répertorie les cinq définitions de segment créées le plus récemment au sein de votre organisation. Cette liste est mise à jour chaque fois qu’une nouvelle définition de segment est créée. Vous pouvez sélectionner une définition de segment dans la liste pour afficher. Vous trouverez plus d’informations sur la définition de segment spécifiée ou sélectionner **[!UICONTROL Afficher tout]** pour afficher la liste de toutes les définitions de segment créées. Vous trouverez plus d’informations sur les segments dans la [présentation de Segmentation Service](../segmentation/home.md).

La section **[!UICONTROL Destinations récentes]** répertorie les cinq destinations créées le plus récemment au sein de votre organisation. Cette liste est mise à jour chaque fois qu’une nouvelle destination est créée. Vous pouvez sélectionner une destination dans la liste pour afficher plus d’informations sur la destination spécifiée ou sélectionner **[!UICONTROL Afficher tout]** pour afficher une liste de toutes les destinations créées. Vous trouverez plus d’informations sur les destinations dans la [présentation des destinations](../destinations/home.md).

### Apprentissage recommandé

La section **[!UICONTROL apprentissage recommandé]** fournit des liens vers la documentation utile pour commencer à utiliser Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barre de navigation supérieure

La barre de navigation supérieure de l’interface utilisateur de Platform affiche l’organisation dans laquelle vous êtes actuellement connecté et fournit plusieurs contrôles importants.

Le logo Adobe Experience Platform se trouve sur le côté gauche de la barre de navigation. La sélection de ce logo à tout moment vous ramène à l’écran d’accueil de l’interface utilisateur de Platform.

![](./images/user-guide/homepage-top-nav-bar.png)

### Sélecteur d’organisation

Le premier élément sur le côté droit de la barre de navigation supérieure est le **sélecteur d’organisation**.

![](./images/user-guide/homepage-ims-org-switcher.png)

Si vous sélectionnez le sélecteur, un menu déroulant des organisations auxquelles vous avez accès s’affiche, le cas échéant. Pour passer à une autre organisation, sélectionnez une option répertoriée.

### Changement d’applications

L’élément suivant sur le côté droit de la navigation supérieure est le **sélecteur d’applications**, représenté par l’icône ![ du sélecteur d’applications](/help/images/icons/apps.png). Lorsque vous sélectionnez cette icône, vous pouvez basculer entre les applications d’Adobe auxquelles votre entreprise a accès (Experience Platform, Analytics, Assets, etc.).

### Aide

À droite du sélecteur d’applications se trouve le **menu d’aide et de support**, qui est représenté par l’icône ![ point d’interrogation/aide](/help/images/icons/help.png). Lorsque vous sélectionnez cette icône, un menu contextuel s’affiche, contenant plusieurs ressources d’aide et d’assistance. L’onglet **[!UICONTROL Aide]** affiche la liste de la documentation appropriée pour la page sur laquelle vous vous trouvez actuellement. L’onglet **[!UICONTROL Assistance]** vous permet de créer un ticket d’assistance avec l’équipe d’assistance d’Adobe. L’onglet **[!UICONTROL Commentaires]** vous permet d’envoyer des commentaires sur Platform à Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notifications et annonces

Dans la **section des notifications**, qui est représentée par l’icône ![ {cloche/notifications et annonces](/help/images/icons/bell.png) . L’onglet **[!UICONTROL Notifications]** affiche des informations importantes sur le produit et d’autres mises à jour pertinentes, tandis que l’onglet **[!UICONTROL Annonces]** affiche des informations sur la maintenance du service.

### Profil utilisateur

Le dernier élément de la barre de navigation supérieure est le **paramètre utilisateur**, représenté par l’icône ![ user settings/User Profile](images/user-guide/profile-icon.png) . Sélectionnez cette icône pour modifier vos préférences ou déconnectez-vous.

Vous pouvez basculer entre le thème clair et sombre de l’interface de Platform avec le commutateur situé juste en dessous de votre nom et de votre email. Sélectionnez le thème que vous préférez.

![](images/theme.png)

### Sandbox

Immédiatement sous la barre de navigation supérieure se trouve la barre d’environnement de test. Cette barre indique l’environnement de test que vous utilisez actuellement pour Platform. Vous trouverez plus d’informations sur les environnements de test dans la [présentation des environnements de test](../sandboxes/home.md).

## Volet de navigation de gauche {#left-nav}

La navigation dans la partie gauche de l’écran répertorie tous les différents services pris en charge dans l’interface utilisateur de Platform.

Cliquez sur l’icône de menu pour afficher ou masquer le panneau de navigation de gauche.

![](images/user-guide/hidemenu.png)

Vous pouvez verrouiller la navigation à l’ouverture en cliquant de nouveau après avoir affiché le panneau.

>[!IMPORTANT]
>
>La barre de navigation de gauche affiche uniquement les fonctionnalités auxquelles vous avez accès. Dans les versions précédentes de Adobe Experience Platform, les éléments indisponibles étaient désactivés. Si vous pensez que vous devriez avoir accès à une section qui n’apparaît pas, contactez votre administrateur système.

![](images/user-guide/homepage-left.png)

La section **[!UICONTROL Accueil]** vous permet de revenir à la page d’accueil de l’interface utilisateur de Platform.

La section **[!UICONTROL Workflows]** présente une liste de workflows à plusieurs étapes pour effectuer des opérations dans Platform. Vous trouverez plus d’informations sur les workflows dans la [présentation des workflows](./workflows.md).

### [!UICONTROL Connexions]

La section **[!UICONTROL Sources]** vous permet de créer, de mettre à jour et de supprimer des connexions source, ce qui vous permet d’ingérer des données provenant de sources externes dans Platform. Vous trouverez plus d’informations sur les sources dans la [présentation des sources](../sources/home.md).

La section **[!UICONTROL Destinations]** vous permet de créer, de mettre à jour et de supprimer des destinations, ce qui vous permet d’exporter des données de Platform vers de nombreuses destinations externes. Vous trouverez plus d’informations sur les destinations dans la [présentation des destinations](../destinations/home.md).

### [!UICONTROL Client]

La section **[!UICONTROL Profils]** vous permet de parcourir les profils client, d’afficher les mesures de profil, de créer et de gérer des stratégies de fusion et d’afficher les schémas d’union. Pour en savoir plus sur l&#39;utilisation de la section [!UICONTROL Profils], consultez le [[!DNL Profile] guide d&#39;utilisation](../profile/ui/user-guide.md). Vous trouverez plus d’informations sur Real-Time Customer Profile dans la [présentation de Real-Time Customer Profile](../profile/home.md).

La section **[!UICONTROL Audiences]** vous permet de créer et de gérer des définitions de segment. Pour en savoir plus sur l’utilisation de la section [!UICONTROL Audiences], consultez le [guide d’utilisation de la segmentation](../segmentation/ui/overview.md). Vous trouverez plus d’informations sur Segmentation Service dans la [présentation de Segmentation Service](../segmentation/home.md).

La section **[!UICONTROL Identités]** vous permet de créer et de gérer des espaces de noms d’identité. Pour plus d’informations sur la section [!UICONTROL Identités], y compris des informations sur les espaces de noms d’identité et sur l’utilisation des identités dans l’interface utilisateur de Platform, reportez-vous à la [présentation des espaces de noms d’identité](../identity-service/features/namespaces.md).

### [!UICONTROL Confidentialité]

La section **[!UICONTROL Stratégies]** vous permet de créer et de gérer des stratégies d’utilisation des données. Pour en savoir plus sur l’utilisation de la section Stratégies, consultez le [guide d’utilisation des stratégies d’utilisation des données](../data-governance/policies/user-guide.md). Vous trouverez plus d’informations sur les stratégies d’utilisation des données dans la [présentation des stratégies d’utilisation des données](../data-governance/policies/overview.md).

La section **[!UICONTROL Demandes]** vous permet de créer et de gérer des demandes d’accès à des informations personnelles. Veuillez noter que vous devez être placé sur la liste autorisée pour avoir accès à l’interface utilisateur de Privacy Service. Pour en savoir plus sur l’utilisation de la section Demandes, consultez le [guide de l’utilisateur du Privacy Service](../privacy-service/ui/user-guide.md). Vous trouverez plus d’informations sur Privacy Service dans la [présentation du Privacy Service](../privacy-service/home.md).

### [!UICONTROL Science des données]

La section **[!UICONTROL Notebooks]** donne accès à JupyterLab, un environnement de développement interactif qui vous permet d’explorer, d’analyser et de modéliser vos données. Pour en savoir plus sur l’utilisation des notebooks, consultez le [guide d’utilisation de JupyterLab](../data-science-workspace/jupyterlab/overview.md). Vous trouverez plus d’informations sur Data Science Workspace dans la [présentation de Data Science Workspace](../data-science-workspace/home.md)

La section **[!UICONTROL Modèles]** vous permet d’utiliser l’apprentissage automatique et l’intelligence artificielle pour créer, développer, former et ajuster des modèles afin de faire des prédictions. Vous trouverez plus d’informations sur la section Modèles dans le tutoriel sur [la formation et l’évaluation d’un modèle](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

La section **[!UICONTROL Services]** vous permet de gérer vos modèles publiés pour la formation et la notation planifiées, ou d’utiliser les services intelligents d’Adobe, un ensemble de services d’IA qui offrent des expériences client personnalisées en temps réel. Vous trouverez plus d’informations sur la section Services dans le [tutoriel Publication d’un modèle en tant que service](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Gestion des données]

La section **[!UICONTROL Schémas]** vous permet de créer et de gérer des schémas de modèle de données d’expérience (XDM). Pour en savoir plus sur les schémas, consultez le tutoriel sur la [création d’un schéma](../xdm/tutorials/create-schema-ui.md). Vous trouverez plus d’informations sur XDM dans la [présentation du système XDM](../xdm/home.md).

La section **[!UICONTROL Jeux de données]** vous permet de créer et de gérer des jeux de données. Vous trouverez plus d’informations sur les jeux de données dans le [guide d’utilisation des jeux de données](../catalog/datasets/user-guide.md).

La section **[!UICONTROL Requêtes]** vous permet de créer et gérer des requêtes, de consigner des requêtes SQL effectuées par Adobe Experience Platform Query Service et d’afficher vos informations d’identification [!DNL PostgreSQL]. Vous trouverez plus d’informations sur les requêtes dans le [guide d’utilisation de Query Service](../query-service/ui/overview.md).

La section **[!UICONTROL Surveillance]** vous permet de surveiller l’ingestion par lots et par flux. Vous trouverez plus d’informations sur la surveillance dans le [guide d’utilisation de la surveillance de l’ingestion de données](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Données fédérées] (Disponibilité limitée)

La section **[!UICONTROL Modèles]** vous permet de concevoir et de créer des modèles et des schémas de données qui définissent la structure, les relations et les contraintes de vos données. Vous trouverez plus d’informations sur les modèles et schémas de données dans le [guide d’utilisation de la composition d’audiences fédérées](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/config/datamodel/schemas).

La section **[!UICONTROL Suivi]** fournit un enregistrement détaillé et chronologique de toutes les actions et tous les événements qui ont été réalisés dans votre environnement en temps réel. Vous trouverez plus d’informations sur le journal d’audit dans le [guide d’utilisation de la composition d’audiences fédérées](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/audit-trail/audit-trail).


La section **[!UICONTROL Base de données fédérées]** vous permet de connecter Adobe Experience Platform à votre entrepôt de données d’entreprise. Vous trouverez plus d’informations sur la connexion aux bases de données fédérées dans le [guide d’utilisation de la composition d’audiences fédérées](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/config/federated-db).

>[!AVAILABILITY]
>
>La composition d’audiences fédérées n’est actuellement disponible que pour un ensemble d’organisations (disponibilité limitée). Pour en savoir plus, contactez votre représentant ou représentante Adobe.

### [!UICONTROL Prise de décision]

Adobe Journey Optimizer est un service d’application reposant sur Experience Platform. Il vous permet d’utiliser de puissantes technologies de prise de décision pour offrir à vos clients la meilleure offre et la meilleure expérience possible sur tous les points de contact au bon moment. Pour en savoir plus sur Journey Optimizer, y compris sur l’utilisation des [!UICONTROL offres] et des [!UICONTROL activités], consultez la [documentation de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=fr).

### [!UICONTROL Administration]

L’interface utilisateur de Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation de la licence de votre entreprise, telles qu’elles sont capturées pendant un instantané quotidien. Accédez à ce tableau de bord en sélectionnant **[!UICONTROL Utilisation de la licence]** dans la navigation. Pour en savoir plus sur le tableau de bord de l’utilisation des licences, consultez le [guide de tableau de bord de l’utilisation des licences](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>Le tableau de bord de l’utilisation des licences est actuellement en version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

## Étapes suivantes

En lisant ce guide, vous avez maintenant découvert la page d’accueil et les principaux éléments de navigation de l’interface utilisateur de Platform. Pour plus d’informations sur l’utilisation de l’interface utilisateur, reportez-vous à la documentation de chaque service Platform. Les liens vers cette documentation sont fournis dans la section [navigation de gauche](#left-nav) qui figure plus haut dans ce document.
