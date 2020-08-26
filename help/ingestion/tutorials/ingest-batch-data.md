---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ingestion de données dans Adobe Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 70%

---


# Ingestion de données dans Adobe Experience Platform

Adobe Experience Platform allows you to easily import data into [!DNL Platform] as batch files. Examples of data to be ingested may include profile data from a flat file in a CRM system (such as a parquet file) or data that conforms to a known [!DNL Experience Data Model] (XDM) schema in the Schema Registry.

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.

Si vous préférez ingérer des données à l’aide des API Data Ingestion, lisez d’abord le [guide de développement de l’ingestion par lots](../batch-ingestion/api-overview.md).

## Espace de travail des jeux de données

The Datasets workspace within [!DNL Experience Platform] allows you to view and manage all of the datasets that your IMS organization has made, as well as create new ones.

Affichez l’espace de travail des jeux de données en cliquant sur **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche. L’espace de travail des jeux de données contient une liste de jeux de données, y compris des colonnes indiquant le _[!UICONTROL nom]_, la date et l’heure de _[!UICONTROL création]_, la _[!UICONTROL source]_, le _[!UICONTROL schéma]_ et l’_[!UICONTROL état du dernier lot]_, ainsi que la date et l’heure de la _[!UICONTROL dernière mise à jour]_ du jeu de données.

>[!NOTE]
>
>Cliquez sur l’icône de filtre en regard de la barre de recherche pour utiliser les fonctionnalités de filtrage afin de n’afficher que les jeux de données activés pour [!DNL Profile].

![Affichage de tous les jeux de données](../images/tutorials/ingest-batch-data/datasets_workspace.png)

## Création d’un jeu de données

Pour créer un jeu de données, cliquez sur **[!UICONTROL Créer un jeu de données]** dans le coin supérieur droit de l’espace de travail des jeux de données.

On the **[!UICONTROL Create Dataset]** screen, select whether you would like to &quot;[!UICONTROL Create Dataset from Schema]&quot; or &quot;[!UICONTROL Create Dataset from CSV File]&quot;.

Dans ce tutoriel, un schéma sera utilisé pour créer le jeu de données. Cliquez sur **[!UICONTROL Créer un jeu de données à partir d’un schéma]** pour continuer.

![Sélectionner la source de données](../images/tutorials/ingest-batch-data/create_dataset.png)

## Sélectionner le schéma d’un jeu de données

Dans l’écran **[!UICONTROL Sélectionner un schéma]**, choisissez un schéma en cliquant sur la case d’option située à côté du schéma que vous souhaitez utiliser. Pour ce tutoriel, le jeu de données sera créé à l’aide du schéma Loyalty Members. L’utilisation de la barre de recherche pour filtrer les schémas est un moyen utile de trouver le schéma exact dont vous avez besoin.

Une fois que vous avez sélectionné la case d’option en regard du schéma que vous souhaitez utiliser, cliquez sur **[!UICONTROL Suivant]**.

![Sélectionner un schéma](../images/tutorials/ingest-batch-data/select_schema.png)

## Configuration d’un jeu de données

Dans l’écran **[!UICONTROL Configurer le jeu de données]**, vous devrez attribuer un **[!UICONTROL nom]** à votre jeu de données et pourrez également fournir une **[!UICONTROL description]** pour celui-ci.

**Remarques sur les noms des jeux de données :**

- Les noms des jeux de données doivent être courts et descriptifs afin qu’ils puissent être facilement retrouvés par la suite dans la bibliothèque.
- Les noms des jeux de données doivent être uniques, ce qui signifie qu’ils doivent également être suffisamment précis pour ne pas être réutilisés à l’avenir.
- Il est recommandé de fournir des informations supplémentaires sur le jeu de données à l’aide du champ de description, car cela peut aider d’autres utilisateurs à différencier les jeux de données à l’avenir.

Une fois que le jeu de données possède un nom et une description, cliquez sur **[!UICONTROL Terminer]**.

![Configurer un jeu de données](../images/tutorials/ingest-batch-data/configure_dataset.png)

## Activité du jeu de données

Un jeu de données vide a désormais été créé et vous avez été renvoyé à l’onglet **[!UICONTROL Activité du jeu de données]** dans l’espace de travail des jeux de données. Vous devriez voir le nom du jeu de données dans le coin supérieur gauche de l’espace de travail, ainsi qu’une notification indiquant « Aucun lot n’a été ajouté ». Cela est normal puisque vous n’avez encore ajouté aucun lot à ce jeu de données.

Sur le côté droit de l’espace de travail des jeux de données, l’onglet **[!UICONTROL Informations]** contient des informations relatives à votre nouveau jeu de données, telles que l’_[!UICONTROL identifiant du jeu de données]_, le _[!UICONTROL nom]_, la _[!UICONTROL description]_, le _[!UICONTROL nom du tableau]_, le _[!UICONTROL schéma]_, le _[!UICONTROL Streaming]_ et la _[!UICONTROL Source]_. L’onglet Informations contient également la date de _[!UICONTROL création]_ du jeu de données et celle de sa _[!UICONTROL dernière modification]_.

L’onglet Informations contient également un bouton activer/désactiver de _[!UICONTROL Profile]_ qui permet d’activer votre jeu de données pour l’utiliser avec [!DNL Real-time Customer Profile]. Use of this toggle, and [!DNL Real-time Customer Profile], will be explained in more detail in the section that follows.

![Activité du jeu de données](../images/tutorials/ingest-batch-data/dataset_activity.png)

## Activer le jeu de données pour [!DNL Real-time Customer Profile]

Datasets are used for ingesting data into [!DNL Experience Platform], and that data is ultimately used to identify individuals and stitch together information coming from multiple sources. Cette information collée ensemble s&#39;appelle un [!DNL Real-Time Customer Profile]. In order for [!DNL Platform] to know which information should be included in the [!DNL Real-Time Profile], datasets can be marked for inclusion using the **[!UICONTROL Profile]** toggle.

Par défaut, ce bouton est désactivé. If you choose to toggle on [!DNL Profile], all data ingested into the dataset will be used to help identify an individual and stitch together their [!DNL Real-Time Profile].

To learn more about [!DNL Real-time Customer Profile] and working with identities, please review the [Identity Service](../../identity-service/home.md) documentation.

To enable the dataset for [!DNL Real-time Customer Profile], click the **[!UICONTROL Profile]** toggle in the **[!UICONTROL Info]** tab.

![Bascule des profils](../images/tutorials/ingest-batch-data/enable_dataset_unified_profile.png)

Une boîte de dialogue s’affiche vous demandant de confirmer que vous souhaitez activer le jeu de données pour [!DNL Real-time Customer Profile].

![Boîte de dialogue d’activation de Profile](../images/tutorials/ingest-batch-data/confirm_dataset_enable.png)

Cliquez sur **[!UICONTROL Activer]** et le bouton activer/désactiver devient bleu, indiquant qu’il est activé.

![Activé pour Profile](../images/tutorials/ingest-batch-data/dataset_enabled.png)

## Ajout de données à un jeu de données

Les données peuvent être ajoutées à un jeu de données de différentes manières. You could choose to use [!DNL Data Ingestion] APIs or an ETL partner such as [!DNL Unifi] or [!DNL Informatica]. Dans ce tutoriel, les données seront ajoutées au jeu de données à l’aide de l’onglet **[!UICONTROL Ajouter des données]** dans l’interface utilisateur.

Pour commencer à ajouter des données au jeu de données, cliquez sur l’onglet **[!UICONTROL Ajouter des données]**. Vous pouvez désormais faire glisser et déposer des fichiers ou rechercher sur votre ordinateur les fichiers à ajouter.

>[!NOTE]
>
>Platform prend en charge deux types de fichiers pour l’ingestion de données : parquet ou JSON. Vous pouvez ajouter jusqu’à cinq fichiers à la fois, la taille maximale de chaque fichier étant de 10 Go.

![Ajouter un onglet de données](../images/tutorials/ingest-batch-data/add_data.png)

## Chargement d’un fichier

Once you drag and drop (or browse and select) a parquet or JSON file that you wish to upload, [!DNL Platform] will immediately begin to process the file and an **[!UICONTROL Uploading]** dialog will appear on the **[!UICONTROL Add Data]** tab showing the progress of your file upload.

![Boîte de dialogue de chargement](../images/tutorials/ingest-batch-data/uploading.png)

## Mesures de jeux de données

Une fois le chargement du fichier terminé, l’onglet **[!UICONTROL Activité du jeu de données]** n’indique plus qu’« aucun lot n’a été ajouté ». Instead, the *[!UICONTROL Dataset Activity]* tab now shows dataset metrics. Toutes les mesures indiqueront « 0 » à cette étape, car le lot n’a pas encore été chargé.

En bas de l’onglet se trouve une liste présentant l’_[!UICONTROL identifiant du lot]_ des données qui venaient d’être ingérées via le processus [« Ajouter des données à un jeu de données »](#add-data-to-dataset). Sont également incluses les informations relatives au lot, notamment la date _[!UICONTROL d’ingestion]_, le nombre d’_[!UICONTROL enregistrements ingérés]_ et l’_[!UICONTROL état]_ actuel du lot.

![Mesures de jeux de données](../images/tutorials/ingest-batch-data/batch_loading.png)

## Détails du lot

Cliquez sur l’_[!UICONTROL identifiant du lot]_ pour afficher un **[!UICONTROL aperçu du lot]**, indiquant des détails supplémentaires sur le lot. Une fois le chargement du lot terminé, les informations sur le lot sont mises à jour afin d’afficher le nombre d’ _[!UICONTROL enregistrements ingérés]_ et la _[!UICONTROL taille du fichier]_. L’_[!UICONTROL état]_ passe également à « Succès » ou « Échec ». Si le lot échoue, la section _[!UICONTROL Code d’erreur]_ contiendra des informations détaillées sur les erreurs survenues lors de l’ingestion.

Pour plus d’informations et pour obtenir des questions fréquentes sur l’ingestion par lots, consultez le [guide de dépannage de l’ingestion par lots](../batch-ingestion/troubleshooting.md).

Pour revenir à l’écran **[!UICONTROL Activité du jeu de données]**, cliquez sur le nom du jeu de données (_[!UICONTROL Loyalty Details]_) dans le chemin de navigation.

![Aperçu du lot](../images/tutorials/ingest-batch-data/batch_overview.png)

## Prévisualisation d’un jeu de données

Une fois que le jeu de données est prêt, une option **[!UICONTROL Prévisualisation du jeu de données]** s’affiche en haut de l’onglet **[!UICONTROL Activité du jeu de données]**.

Cliquez sur **[!UICONTROL Prévisualisation du jeu de données]** pour ouvrir une boîte de dialogue présentant les données d’exemple du jeu de données. Si le jeu de données a été créé à l’aide d’un schéma, les informations concernant le schéma du jeu de données s’affichent sur le côté gauche de la prévisualisation. Vous pouvez développer le schéma à l’aide des flèches pour voir la structure du schéma. Chaque en-tête de colonne dans la prévisualisation des données représente un champ dans le jeu de données.

![Informations sur le jeu de données](../images/tutorials/ingest-batch-data/dataset_details.png)

## Étapes suivantes et ressources supplémentaires

Now that you have created a dataset and successfully ingested data into [!DNL Experience Platform], you can repeat these steps to create a new dataset or ingest more data into the existing dataset.

Pour en savoir plus sur l&#39;assimilation par lots, veuillez lire l&#39;aperçu [](../batch-ingestion/overview.md) de l&#39;assimilation par lots et compléter votre apprentissage en regardant la vidéo ci-dessous.

>[!WARNING]
>
> L’ [!DNL Platform] interface utilisateur affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation ci-dessus pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
