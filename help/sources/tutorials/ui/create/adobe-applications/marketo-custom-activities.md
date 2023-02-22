---
title: Création d’une connexion source Marketo Engage et d’un flux de données pour les données d’activité personnalisée dans l’interface utilisateur
description: Ce tutoriel décrit les étapes à suivre pour créer une connexion source Marketo Engage et un flux de données dans l’interface utilisateur afin d’importer des données d’activités personnalisées dans Adobe Experience Platform.
source-git-commit: d049a29d4c39fa41917e8da1dde530966f4cbaf4
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 23%

---

# Créez un [!DNL Marketo Engage] connexion source et flux de données pour les données d’activité personnalisées dans l’interface utilisateur

>[!NOTE]
>
>Ce tutoriel décrit des étapes spécifiques à la configuration et à l’importation **activité personnalisée** des données provenant de [!DNL Marketo] à Experience Platform. Pour connaître les étapes à suivre **activité standard** data, lisez la [[!DNL Marketo] Guide de l’interface utilisateur](./marketo.md).

En complément de [activités standard](../../../../connectors/adobe-applications/mapping/marketo.md#activities), vous pouvez également utiliser la variable [!DNL Marketo] source pour importer des données d’activités personnalisées dans Adobe Experience Platform. Ce document décrit les étapes de création d’une connexion source et d’un flux de données pour les données d’activité personnalisées à l’aide du [!DNL Marketo] source dans l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Espaces de noms B2B et utilitaire de génération automatique de schéma](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Les espaces de noms B2B et l’utilitaire de génération automatique de schéma vous permettent d’utiliser [!DNL Postman] pour générer automatiquement des valeurs pour vos espaces de noms et vos schémas B2B. Vous devez d’abord renseigner vos espaces de noms et schémas B2B avant de créer une [!DNL Marketo] connexion source et flux de données.
* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données d’expérience client.
   * [Créer et modifier des schémas dans l’interface utilisateur](../../../../../xdm/ui/resources/schemas.md) : découvrez comment créer et modifier des schémas dans l’interface utilisateur.
* [Espaces de noms d’identité](../../../../../identity-service/namespaces.md) : les espaces de noms d’identité sont des composants d’[!DNL Identity Service] qui servent d’indicateurs du contexte auquel une identité se rapporte. Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Récupération des détails de votre activité personnalisée

Première étape pour obtenir des données d’activité personnalisées à partir de [!DNL Marketo] pour Experience Platform est de récupérer le nom de l’API et le nom d’affichage de votre activité personnalisée.

Connectez-vous à votre compte à l’aide du [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) . Dans le volet de navigation de gauche, sous [!DNL Database Management], sélectionnez **Activités personnalisées Marketo**.

L’interface se met à jour pour afficher vos activités personnalisées, y compris des informations sur leurs noms d’affichage et noms d’API respectifs. Vous pouvez également utiliser le rail droit pour sélectionner et afficher d’autres activités personnalisées à partir de votre compte.

![Interface des activités personnalisées dans l’interface utilisateur de Adobe Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Sélectionner **Champs** dans l’en-tête supérieur pour afficher les champs associés à votre activité personnalisée. Dans cette page, vous pouvez afficher les noms, les noms d’API, les descriptions et les types de données des champs de votre activité personnalisée. Les détails relatifs aux champs individuels seront utilisés ultérieurement lors de la création d’un schéma.

![La page Détails des champs d’activité personnalisés Marketo dans l’interface utilisateur du Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Configuration de groupes de champs pour les activités personnalisées dans le schéma des activités B2B

Dans le *[!UICONTROL Schémas]* Tableau de bord de l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Parcourir]** puis sélectionnez **[!UICONTROL Activité B2B]** dans la liste des schémas.

>[!TIP]
>
>Utilisez la barre de recherche pour accélérer la navigation dans la liste des schémas.

![Espace de travail des schémas dans l’interface utilisateur Experience Platform avec le schéma d’activité B2B sélectionné.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Création d’un groupe de champs pour une activité personnalisée

Ajoutez ensuite un nouveau groupe de champs au [!DNL B2B Activity] schéma. Ce groupe de champs doit correspondre à l’activité personnalisée que vous souhaitez ingérer et doit utiliser le nom d’affichage de l’activité personnalisée que vous avez récupéré précédemment.

Pour ajouter un nouveau groupe de champs, sélectionnez **[!UICONTROL + Ajouter]** en regard de la variable *[!UICONTROL Groupes de champs]* panneau sous *[!UICONTROL Composition]*.

![Structure du schéma.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

Le *[!UICONTROL Ajouter des groupes de champs]* s’affiche. Sélectionner **[!UICONTROL Créer un groupe de champs]** puis indiquez le même nom d’affichage pour l’activité personnalisée que vous avez récupérée à une étape précédente et fournissez une description facultative pour votre nouveau groupe de champs. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Ajouter des groupes de champs]**.

![Fenêtre d’étiquetage et de création d’un groupe de champs.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Une fois créé, le nouveau groupe de champs pour l’activité personnalisée s’affiche dans la [!UICONTROL Groupes de champs] catalogue.

![Structure du schéma avec un nouveau groupe de champs ajouté sous le panneau du groupe de champs.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Ajouter un nouveau champ à la structure de votre schéma

Ajoutez ensuite un nouveau champ à votre schéma. Ce nouveau champ doit être défini sur `type: object` et contiendra les champs individuels de l’activité personnalisée.

Pour ajouter un nouveau champ, sélectionnez le signe plus (`+`) en regard du nom du schéma. Une entrée pour *[!UICONTROL Champ sans titre | Type]* apparaît. Ensuite, configurez les propriétés de votre champ à l’aide de la fonction *[!UICONTROL Propriétés du champ]* du panneau. Définissez le nom du champ comme nom d’API de votre activité personnalisée et définissez le nom d’affichage comme nom d’affichage de votre activité personnalisée. Définissez ensuite le type sur `object` et affectez le groupe de champs à l’activité personnalisée que vous avez créée à l’étape précédente. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![La structure du schéma avec le plus (`+`) est sélectionné afin qu’un nouveau champ puisse être ajouté.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

Le nouveau champ apparaît dans votre schéma.

![Un nouveau champ a été ajouté au schéma.](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Ajouter des sous-champs au champ d’objet {#add-sub-fields-to-the-object-field}

La dernière étape de la préparation de votre schéma consiste à ajouter des champs individuels dans le champ que vous avez créé à l’étape précédente.

![Groupe de sous-champs ajoutés à un champ du schéma.](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Créer un flux de données

Une fois la configuration de votre schéma terminée, vous pouvez créer un flux de données pour vos données d’activité personnalisées.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Applications Adobe], sélectionnez **[!UICONTROL Marketo Engage]**. Sélectionnez ensuite **[!UICONTROL Ajouter des données]** pour créer un flux de données [!DNL Marketo].

![Catalogue des sources sur l’interface utilisateur de l’Experience Platform avec la source du Marketo Engage sélectionnée.](../../../../images/tutorials/create/marketo/catalog.png)

### Sélectionner les données

Sélectionner **[!UICONTROL Activités]** de la liste de [!DNL Marketo] jeux de données, puis sélectionnez **[!UICONTROL Suivant]**.

![L’étape de sélection des données dans le workflow des sources avec le jeu de données des activités sélectionné.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Détails du flux de données

Ensuite, [fournir des informations sur votre flux de données ;](./marketo.md#provide-dataflow-details), y compris les noms et descriptions de votre jeu de données et de votre flux de données, le schéma que vous utiliserez et les configurations pour [!DNL Profile] ingestion, diagnostics d’erreur et ingestion partielle.

![L’étape de détail du flux de données.](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Mappage

Les mappages des champs d’activité standard sont automatiquement renseignés, mais les champs d’activité personnalisés doivent être mappés manuellement à leurs champs cibles correspondants.

Pour commencer à mapper vos champs d’activité personnalisés, sélectionnez **[!UICONTROL Nouveau type de champ]** puis sélectionnez **[!UICONTROL Ajouter un nouveau champ]**.

![L’étape de mappage avec le menu déroulant pour ajouter un nouveau champ.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Parcourez la structure de données source et recherchez le champ d’activité personnalisé à ingérer. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Sélectionner]**.

>[!TIP]
>
>Pour éviter toute confusion et gérer les noms de champ en double, les champs d’activité personnalisés sont précédés du préfixe du nom de l’API.

![Structure des données source.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Pour ajouter un champ cible, sélectionnez l&#39;icône de schéma ![icône de schéma](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png) puis sélectionnez les champs personnalisés de l&#39;activité dans le schéma cible.

![Structure du schéma cible.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Répétez les étapes pour ajouter le reste de vos champs de mappage d’activité personnalisés. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Tous les mappages pour les données source et cible.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Révision

L’écran de *[!UICONTROL Révision]* s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant de l’entité source choisie et le nombre de colonnes au sein de cette entité source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez révisé votre flux de données, sélectionnez **[!UICONTROL Enregistrer et ingérer]** et patientez quelques instants le temps que le flux de données soit créé.

![L’étape de révision finale qui résume les informations sur la connexion, le jeu de données et les champs de mappage.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

>[!NOTE]
>
>Une fois l’ingestion terminée, le jeu de données ingéré contient toutes les activités, y compris les activités standard et personnalisées de votre [!DNL Marketo] instance. Pour sélectionner vos enregistrements d’activité personnalisés sur Platform, vous devez utiliser [Query Service](../../../../../query-service/home.md) et fournissez les prédicats appropriés.

## Étapes suivantes

En suivant ce tutoriel, vous avez configuré un schéma Platform pour [!DNL Marketo] données d’activité personnalisées et créé un flux de données pour importer ces données dans Platform. Pour obtenir des informations générales sur la variable [!DNL Marketo] source, lisez la [[!DNL Marketo] présentation de la source](../../../../connectors/adobe-applications/marketo/marketo.md).