---
title: Créer une connexion Source Marketo Engage et un flux de données pour les données d’activité personnalisées dans l’interface utilisateur
description: Ce tutoriel décrit les étapes à suivre pour créer une connexion source Marketo Engage et un flux de données dans l’interface utilisateur afin d’importer des données d’activités personnalisées dans Adobe Experience Platform.
exl-id: 05a7b500-11d2-4d58-be43-a2c4c0ceeb87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 17%

---

# Créer une connexion source [!DNL Marketo Engage] et un flux de données pour les données d’activité personnalisées dans l’interface utilisateur

>[!NOTE]
>
>Ce tutoriel décrit les étapes spécifiques à suivre pour configurer et importer des données **activité personnalisée** de [!DNL Marketo] vers Experience Platform. Pour savoir comment importer des données **activité standard**, consultez le guide de l’interface utilisateur [[!DNL Marketo] ](./marketo.md).

Outre les [activités standard](../../../../connectors/adobe-applications/mapping/marketo.md#activities), vous pouvez également utiliser la source de [!DNL Marketo] pour importer des données d’activités personnalisées dans Adobe Experience Platform. Ce document décrit les étapes à suivre pour créer une connexion source et un flux de données pour les données d’activité personnalisées à l’aide de la source [!DNL Marketo] dans l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Utilitaire de génération automatique de schémas et d’espaces de noms B2B ](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) : l’utilitaire de génération automatique de schémas et d’espaces de noms B2B vous permet d’utiliser [!DNL Postman] pour générer automatiquement des valeurs pour vos schémas et espaces de noms B2B. Vous devez d’abord terminer vos espaces de noms et schémas B2B, avant de créer une connexion source [!DNL Marketo] et un flux de données.
* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données d’expérience client.
   * [Créer et modifier des schémas dans l’interface utilisateur](../../../../../xdm/ui/resources/schemas.md) : découvrez comment créer et modifier des schémas dans l’interface utilisateur.
* [Espaces de noms d’identité](../../../../../identity-service/features/namespaces.md) : les espaces de noms d’identité sont des composants d’[!DNL Identity Service] qui servent d’indicateurs du contexte auquel une identité se rapporte. Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Récupérer les détails de votre activité personnalisée

La première étape pour importer des données d’activité personnalisées de [!DNL Marketo] vers Experience Platform consiste à récupérer le nom de l’API et le nom d’affichage de votre activité personnalisée.

Connectez-vous à votre compte à l’aide de l’interface [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1). Dans le volet de navigation de gauche, sous [!DNL Database Management], sélectionnez **Activités personnalisées Marketo**.

L’interface met à jour un affichage de vos activités personnalisées, y compris des informations sur leurs noms d’affichage et noms d’API respectifs. Vous pouvez également utiliser le rail droit pour sélectionner et afficher d’autres activités personnalisées à partir de votre compte.

![Interface des activités personnalisées dans l’interface utilisateur de Adobe Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Sélectionnez **Champs** dans l’en-tête supérieur pour afficher les champs associés à votre activité personnalisée. Dans cette page, vous pouvez afficher les noms, noms d’API, descriptions et types de données des champs dans votre activité personnalisée. Les détails concernant les champs individuels seront utilisés à une étape ultérieure, lors de la création d’un schéma.

![Page Détails des champs d’activité personnalisés Marketo dans l’interface utilisateur de Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Configurer des groupes de champs pour les activités personnalisées dans le schéma d’activités B2B

Dans le tableau de bord *[!UICONTROL Schémas]* de l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Parcourir]** puis sélectionnez **[!UICONTROL Activité B2B]** dans la liste des schémas.

>[!TIP]
>
>Utilisez la barre de recherche pour accélérer votre navigation dans la liste des schémas.

![Espace de travail des schémas dans l’interface utilisateur d’Experience Platform avec le schéma d’activité B2B sélectionné.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Créer un nouveau groupe de champs pour l’activité personnalisée

Ajoutez ensuite un nouveau groupe de champs au schéma [!DNL B2B Activity]. Ce groupe de champs doit correspondre à l’activité personnalisée que vous souhaitez ingérer et doit utiliser le nom d’affichage de l’activité personnalisée que vous avez récupéré précédemment.

Pour ajouter un nouveau groupe de champs, sélectionnez **[!UICONTROL + Ajouter]** en regard du panneau *[!UICONTROL Groupes de champs]* sous *[!UICONTROL Composition]*.

![Structure du schéma.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

La fenêtre *[!UICONTROL Ajouter des groupes de champs]* s’affiche. Sélectionnez **[!UICONTROL Créer un groupe de champs]** puis indiquez le même nom d’affichage pour l’activité personnalisée récupérée à une étape précédente et fournissez une description facultative de votre nouveau groupe de champs. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Ajouter des groupes de champs]**.

![Fenêtre permettant de libeller et de créer un groupe de champs.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Une fois créé, votre nouveau groupe de champs pour l’activité personnalisée apparaît dans le catalogue [!UICONTROL Groupes de champs].

![Structure du schéma avec un nouveau groupe de champs ajouté sous le panneau groupe de champs.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Ajoutez un nouveau champ à la structure de votre schéma

Ajoutez ensuite un nouveau champ à votre schéma. Ce nouveau champ doit être défini sur `type: object` et contiendra les champs individuels de l’activité personnalisée.

Pour ajouter un nouveau champ, sélectionnez le signe plus (`+`) à côté du nom du schéma. Une entrée pour *[!UICONTROL Champ sans titre | Type]* s’affiche. Configurez ensuite les propriétés de votre champ à l’aide du panneau *[!UICONTROL Propriétés du champ]*. Définissez le nom du champ sur le nom d’API de votre activité personnalisée et définissez le nom d’affichage sur le nom d’affichage de votre activité personnalisée. Définissez ensuite le type sur `object` et affectez le groupe de champs au groupe de champs d’activité personnalisée que vous avez créé à l’étape précédente. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![Structure du schéma avec le signe plus (`+`) sélectionné pour qu’un nouveau champ puisse être ajouté.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

Le nouveau champ apparaît dans votre schéma.

![Un nouveau champ ajouté au schéma.](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Ajouter des sous-champs au champ d’objet {#add-sub-fields-to-the-object-field}

La dernière étape de la préparation de votre schéma consiste à ajouter des champs individuels dans le champ que vous avez créé à l’étape précédente.

![Groupe de sous-champs ajoutés à un champ dans le schéma.](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Créer un flux de données

Une fois la configuration de votre schéma terminée, vous pouvez procéder à la création d’un flux de données pour vos données d’activité personnalisées.

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Applications Adobe], sélectionnez **[!UICONTROL Marketo Engage]**. Sélectionnez ensuite **[!UICONTROL Ajouter des données]** pour créer un flux de données [!DNL Marketo].

![Le catalogue des sources sur l’interface utilisateur d’Experience Platform avec la source Marketo Engage sélectionnée.](../../../../images/tutorials/create/marketo/catalog.png)

### Sélectionner les données

Sélectionnez **[!UICONTROL Activités]** dans la liste des jeux de données [!DNL Marketo], puis sélectionnez **[!UICONTROL Suivant]**.

![L’étape de sélection des données dans le workflow des sources avec le jeu de données des activités sélectionné.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Détails du flux de données

Ensuite, [fournissez des informations pour votre flux de données](./marketo.md#provide-dataflow-details), y compris les noms et descriptions de votre jeu de données et de votre flux de données, le schéma que vous utiliserez et les configurations pour l’ingestion [!DNL Profile], les diagnostics d’erreur et l’ingestion partielle.

![Étape Détails du flux de données.](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Mappage

Les mappages des champs d’activité standard sont automatiquement renseignés, mais les champs d’activité personnalisés doivent être mappés manuellement à leurs champs cibles correspondants.

Pour commencer à mapper vos champs d’activité personnalisés, sélectionnez **[!UICONTROL Nouveau type de champ]** puis **[!UICONTROL Ajouter un nouveau champ]**.

![L’étape de mappage avec le menu déroulant pour ajouter un nouveau champ.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Parcourez la structure des données sources et recherchez le champ d’activité personnalisé à ingérer. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Sélectionner]**.

>[!TIP]
>
>Pour éviter toute confusion et gérer les noms de champ en double, les champs d’activité personnalisés sont précédés du nom de l’API.

![La structure des données sources.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Pour ajouter un champ cible, sélectionnez l’icône de schéma ![icône de schéma](/help/images/icons/schema.png) puis sélectionnez les champs d’activité personnalisés dans le schéma cible.

![Structure du schéma cible.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Répétez les étapes pour ajouter le reste de vos champs de mappage d’activité personnalisés. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Tous les mappages pour les données source et cible.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Révision

L’écran de *[!UICONTROL Révision]* s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant de l’entité source choisie et le nombre de colonnes au sein de cette entité source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez révisé votre flux de données, sélectionnez **[!UICONTROL Enregistrer et ingérer]** et patientez quelques instants le temps que le flux de données soit créé.

![Étape de révision finale qui résume les informations sur les champs de connexion, de jeu de données et de mappage.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### Ajouter des activités personnalisées à un flux de données d’activités existant {#add-to-existing-dataflows}

Pour ajouter des données d’activité personnalisées à un flux de données existant, modifiez les mappages d’un flux de données d’activités existant avec les données d’activité personnalisées à ingérer. Vous pouvez ainsi ingérer une activité personnalisée dans le même jeu de données d’activités existant. Pour plus d’informations sur la mise à jour des mappages d’un flux de données existant, consultez le guide sur la [mise à jour des flux de données dans l’interface utilisateur](../../update-dataflows.md).

### Utilisation de [!DNL Query Service] pour filtrer les activités en fonction des activités personnalisées {#query-service-filter}

Une fois votre flux de données terminé, vous pouvez utiliser [Query Service](../../../../../query-service/home.md) pour filtrer les activités en fonction des données de vos activités personnalisées.

Lorsque des activités personnalisées sont ingérées dans Experience Platform, le nom d’API de l’activité personnalisée en devient automatiquement le `eventType`. Utilisez `eventType={API_NAME}` pour filtrer les données d’activité personnalisées.

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

Utilisez la clause `IN` pour filtrer plusieurs activités personnalisées :

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

L’image ci-dessous présente un exemple d’instruction SQL dans le [Query Editor](../../../../../query-service/ui/user-guide.md) qui filtre les données d’activité personnalisées.

![L’interface utilisateur d’Experience Platform affiche un exemple de requête pour les activités personnalisées.](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## Étapes suivantes

Ce tutoriel vous a permis de configurer un schéma Experience Platform pour [!DNL Marketo] des données d’activité personnalisées et de créer un flux de données pour importer ces données dans Experience Platform. Pour obtenir des informations générales sur la source de [!DNL Marketo], lisez la [[!DNL Marketo] présentation de la source](../../../../connectors/adobe-applications/marketo/marketo.md).
