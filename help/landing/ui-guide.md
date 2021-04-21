---
keywords: Experience Platform ; accueil ; sujets populaires ; Adobe Experience Platform ; guide de l'utilisateur ; guide de l'interface utilisateur ; guide de l'interface utilisateur de la plate-forme ; introduction à la plate-forme ; tableau de bord ;
solution: Experience Platform
title: Présentation de l’interface utilisateur Experience Platform
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 2%

---

# Guide de l’interface utilisateur Adobe Experience Platform

Ce guide présente l’utilisation de l’interface utilisateur de Adobe Experience Platform, explique les différents composants utilisés et fournit des liens vers d’autres documents pour plus d’informations.

Pour en savoir plus sur Adobe Experience Platform, veuillez lire la [présentation Experience Platform](home.md).

## Ecran d’accueil

Après vous être connecté à Adobe Experience Platform, vous vous trouvez sur la page [!UICONTROL Accueil], qui comprend les sections [tableau de bord de mesures](#metrics), [données récentes](#recent-data) et [apprentissage recommandé](#recommended-learning).

![](images/user-guide/homepage.png)

### Mesures

Le tableau de bord de mesures fournit des cartes qui vous donnent des informations sur les jeux de données, les profils, les segments et les destinations au sein de votre organisation.

![](images/user-guide/homepage-dashboard.png)

La section **[!UICONTROL Jeux de données]** indique le nombre de jeux de données au sein de votre organisation IMS. Ce numéro est mis à jour lorsqu&#39;un nouveau jeu de données est créé. Pour plus d&#39;informations sur les jeux de données, consultez l&#39;[aperçu des jeux de données](../catalog/datasets/overview.md).

La section **[!UICONTROL Profils]** indique le nombre total de personnes ayant des profils au sein de votre organisation IMS, à l’exclusion des fragments de profil. Ce nombre total de personnes représente l’audience adressable totale et est mis à jour une fois toutes les 24 heures. Pour plus d’informations sur les profils, consultez la [Présentation du Profil client en temps réel](../profile/home.md).

La section **[!UICONTROL Segments]** indique le nombre total de segments créés dans votre organisation IMS. Ce numéro est mis à jour lorsqu’un nouveau segment est créé. Pour plus d’informations sur les segments, consultez la section [Présentation du service de segmentation](../segmentation/home.md).

La section **[!UICONTROL Destinations]** indique le nombre total de destinations créées pour l’organisation IMS. Ce numéro est mis à jour lorsqu’une nouvelle destination est créée. Vous trouverez plus d&#39;informations sur les destinations dans le [aperçu des destinations](../destinations/home.md).

### Données récentes

Le tableau de bord de données récent fournit des informations sur les jeux de données, les sources, les segments et les destinations récemment créés.

![](images/user-guide/homepage-recent.png)

La section **[!UICONTROL Jeu de données récents]** liste les cinq derniers jeux de données créés au sein de votre organisation IMS. Cette liste est mise à jour chaque fois qu&#39;un nouveau jeu de données est créé. Vous pouvez sélectionner un jeu de données de la liste à la vue pour plus d&#39;informations sur le jeu de données spécifié ou sélectionner **[!UICONTROL Vue all]** pour afficher la liste de tous les jeux de données créés. Pour plus d&#39;informations sur les jeux de données, consultez l&#39;[aperçu des jeux de données](../catalog/datasets/overview.md).

La section **[!UICONTROL Sources récentes]** liste les cinq connecteurs source les plus récents au sein de votre organisation IMS. Cette liste est mise à jour chaque fois qu&#39;un nouveau connecteur source est créé. Vous pouvez sélectionner une connexion source de la liste à la vue pour plus d&#39;informations sur le connecteur spécifié ou sélectionner **[!UICONTROL Vue all]** pour voir la liste de toutes les connexions source créées. Vous trouverez plus d&#39;informations sur les sources dans le [aperçu des sources](../sources/home.md).

La section **[!UICONTROL Segments récents]** liste les cinq définitions de segment créées le plus récemment au sein de votre organisation IMS. Cette liste est mise à jour chaque fois qu’une nouvelle définition de segment est créée. Vous pouvez sélectionner une définition de segment de la liste à la vue plus d&#39;informations sur la définition de segment spécifiée ou sélectionner **[!UICONTROL Vue all]** pour afficher une liste de toutes les définitions de segment créées. Pour plus d’informations sur les segments, consultez la section [Présentation du service de segmentation](../segmentation/home.md).

La section **[!UICONTROL Destinations récentes]** liste les cinq destinations les plus récemment créées au sein de votre organisation IMS. Cette liste est mise à jour chaque fois qu’une nouvelle destination est créée. Vous pouvez sélectionner une destination de la liste à la vue plus d&#39;informations sur la destination spécifiée ou sélectionner **[!UICONTROL Vue all]** pour afficher une liste de toutes les destinations créées. Vous trouverez plus d&#39;informations sur les destinations dans le [aperçu des destinations](../destinations/home.md).

### Apprentissage recommandé

La section **[!UICONTROL Apprentissage recommandé]** contient des liens vers la documentation utile pour commencer à utiliser Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barre de navigation supérieure

La barre de navigation supérieure de l’interface utilisateur de la plate-forme affiche l’organisation IMS dans laquelle vous êtes actuellement connecté et fournit plusieurs contrôles importants.

Sur le côté gauche de la barre de navigation se trouve le logo Adobe Experience Platform. Si vous sélectionnez cette option à tout moment, vous revenez à l’écran d’accueil de l’interface utilisateur de la plate-forme.

![](./images/user-guide/homepage-top-nav-bar.png)

### Commutateur d&#39;organisation IMS

Le premier élément sur le côté droit de la barre de navigation supérieure est le commutateur **IMS Organization**.

![](./images/user-guide/homepage-ims-org.png)

Si vous sélectionnez le sélecteur, un menu déroulant des organisations IMS auxquelles vous avez accès s&#39;affiche, le cas échéant. Sélectionnez une option répertoriée pour passer à cette organisation IMS.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Changement d’application

L&#39;élément suivant sur le côté droit de la navigation supérieure est le **commutateur d&#39;applications**, représenté par l&#39;icône ![commutateur d&#39;applications](./images/user-guide/app-switcher-icon.png). Lorsque vous sélectionnez cette icône, vous pouvez basculer entre les applications d’Adobe auxquelles votre organisation IMS a accès, telles que Experience Platform, Analytics, Assets et Launch.

### Aide

À droite du sélecteur d’applications se trouve le **menu d’aide et de support**, qui est représenté par l’icône ![point d’interrogation/aide](./images/user-guide/help-icon.png). Lorsque vous sélectionnez cette icône, un menu contextuel s’affiche, contenant plusieurs ressources d’aide et d’assistance. L&#39;onglet **[!UICONTROL Aide]** affiche une liste de la documentation pertinente pour la page sur laquelle vous vous trouvez actuellement. L&#39;onglet **[!UICONTROL Support]** vous permet de créer un ticket d&#39;assistance auprès de l&#39;équipe d&#39;assistance Adobe. L&#39;onglet **[!UICONTROL Commentaires]** vous permet d&#39;envoyer des commentaires sur la plate-forme à l&#39;Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notifications et annonces

Dans la section **notifications**, qui est représentée par l&#39;icône ![bell/Notifications and Annoncements](images/user-guide/notification-icon.png). L&#39;onglet **[!UICONTROL Notifications]** affiche des informations importantes sur le produit et d&#39;autres mises à jour pertinentes, tandis que l&#39;onglet **[!UICONTROL Annonces]** affiche des informations sur la maintenance du service.

### Profil utilisateur

Le dernier élément de la barre de navigation supérieure est **paramètres utilisateur**, qui est représenté par l&#39;icône ![paramètres utilisateur/Profil utilisateur](images/user-guide/profile-icon.png). Sélectionnez cette icône pour modifier vos préférences ou vous déconnecter.

### Environnements de test

Immédiatement sous la barre de navigation supérieure se trouve la barre de sandbox. Cette barre indique le sandbox que vous utilisez actuellement pour Platform. Vous trouverez plus d&#39;informations sur les sandbox dans le [aperçu des sandbox](../sandboxes/home.md).

## Navigation de gauche {#left-nav}

La navigation sur le côté gauche de l’écran liste tous les différents services pris en charge dans l’interface utilisateur de la plate-forme.

>[!IMPORTANT]
>
>Il se peut que certaines sections de la barre de navigation de gauche n’apparaissent pas ou ne soient pas grisées. Ceci est dû au fait que vous n’avez pas accès à ces fonctionnalités. Si vous pensez avoir accès à ces sections, contactez votre administrateur système.

![](images/user-guide/homepage-left.png)

La section **[!UICONTROL Accueil]** vous permet de revenir à la page d&#39;accueil de l&#39;interface utilisateur de la plate-forme.

La section **[!UICONTROL Workflows]** présente une liste de workflows à plusieurs étapes pour effectuer des opérations dans Platform. Vous trouverez plus d&#39;informations sur les workflows dans le [aperçu des workflows](./workflows.md).

### [!UICONTROL Connexions]

La section **[!UICONTROL Sources]** vous permet de créer, de mettre à jour et de supprimer des connexions source, ce qui vous permet d&#39;assimiler des données provenant de sources externes dans la plate-forme. Vous trouverez plus d&#39;informations sur les sources dans le [aperçu des sources](../sources/home.md).

La section **[!UICONTROL Destinations]** vous permet de créer, de mettre à jour et de supprimer des destinations, ce qui vous permet d&#39;exporter des données de la plate-forme vers de nombreuses destinations externes. Vous trouverez plus d&#39;informations sur les destinations dans le [aperçu des destinations](../destinations/home.md).

### [!UICONTROL Informations     ]

La section **[!UICONTROL Profils]** vous permet de parcourir les profils client, les mesures de profil de vue, de créer et de gérer des stratégies de fusion et des schémas d&#39;union de vue. Pour en savoir plus sur l&#39;utilisation de la section [!UICONTROL Profils], consultez le [[!DNL Profile] guide d&#39;utilisateur](../profile/ui/user-guide.md). Pour plus d’informations sur le Profil client en temps réel, consultez la [Présentation du Profil client en temps réel](../profile/home.md).

La section **[!UICONTROL Segments]** permet de créer et de gérer des définitions de segment. Pour en savoir plus sur l&#39;utilisation de la section [!UICONTROL Segments], consultez le [guide d&#39;utilisateur de la segmentation](../segmentation/ui/overview.md). Pour plus d&#39;informations sur le service de segmentation, consultez la section [Présentation du service de segmentation](../segmentation/home.md).

La section **[!UICONTROL Identités]** vous permet de créer et de gérer des espaces de nommage d&#39;identité. Pour plus d&#39;informations sur la section [!UICONTROL Identités], y compris des informations sur les espaces de nommage d&#39;identité et sur la façon d&#39;utiliser les identités dans l&#39;interface utilisateur de la plate-forme, consultez la [présentation de l&#39;espace de nommage d&#39;identité](../identity-service/namespaces.md).

### [!UICONTROL Confidentialité]

La section **[!UICONTROL Stratégies]** vous permet de créer et de gérer des stratégies d&#39;utilisation des données. Pour en savoir plus sur l&#39;utilisation de la section Stratégies, consultez le [guide d&#39;utilisation des stratégies d&#39;utilisation des données](../data-governance/policies/user-guide.md). Vous trouverez plus d&#39;informations sur les stratégies d&#39;utilisation des données dans le [aperçu des stratégies d&#39;utilisation des données](../data-governance/policies/overview.md).

La section **[!UICONTROL Demandes]** vous permet de créer et de gérer des demandes de confidentialité. Veuillez noter que vous devez être placé sur la liste autorisée pour avoir accès à l&#39;interface utilisateur du Privacy Service. Pour en savoir plus sur l&#39;utilisation de la section Demandes, veuillez lire le [guide de l&#39;utilisateur Privacy Service](../privacy-service/ui/user-guide.md). Vous trouverez plus d&#39;informations sur le Privacy Service dans le [aperçu du Privacy Service](../privacy-service/home.md).

### [!UICONTROL Science des données]

La section **[!UICONTROL Ordinateurs portables]** donne accès à JupyterLab, un environnement de développement interactif qui vous permet d&#39;explorer, d&#39;analyser et de modéliser vos données. Pour en savoir plus sur l&#39;utilisation de la section Ordinateurs portables, consultez le [Guide d&#39;utilisation de JupyterLab](../data-science-workspace/jupyterlab/overview.md). Pour plus d’informations sur Data Science Workspace, consultez la section [Présentation de Data Science Workspace](../data-science-workspace/home.md).

La section **[!UICONTROL Modèles]** vous permet de tirer parti de l&#39;apprentissage automatique et de l&#39;intelligence artificielle pour créer, développer, former et ajuster des modèles afin de faire des prédictions. Vous trouverez plus d&#39;informations sur la section Modèles dans le didacticiel sur la [formation et l&#39;évaluation d&#39;un modèle](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

La section **[!UICONTROL Services]** vous permet de gérer vos modèles publiés pour la formation et le score planifiés, ou de tirer parti des services intelligents de Adobe, un ensemble de services d&#39;IA qui offrent des expériences client personnalisées en temps réel. Pour plus d&#39;informations sur la section Services, consultez le [didacticiel Publier un modèle en tant que service](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Gestion des données]

La section **[!UICONTROL Schémas]** vous permet de créer et de gérer des schémas de modèle de données d’expérience (XDM). Pour en savoir plus sur les schémas, veuillez lire le didacticiel sur la création d&#39;un schéma [. ](../xdm/tutorials/create-schema-ui.md) Pour plus d&#39;informations sur XDM, consultez la section [Présentation du système XDM](../xdm/home.md).

La section **[!UICONTROL Datasets]** permet de créer et de gérer des jeux de données. Pour plus d&#39;informations sur les jeux de données, consultez le [guide d&#39;utilisateur des jeux de données](../catalog/datasets/user-guide.md).

La section **[!UICONTROL Requêtes]** vous permet de créer et de gérer des requêtes, de consigner des requêtes SQL créées par Adobe Experience Platform Requête Service et de vue de vos informations d&#39;identification PostgreSQL. Pour plus d&#39;informations sur les requêtes, consultez le [Guide de l&#39;utilisateur de Requête Service](../query-service/ui/overview.md).

La section **[!UICONTROL Surveillance]** permet de surveiller l’assimilation par lot et en flux continu. Pour plus d&#39;informations sur la surveillance, consultez le [guide de l&#39;utilisateur d&#39;assimilation des données de surveillance](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Prise de décision]

Offer Decisioning est un service applicatif intégré à Adobe Experience Platform. Il vous permet de tirer parti de l’Experience Platform pour offrir à vos clients la meilleure offre et la meilleure expérience possible sur tous les points de contact au bon moment. Pour en savoir plus sur l&#39;Offer decisioning, y compris l&#39;utilisation des [!UICONTROL Offres] et [!UICONTROL Activités], consultez la [documentation sur l&#39;Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning.html).

### [!UICONTROL Administration]

L’interface utilisateur de la plate-forme fournit un tableau de bord par lequel vous pouvez vue des informations importantes sur l’utilisation des licences de votre entreprise, telles qu’elles sont capturées au cours d’un instantané quotidien. Pour y accéder, sélectionnez **[!UICONTROL Utilisation de la licence]** dans la barre de navigation. Pour en savoir plus sur le tableau de bord d&#39;utilisation des licences, consultez le [guide du tableau de bord d&#39;utilisation des licences](license-usage-dashboard.md).

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord d’utilisation des licences est actuellement en alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

## Étapes suivantes

En lisant ce guide, vous avez maintenant été initié à la page d&#39;accueil et aux principaux éléments de navigation de l&#39;interface utilisateur de la plate-forme. Pour plus d&#39;informations sur le fonctionnement de l&#39;interface utilisateur, reportez-vous à la documentation de chaque service de plateforme. Vous trouverez des liens vers cette documentation dans la section [navigation de gauche](#left-nav) qui se trouve plus haut dans ce document.
