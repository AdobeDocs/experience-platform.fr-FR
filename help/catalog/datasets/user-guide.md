---
keywords: Experience Platform;accueil;rubriques les plus consultées;activer le jeu de données;jeu de données;jeu de données
solution: Experience Platform
title: Guide de l’interface utilisateur des jeux de données
topic-legacy: datasets
description: Découvrez comment exécuter des actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur de Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 72%

---

# Guide de l’interface utilisateur des jeux de données

Ce guide d’utilisation fournit des instructions permettant d’exécuter des actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur d’Adobe Experience Platform.

## Prise en main

Ce guide d’utilisation nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Jeu de données](overview.md) : la structure de stockage et de gestion pour la persistance des données dans [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   * [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Éditeur](../../xdm/tutorials/create-schema-ui.md) de schéma : Découvrez comment créer vos propres schémas XDM personnalisés à l’aide du  [!DNL Schema Editor] dans l’interface  [!DNL Platform] utilisateur.
* [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Veillez à la conformité aux réglementations, aux restrictions et aux politiques concernant l’utilisation des données clients.

## Affichage des jeux de données

Dans l’interface utilisateur [!DNL Experience Platform], cliquez sur **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche pour ouvrir le tableau de bord **[!UICONTROL Jeux de données]**. Le tableau de bord répertorie tous les jeux de données disponibles pour votre organisation. Des détails s’affichent pour chaque jeu de données répertorié, notamment son nom, le schéma auquel le jeu de données adhère et l’état de l’exécution d’ingestion la plus récente.

![](../images/datasets/user-guide/browse-datasets.png)

Cliquez sur le nom d’un jeu de données pour accéder à l’écran **[!UICONTROL Activité du jeu de données]** et consulter les détails du jeu de données que vous avez sélectionné. L’onglet activité contient un graphique qui permet de visualiser le taux de messages consommé ainsi qu’une liste des lots réussis et en échec.

![](../images/datasets/user-guide/dataset-activity-1.png)
![](../images/datasets/user-guide/dataset-activity-2.png)

## Prévisualisation d’un jeu de données

À l’écran **[!UICONTROL Activité du jeu de données]**, cliquez sur **[!UICONTROL Prévisualiser le jeu de données]** près du coin supérieur droit de votre écran pour prévisualiser jusqu’à 100 lignes de données. Si le jeu de données est vide, le lien de prévisualisation est désactivé et indique à la place que l’aperçu n’est pas disponible.

![](../images/datasets/user-guide/click-to-preview.png)

Dans la fenêtre de prévisualisation, l’affichage hiérarchique du schéma pour le jeu de données s’affiche sur la droite.

![](../images/datasets/user-guide/preview-dataset.png)

Pour des méthodes plus robustes d’accès à vos données, [!DNL Experience Platform] fournit des services en aval tels que [!DNL Query Service] et [!DNL JupyterLab] pour explorer et analyser les données. Consultez les documents suivants pour plus d’informations :

* [Présentation de Query Service](../../query-service/home.md)
* [Guide d’utilisation de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Création d’un jeu de données {#create}

Pour créer un nouveau jeu de données, commencez par cliquer sur **[!UICONTROL Créer un jeu de données]** dans le tableau de bord **[!UICONTROL Jeux de données]**.

![](../images/datasets/user-guide/click-to-create.png)

Sur l’écran suivant, les deux options de création d’un nouveau jeu de données suivantes vous sont proposées :

* [Créer un jeu de données à partir d’un schéma](#schema)
* [Créer un jeu de données à partir d’un fichier CSV](#csv)

### Création d’un jeu de données à partir d’un schéma existant {#schema}

Sur l’écran **[!UICONTROL Créer un jeu de données]**, cliquez sur **[!UICONTROL Créer un jeu de données à partir d’un schéma]** pour créer un nouveau jeu de données vide.

![](../images/datasets/user-guide/create-dataset-schema.png)

L’étape **[!UICONTROL Sélectionner un schéma]** apparaît. Parcourez la liste des schémas et sélectionnez le schéma auquel le jeu de données doit s’adapter avant de cliquer sur **[!UICONTROL Suivant]**.

![](../images/datasets/user-guide/select-schema.png)

L’étape **[!UICONTROL Configurer le jeu de données]** apparaît. Ajoutez un nom et une description facultative au jeu de données, puis cliquez sur **[!UICONTROL Terminer]** pour créer le jeu de données.

![](../images/datasets/user-guide/configure-dataset-schema.png)

### Création d’un jeu de données à partir d’un fichier CSV {#csv}

Lorsque vous créez un jeu de données à l’aide d’un fichier CSV, un schéma ad hoc est créé pour fournir une structure au jeu de données qui correspond au fichier CSV fourni. Sur l’écran **[!UICONTROL Créer un jeu de données]**, cliquez sur la case intitulée **[!UICONTROL Créer un jeu de données à partir d’un fichier CSV]**.

![](../images/datasets/user-guide/create-dataset-csv.png)

L’étape **[!UICONTROL Configurer]** apparaît. Ajoutez un nom et une description facultative au jeu de données, puis cliquez sur **[!UICONTROL Suivant]**.

![](../images/datasets/user-guide/configure-dataset-csv.png)

L’étape **[!UICONTROL Ajouter les données]** apparaît. Chargez le fichier CSV soit en le faisant glisser et en le déposant au centre de votre écran, soit en cliquant sur **[!UICONTROL Parcourir]** pour explorer votre répertoire de fichiers. La taille du fichier peut aller jusqu’à 10 gigaoctets. Une fois le fichier CSV chargé, cliquez sur **[!UICONTROL Enregistrer]** pour créer le jeu de données.

>[!NOTE]
>
>Les noms de colonne CSV doivent commencer par des caractères alphanumériques et ne peuvent contenir que des lettres, des chiffres et des traits de soulignement.

![](../images/datasets/user-guide/add-csv-data.png)

## Activation d’un jeu de données pour Real-time Customer Profile {#enable-profile}

Chaque jeu de données a la possibilité d’enrichir les profils clients des données qu’ils ingèrent. Pour ce faire, le schéma auquel le jeu de données adhère doit être compatible avec [!DNL Real-time Customer Profile]. Un schéma compatible répond aux critères suivants :

* Le schéma comporte au moins un attribut défini comme propriété d’identité.
* Le schéma comporte au moins une propriété d’identité définie comme identité principale.

Pour plus d’informations sur l’activation d’un schéma pour [!DNL Profile], consultez le [guide d’utilisation de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).

Pour activer un jeu de données dans Profile, accédez à son écran **[!UICONTROL Activité du jeu de données]** et cliquez sur le bouton de basculement **[!UICONTROL Profil]** au sein de la colonne **[!UICONTROL Propriétés]**. Une fois activées, les données ingérées dans le jeu de données seront également utilisées pour générer les profils clients.

>[!NOTE]
>
>Si un jeu de données contient déjà des données et est activé pour [!DNL Profile], les données existantes ne sont pas automatiquement utilisées par [!DNL Profile]. Une fois qu’un jeu de données est activé pour [!DNL Profile], il est recommandé d’ingérer à nouveau toutes les données existantes pour qu’elles contribuent aux profils client.

![](../images/datasets/user-guide/enable-dataset-profiles.png)

## Gestion et application de la gouvernance des données sur un jeu de données

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Pour en savoir plus sur les libellés, consultez la [Présentation de la gouvernance des données](../../data-governance/home.md) ou reportez-vous au [guide d’utilisation des libellés d’utilisation des données](../../data-governance/labels/overview.md) pour savoir comment appliquer des libellés à vos jeux de données.

## Suppression d’un jeu de données

Vous pouvez supprimer un jeu de données en accédant d’abord à son écran **[!UICONTROL Activité du jeu de données]**. Cliquez ensuite sur **[!UICONTROL Supprimer un jeu de données]** pour le supprimer.

>[!NOTE]
>
>Les jeux de données créés et utilisés par les applications et services Adobe (tels qu’Adobe Analytics, Adobe Audience Manager ou [!DNL Offer Decisioning]) ne peuvent pas être supprimés.

![](../images/datasets/user-guide/delete-dataset.png)

Une boîte de confirmation s’affiche alors. Cliquez sur **[!UICONTROL Supprimer]** pour confirmer la suppression du jeu de données.

![](../images/datasets/user-guide/confirm-delete.png)

## Suppression d’un jeu de données activé par Profile

Si un jeu de données est activé pour [!DNL Profile], la suppression de ce jeu de données via l’interface utilisateur le supprime à la fois du lac de données et de la banque de profils dans Platform.

Vous pouvez supprimer un jeu de données du magasin [!DNL Profile] uniquement (en laissant les données dans le lac de données) à l’aide de l’API Real-time Customer Profile. Pour plus d’informations, consultez le [guide relatif au point d’entrée de l’API du système de profils](../../profile/api/profile-system-jobs.md).

## Surveillance de l’ingestion des données

Dans l’interface utilisateur [!DNL Experience Platform], cliquez sur **[!UICONTROL Surveillance]** dans le volet de navigation de gauche. Le tableau de bord **[!UICONTROL Surveillance]** vous permet de consulter les états des données entrantes soit depuis le lot soit depuis l’ingestion par flux. Pour afficher les états de lots individuels, cliquez sur **[!UICONTROL Lot de bout en bout]** ou sur **[!UICONTROL Diffusion en continu de bout en bout]**. Les tableaux de bord répertorient toutes les exécutions d’ingestion par lots ou par flux, y compris celles qui ont réussi, échoué ou qui sont toujours en cours. Chaque liste fournit des détails sur le lot, notamment l’identifiant de lot, le nom du jeu de données cibles et le nombre d’enregistrements ingérés. Si le jeu de données cible est activé pour [!DNL Profile], le nombre d’identités ingérées et d’enregistrements de profil s’affiche également.

![](../images/datasets/user-guide/batch-listing.png)

Vous pouvez cliquer sur un **[!UICONTROL identifiant de lot]** individuel pour accéder au tableau de bord **[!UICONTROL Présentation du lot]** et afficher les détails pour le lot et notamment les journaux d’erreurs dans le cas de l’échec de l’ingestion du lot.

![](../images/datasets/user-guide/batch-overview.png)

Si vous souhaitez supprimer le lot, vous pouvez le faire en cliquant sur **[!UICONTROL Supprimer le lot]** situé près du coin supérieur droit du tableau de bord. Cette opération supprimera également les enregistrements du jeu de données pour lequel le lot a été ingéré à l’origine.

![](../images/datasets/user-guide/delete-batch.png)

## Étapes suivantes

Ce guide d’utilisation a fourni des instructions pour exécuter des actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur de [!DNL Experience Platform]. Pour obtenir des instructions sur l’exécution de processus [!DNL Platform] courants impliquant des jeux de données, reportez-vous aux tutoriels suivants :

* [Création d’un jeu de données à l’aide d’API](create.md)
* [Interrogation des données d’un jeu de données à l’aide de l’API Data Access](../../data-access/home.md)
* [Configuration d’un jeu de données pour Real-time Customer Profile et Identity Service à l’aide des API](../../profile/tutorials/dataset-configuration.md)
