---
keywords: Experience Platform;accueil;rubriques les plus consultées;diffusion en continu;connecteur de stockage dans le cloud;stockage dans le cloud
solution: Experience Platform
title: Créer un flux de données en continu pour une source d’espace de stockage dans l’interface utilisateur
type: Tutorial
description: Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Experience Platform. Ce tutoriel décrit les étapes à suivre pour configurer un nouveau flux de données à l’aide de votre connecteur de base d’espace de stockage.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 20%

---

# Créer un flux de données en continu pour une source d’espace de stockage dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Adobe Experience Platform. Ce tutoriel décrit les étapes à suivre pour créer un flux de données en continu pour une source d’espace de stockage dans l’interface utilisateur.

Avant de suivre ce tutoriel, vous devez d’abord établir une connexion valide et authentifiée entre votre compte d’espace de stockage et Experience Platform. Si vous ne disposez pas déjà d’une connexion authentifiée, consultez l’un des tutoriels suivants pour obtenir des informations sur l’authentification de vos comptes d’espace de stockage dans le cloud en flux continu :

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Flux de données](../../../../../dataflows/home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Experience Platform. Les flux de données sont configurés sur différents services, des sources aux [!DNL Identity Service], en passant par les [!DNL Profile] et les [!DNL Destinations].
- [Préparation de données](../../../../../data-prep/home.md) : la préparation des données permet aux ingénieur(e)s de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM). La préparation des données apparaît comme étape de « mappage » dans les processus dʼingestion de données, y compris le workflow dʼingestion de données CSV.
- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Ajouter des données

>[!NOTE]
>
>Vous ne pouvez créer qu’un seul flux de données source par groupe de clients pour un hub d’événements donné.

Une fois que vous avez créé votre compte d’espace de stockage dans le cloud pour la diffusion en continu, l’étape **[!UICONTROL Sélectionner les données]** s’affiche, fournissant une interface vous permettant de sélectionner le flux de données que vous apporterez à Experience Platform.

- La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
- La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

![ interface ](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Sélectionnez le flux de données à utiliser, puis sélectionnez **[!UICONTROL Choisir un fichier]** pour charger un exemple de schéma.

>[!TIP]
>
>Si vos données sont conformes à XDM, vous pouvez ignorer le chargement d’un exemple de schéma, puis sélectionner **[!UICONTROL Suivant]** pour continuer.

![select-stream](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

Une fois le schéma chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface de prévisualisation vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser l’utilitaire [!UICONTROL Champ de recherche] pour accéder à des éléments spécifiques à partir de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![schema-preview](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Mappage

L’étape **[!UICONTROL Mappage]** s’affiche, fournissant une interface pour mapper les données sources à un jeu de données Experience Platform.

Sélectionnez un jeu de données dans lequel ingérer les données entrantes. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Nouveau jeu de données

Pour ingérer des données dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis. Pour ajouter un schéma, vous pouvez saisir un nom de schéma existant dans la boîte de dialogue **[!UICONTROL Sélectionner un schéma]**. Vous pouvez également sélectionner **[!UICONTROL Recherche avancée de schéma]** pour rechercher un schéma approprié.

![new-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

La fenêtre [!UICONTROL &#x200B; Sélectionner un schéma &#x200B;] s’affiche, vous fournissant une liste des schémas disponibles parmi lesquels choisir. Sélectionnez un schéma dans la liste pour mettre à jour le rail de droite afin d’afficher les détails spécifiques au schéma que vous avez sélectionné, y compris des informations indiquant si le schéma est activé pour la [!DNL Profile].

Une fois que vous avez identifié et sélectionné le schéma à utiliser, cliquez sur **[!UICONTROL Terminé]**.

![select-schema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

La page [!UICONTROL Jeu de données cible] est mise à jour avec le schéma sélectionné affiché dans le jeu de données. Au cours de cette étape, vous pouvez activer votre jeu de données pour la [!DNL Profile] et créer une vue holistique des attributs et des comportements d’une entité. Les données de tous les jeux de données activés seront incluses dans [!DNL Profile] et les modifications sont appliquées lorsque vous enregistrez votre flux de données.

Activez le bouton **[!UICONTROL Jeu de données de profil]** pour activer votre jeu de données cible à [!DNL Profile].

![new-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Jeu de données existant

Pour ingérer des données dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**, puis sélectionnez l’icône du jeu de données.

![existing-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

La boîte de dialogue **[!UICONTROL Sélectionner un jeu de données]** s’affiche, vous fournissant une liste des jeux de données disponibles parmi lesquels choisir. Sélectionnez un jeu de données dans la liste pour mettre à jour le rail de droite afin d’afficher les détails spécifiques au jeu de données que vous avez sélectionné, y compris des informations indiquant si le jeu de données peut être activé pour [!DNL Profile].

Une fois que vous avez identifié et sélectionné le jeu de données à utiliser, cliquez sur **[!UICONTROL Terminé]**.

![select-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

Une fois que vous avez sélectionné votre jeu de données, cliquez sur le bouton (bascule) [!DNL Profile] pour activer votre jeu de données à des fins d’[!DNL Profile].

![existing-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Mappage des champs standard

Une fois votre jeu de données et votre schéma établis, l’interface **[!UICONTROL Mapper les champs standard]** s’affiche, vous permettant de configurer manuellement les champs de mappage pour vos données.

>[!TIP]
>
>Experience Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation.

Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [ Guide de l’interface utilisateur de la préparation des données ](../../../../../data-prep/ui/mapping.md).

Une fois vos données source mappées, sélectionnez **[!UICONTROL Suivant]**.

![mappage](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Détails du flux de données

L’étape **[!UICONTROL Détails du flux de données]** s’affiche, vous permettant de nommer et de donner une brève description de votre nouveau flux de données.

Indiquez les valeurs du flux de données et sélectionnez **[!UICONTROL Suivant]**.

![dataflow-detail](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Révision

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

- **[!UICONTROL Connexion]** : affiche le nom de votre compte, le type de source et d’autres informations diverses spécifiques à la source de stockage dans le cloud en flux continu que vous utilisez.
- **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données et le schéma cibles que vous utilisez pour votre flux de données.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![review](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Surveiller et supprimer le flux de données

Une fois votre flux de données de stockage dans le cloud en flux continu créé, vous pouvez surveiller les données ingérées par celui-ci. Pour plus d’informations sur la surveillance et la suppression des flux de données en flux continu, consultez le tutoriel sur la [surveillance des flux de données en flux continu](../../monitor-streaming.md).

## Étapes suivantes

Ce tutoriel vous a permis de créer un flux de données pour diffuser des données à partir d’une source d’espace de stockage dans le cloud. Ces données entrantes peuvent désormais être utilisées par les services Experience Platform en aval tels que [!DNL Real-Time Customer Profile] et [!DNL Data Science Workspace]. Consultez les documents suivants pour plus d’informations :

- [Présentation de [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
- [Présentation de [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)