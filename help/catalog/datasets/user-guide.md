---
keywords: Experience Platform;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: Guide d’utilisation des jeux de données
topic: datasets
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 74%

---


# Guide d’utilisation des jeux de données

Ce guide d’utilisation fournit des instructions permettant d’exécuter des actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur d’Adobe Experience Platform.

## Prise en main

Ce guide d’utilisation nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Jeu de données](overview.md) : la structure de stockage et de gestion pour la persistance des données dans [!DNL Experience Platform].
* [[ ! Système de modèle de données d’expérience (XDM) DNL]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Éditeur](../../xdm/tutorials/create-schema-ui.md)de schéma : Découvrez comment créer vos propres schémas XDM personnalisés à l’aide de la [!DNL Schema Editor] section dans l’ [!DNL Platform] interface utilisateur.
* [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[ !Gouvernance des données DNL]](../../data-governance/home.md): Veiller au respect des réglementations, restrictions et stratégies relatives à l’utilisation des données client.

## Affichage des jeux de données

In the [!DNL Experience Platform] UI, click **[!UICONTROL Datasets]** in the left-navigation to open the *[!UICONTROL Datasets]* dashboard. Le tableau de bord répertorie tous les jeux de données disponibles pour votre organisation. Des détails s’affichent pour chaque jeu de données répertorié, notamment son nom, le schéma auquel le jeu de données adhère et l’état de l’exécution d’ingestion la plus récente.

![](../images/datasets/user-guide/browse_datasets.png)

Cliquez sur le nom d’un jeu de données pour accéder à l’écran *[!UICONTROL Activité du jeu de données]* et consulter les détails du jeu de données que vous avez sélectionné. L’onglet activité contient un graphique qui permet de visualiser le taux de messages consommé ainsi qu’une liste des lots réussis et en échec.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Prévisualisation d’un jeu de données

À l’écran *[!UICONTROL Activité du jeu de données]*, cliquez sur **[!UICONTROL Prévisualiser le jeu de données]** près du coin supérieur droit de votre écran pour prévisualiser jusqu’à 100 lignes de données. Si le jeu de données est vide, le lien de prévisualisation sera désactivé et indiquera à la place **[!UICONTROL Prévisualisation non disponible]**.

![](../images/datasets/user-guide/click_to_preview.png)

Dans la fenêtre de prévisualisation, l’affichage hiérarchique du schéma pour le jeu de données s’affiche sur la droite.

![](../images/datasets/user-guide/preview_dataset.png)

For more robust methods to access your data, [!DNL Experience Platform] provides downstream services such as [!DNL Query Service] and [!DNL JupyterLab] to explore and analyze data. Consultez les documents suivants pour plus d’informations :

* [Présentation de Query Service](../../query-service/home.md)
* [Guide d’utilisation de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Création d’un jeu de données {#create}

Pour créer un nouveau jeu de données, commencez par cliquer sur **[!UICONTROL Créer un jeu de données]** dans le tableau de bord *[!UICONTROL Jeux de données]*.

![](../images/datasets/user-guide/click_to_create.png)

Sur l’écran suivant, les deux options de création d’un nouveau jeu de données suivantes vous sont proposées :

* [Créer un jeu de données à partir d’un schéma](#create-a-dataset-with-an-existing-schema)
* [Créer un jeu de données à partir d’un fichier CSV](#create-a-dataset-with-a-csv-file)

### Création d’un jeu de données à partir d’un schéma existant

Sur l’écran *[!UICONTROL Créer un jeu de données]*, cliquez sur **[!UICONTROL Créer un jeu de données à partir d’un schéma]** pour créer un nouveau jeu de données vide.

![](../images/datasets/user-guide/create_dataset_schema.png)

L’étape *[!UICONTROL Sélectionner un schéma]* apparaît. Parcourez la liste des schémas et sélectionnez le schéma auquel le jeu de données doit s’adapter avant de cliquer sur **[!UICONTROL Suivant]**.

![](../images/datasets/user-guide/select_schema.png)

L’étape *[!UICONTROL Configurer le jeu de données]* apparaît. Ajoutez un nom et une description facultative au jeu de données, puis cliquez sur **[!UICONTROL Terminer]** pour créer le jeu de données.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Création d’un jeu de données à partir d’un fichier CSV

Lorsque vous créez un jeu de données à l’aide d’un fichier CSV, un schéma ad hoc est créé pour fournir une structure au jeu de données qui correspond au fichier CSV fourni. Sur l’écran *[!UICONTROL Créer un jeu de données]*, cliquez sur la case intitulée **[!UICONTROL Créer un jeu de données à partir d’un fichier CSV]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

L’étape *[!UICONTROL Configurer]* apparaît. Ajoutez un nom et une description facultative au jeu de données, puis cliquez sur **[!UICONTROL Suivant]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

L’étape *[!UICONTROL Ajouter les données]* apparaît. Chargez le fichier CSV soit en le faisant glisser et en le déposant au centre de votre écran, soit en cliquant sur **[!UICONTROL Parcourir]** pour explorer votre répertoire de fichiers. La taille du fichier peut aller jusqu’à 10 gigaoctets. Une fois le fichier CSV chargé, cliquez sur **[!UICONTROL Enregistrer]** pour créer le jeu de données.

>[!NOTE]
>
>Les noms de colonne CSV doivent commencer par des caractères alphanumériques et ne peuvent contenir que des lettres, des chiffres et des traits de soulignement.

![](../images/datasets/user-guide/add_csv_data.png)

## Activation d’un jeu de données pour Real-time Customer Profile

Chaque jeu de données a la possibilité d’enrichir les profils clients des données qu’ils ingèrent. Pour ce faire, le schéma auquel le jeu de données adhère doit être compatible avec [!DNL Real-time Customer Profile]. Un schéma compatible répond aux critères suivants :

* Le schéma comporte au moins un attribut défini comme propriété d’identité.
* Le schéma comporte au moins une propriété d’identité définie comme identité principale.

For more information on enabling a schema for [!DNL Profile], see the [Schema Editor user guide](../../xdm/tutorials/create-schema-ui.md).

Pour activer un jeu de données dans Profile, accédez à son écran *[!UICONTROL Activité du jeu de données]* et cliquez sur le bouton de basculement **[!UICONTROL Profil]** au sein de la colonne *[!UICONTROL Propriétés]*. Une fois activées, les données ingérées dans le jeu de données seront également utilisées pour générer les profils clients.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

If a dataset already contains data and is then enabled for [!DNL Profile], the existing data is not consumed by [!DNL Profile]. After a dataset is enabled for [!DNL Profile], it is recommended that you re-ingest any existing data to have them populate customer profiles.

## Gestion et application de la gouvernance des données sur un jeu de données

Data Usage Labeling and Enforcement (DULE) is the core data governance mechanism for [!DNL Experience Platform]. Les libellés DULE vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Pour en savoir plus sur les libellés, consultez la [Présentation de la gouvernance des données](../../data-governance/home.md) ou reportez-vous au [guide d’utilisation des libellés d’utilisation des données](../../data-governance/labels/overview.md) pour savoir comment appliquer des libellés à vos jeux de données.

## Suppression d’un jeu de données

Vous pouvez supprimer un jeu de données en accédant d’abord à son écran *[!UICONTROL Activité du jeu de données]*. Cliquez ensuite sur **[!UICONTROL Supprimer un jeu de données]** pour le supprimer.

>[!NOTE]
>
>Datasets created and utilized by Adobe applications and services (such as Adobe Analytics, Adobe Audience Manager, or [!DNL Decisioning Service]) cannot be deleted.

![](../images/datasets/user-guide/delete_dataset.png)

Une boîte de confirmation s’affiche alors. Cliquez sur **[!UICONTROL Supprimer]** pour confirmer la suppression du jeu de données.

![](../images/datasets/user-guide/confirm_delete.png)

## Suppression d’un jeu de données activé par Profile

If a dataset is enabled for [!DNL Profile], deleting it through the UI disables the dataset for ingestion, but does not automatically delete the dataset in the backend. Pour supprimer complètement le jeu de données ainsi que les données de profil et d’identité qu’il fournit, vous devez effectuer une requête de suppression supplémentaire. For steps on how to properly delete data from the [!DNL Profile] store, see the [!DNL Real-time Customer Profile] API [sub-guide on profile system jobs, also known as &quot;delete requests&quot;](../../profile/api/profile-system-jobs.md).

## Surveillance de l’ingestion des données

In the [!DNL Experience Platform] UI, click **[!UICONTROL Monitoring]** in the left-navigation. Le tableau de bord *[!UICONTROL Surveillance]* vous permet de consulter les états des données entrantes soit depuis le lot soit depuis l’ingestion par flux. Pour afficher les états de lots individuels, cliquez sur *[!UICONTROL Lot de bout en bout]* ou sur *[!UICONTROL Diffusion en continu de bout en bout]*. Le tableau de bord répertorie toutes les exécutions de lot ou d’ingestion par flux, notamment celles réussies, en échec ou toujours en cours. Chaque liste fournit des détails sur le lot, notamment l’identifiant de lot, le nom du jeu de données cibles et le nombre d’enregistrements ingérés. If the target dataset is enabled for [!DNL Profile], the number of ingested identity and profile records is also displayed.

![](../images/datasets/user-guide/batch_listing.png)

Vous pouvez cliquer sur un **[!UICONTROL identifiant de lot]** individuel pour accéder au tableau de bord *[!UICONTROL Présentation du lot]* et afficher les détails pour le lot et notamment les journaux d’erreurs dans le cas de l’échec de l’ingestion du lot.

![](../images/datasets/user-guide/batch_overview.png)

Si vous souhaitez supprimer le lot, vous pouvez le faire en cliquant sur **[!UICONTROL Supprimer le lot]** situé près du coin supérieur droit du tableau de bord. Cette opération supprimera également les enregistrements du jeu de données pour lequel le lot a été ingéré à l’origine.

![](../images/datasets/user-guide/delete_batch.png)

## Étapes suivantes

This user guide provided instructions for performing common actions when working with datasets in the [!DNL Experience Platform] user interface. For steps on performing common [!DNL Platform] workflows involving datasets, please refer to the following tutorials:

* [Création d’un jeu de données à l’aide d’API](create.md)
* [Interrogation des données d’un jeu de données à l’aide de l’API Data Access](../../data-access/home.md)
* [Configuration d’un jeu de données pour Real-time Customer Profile et Identity Service à l’aide des API](../../profile/tutorials/dataset-configuration.md)