---
keywords: Experience Platform;accueil;rubriques les plus consultées;diffusion en continu;connecteur de stockage dans le cloud;espace de stockage dans le cloud
solution: Experience Platform
title: Création d’un flux de données en continu pour une source de stockage dans le cloud dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Platform. Ce tutoriel décrit les étapes de configuration d’un nouveau flux de données à l’aide de votre connecteur de base de stockage dans le cloud.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 4a2d82fd6aec25f2570082ebc54f826251bc0a51
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 10%

---

# Création d’un flux de données en continu pour une source de stockage dans le cloud dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source vers un jeu de données Adobe Experience Platform. Ce tutoriel décrit les étapes à suivre pour créer un flux de données en continu pour une source de stockage dans le cloud dans l’interface utilisateur.

Avant de lancer ce tutoriel, vous devez établir une connexion valide et authentifiée entre votre compte de stockage dans le cloud et Platform. Si vous ne disposez pas déjà d’une connexion authentifiée, consultez l’un des tutoriels suivants pour plus d’informations sur l’authentification de vos comptes de stockage dans le cloud en continu :

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Flux de données](../../../../../dataflows/home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Les flux de données sont configurés entre différents services, depuis les sources, jusqu’à [!DNL Identity Service], jusqu’à [!DNL Profile] et jusqu’à [!DNL Destinations].
- [Préparation de données](../../../../../data-prep/home.md) : la préparation des données permet aux ingénieurs de données de mapper, transformer et valider les données vers et à partir du modèle de données d’expérience (XDM). Data Prep sʼaffiche en tant quʼétape de « mappage » dans les processus dʼingestion de données, y compris le processus dʼingestion de données CSV.
- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Ajout de données

Après avoir créé votre compte d’authentification de stockage dans le cloud en continu, l’étape **[!UICONTROL Sélectionner les données]** s’affiche, fournissant une interface vous permettant de sélectionner le flux de données que vous allez apporter à Platform.

- La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
- La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

![interface](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Sélectionnez le flux de données à utiliser, puis **[!UICONTROL Sélectionnez file]** pour charger un exemple de schéma.

>[!TIP]
>
>Si vos données sont conformes à XDM, vous pouvez ignorer le téléchargement d’un exemple de schéma et sélectionner **[!UICONTROL Suivant]** pour continuer.

![select-stream](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

Une fois votre schéma chargé, l’interface d’aperçu se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser l’utilitaire [!UICONTROL Champ de recherche] pour accéder à des éléments spécifiques de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![schema-preview](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Mappage

L’étape **[!UICONTROL Mappage]** s’affiche, fournissant une interface pour mapper les données source à un jeu de données Platform.

Sélectionnez un jeu de données dans lequel ingérer les données entrantes. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Nouveau jeu de données

Pour ingérer des données dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis. Pour ajouter un schéma, vous pouvez saisir un nom de schéma existant dans la boîte de dialogue **[!UICONTROL Sélectionner le schéma]**. Vous pouvez également sélectionner **[!UICONTROL Recherche avancée de schéma]** pour rechercher un schéma approprié.

![new-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

La fenêtre [!UICONTROL Sélectionner le schéma] s’affiche, vous indiquant la liste des schémas disponibles parmi lesquels choisir. Sélectionnez un schéma dans la liste pour mettre à jour le rail droit afin d’afficher les détails spécifiques au schéma que vous avez sélectionné, y compris des informations sur l’activation ou non du schéma pour [!DNL Profile].

Une fois que vous avez identifié et sélectionné le schéma à utiliser, sélectionnez **[!UICONTROL Terminé]**.

![select-schema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

La page [!UICONTROL Jeu de données Target] se met à jour avec le schéma sélectionné affiché dans le cadre du jeu de données. Au cours de cette étape, vous pouvez activer votre jeu de données pour [!DNL Profile] et créer une vue holistique des attributs et des comportements d’une entité. Les données de tous les jeux de données activés seront incluses dans [!DNL Profile] et des modifications sont appliquées lorsque vous enregistrez votre flux de données.

Active/désactive le bouton **[!UICONTROL Jeu de données de profil]** pour activer votre jeu de données cible pour [!DNL Profile].

![new-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Jeu de données existant

Pour ingérer des données dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**, puis sélectionnez l’icône du jeu de données.

![existing-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

La boîte de dialogue **[!UICONTROL Sélectionner un jeu de données]** s’affiche, vous fournissant une liste des jeux de données disponibles parmi lesquels choisir. Sélectionnez un jeu de données dans la liste pour mettre à jour le rail droit afin d’afficher les détails spécifiques au jeu de données que vous avez sélectionné, y compris des informations sur l’activation ou non du jeu de données pour [!DNL Profile].

Une fois que vous avez identifié et sélectionné le jeu de données à utiliser, sélectionnez **[!UICONTROL Terminé]**.

![select-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

Une fois que vous avez sélectionné votre jeu de données, sélectionnez la bascule [!DNL Profile] pour activer votre jeu de données pour [!DNL Profile].

![existing-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Mappage des champs standard

Une fois votre jeu de données et votre schéma créés, l’interface **[!UICONTROL Mapper les champs standard]** s’affiche, ce qui vous permet de configurer manuellement les champs de mappage pour vos données.

>[!TIP]
>
>Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation.

Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs calculées ou calculées. Pour plus d’informations sur les fonctions du mappeur et les champs calculés, consultez le [guide des fonctions de préparation de données](../../../../../data-prep/functions.md) ou le [guide des champs calculés](../../../../../data-prep/calculated-fields.md).

Une fois les données source mises en correspondance, sélectionnez **[!UICONTROL Suivant]**.

![mapping](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Détails du flux de données

L’étape **[!UICONTROL Détails du flux de données]** s’affiche, ce qui vous permet de nommer et de décrire brièvement votre nouveau flux de données.

Indiquez les valeurs du flux de données et sélectionnez **[!UICONTROL Suivant]**.

![dataflow-detail](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Révision

L’étape **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de passer en revue votre nouveau flux de données avant qu’il ne soit créé. Les détails sont regroupés dans les catégories suivantes :

- **[!UICONTROL Connexion]** : Affiche le nom de votre compte, le type de source et d’autres informations diverses spécifiques à la source de stockage dans le cloud de diffusion en continu que vous utilisez.
- **[!UICONTROL Attribuez des champs de jeu de données et de mappage]** : Affiche le jeu de données et le schéma cible que vous utilisez pour votre flux de données.

Une fois que vous avez examiné votre flux de données, sélectionnez **[!UICONTROL Terminer]** et laissez un certain temps pour que le flux de données soit créé.

![review](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Surveillance et suppression de votre flux de données

Une fois votre flux de données de stockage dans le cloud en continu créé, vous pouvez surveiller les données qui sont ingérées par celui-ci. Pour plus d’informations sur la surveillance et la suppression des flux de données en continu, consultez le tutoriel sur la [surveillance des flux de données en continu](../../monitor-streaming.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour diffuser des données à partir d’une source de stockage dans le cloud. Les données entrantes peuvent désormais être utilisées par les services Platform en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, consultez les documents suivants :

- [Présentation d’[!DNL Real-time Customer Profile]](../../../../../profile/home.md)
- [Présentation d’[!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)