---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion;ingérer des données par lot;tutoriel;ingestion par lots;tutoriel;guide de l’interface utilisateur;
solution: Experience Platform
title: Ingestion De Données Dans Experience Platform
type: Tutorial
description: Adobe Experience Platform vous permet d’importer facilement des données sous la forme de fichiers de lots, sous la forme de fichiers parquet ou de données conformes à un schéma de modèle de données d’expérience (XDM) connu.
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
TQID: https://experienceleague.adobe.com/PDftlpFl4BsPvOinOjBjdXF5hKRpRrXwh9TywjLzCcc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1268
ht-degree: 30%

---

# Ingestion de données dans Adobe Experience Platform

Adobe Experience Platform vous permet d’importer facilement des données dans [!DNL Experience Platform] sous forme de fichiers de lots. Parmi les exemples de données à ingérer, citons notamment les données de profil d’un fichier plat dans un système CRM (un fichier Parquet, par exemple) ou les données conformes à un schéma [!DNL Experience Data Model] (XDM) connu dans le registre des schémas.

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n’avez pas accès à une organisation dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.

Si vous préférez ingérer des données à l’aide des API Data Ingestion, lisez d’abord le [guide de développement de l’ingestion par lots](../batch-ingestion/api-overview.md).

## Espace de travail des jeux de données

L’espace de travail Jeux de données dans [!DNL Experience Platform] vous permet d’afficher et de gérer tous les jeux de données créés par votre organisation et d’en créer.

Affichez l’espace de travail Jeux de données en cliquant sur **[!UICONTROL Datasets]** dans le volet de navigation de gauche. L’espace de travail Jeux de données contient une liste de jeux de données, y compris des colonnes indiquant le nom, la date et l’heure de création, la source, le schéma et le statut du dernier lot, ainsi que la date et l’heure de la dernière mise à jour du jeu de données.

>[!NOTE]
>
>Cliquez sur l’icône de filtre à côté de la barre de recherche pour utiliser les fonctionnalités de filtrage afin d’afficher uniquement les jeux de données activés pour la [!DNL Profile].

![Affichage de tous les jeux de données](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Créer un jeu de données

Pour créer un jeu de données, cliquez sur **[!UICONTROL Create Dataset]** dans le coin supérieur droit de l’espace de travail Jeux de données .

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Sur l’écran **[!UICONTROL Create Dataset]**, choisissez si vous souhaitez afficher « [!UICONTROL Create Dataset from Schema] » ou « [!UICONTROL Create Dataset from CSV File] ».

Dans ce tutoriel, un schéma sera utilisé pour créer le jeu de données. Cliquez sur **[!UICONTROL Create Dataset from Schema]** pour continuer.

![Sélectionner la source de données](../images/tutorials/ingest-batch-data/create-dataset.png)

## Sélectionner le schéma d’un jeu de données

Sur l’écran **[!UICONTROL Select Schema]**, choisissez un schéma en cliquant sur le bouton radio en regard du schéma que vous souhaitez utiliser. Pour ce tutoriel, le jeu de données sera créé à l’aide du schéma Loyalty Members. L’utilisation de la barre de recherche pour filtrer les schémas est un moyen utile de trouver le schéma exact dont vous avez besoin.

Une fois que vous avez sélectionné le bouton radio en regard du schéma que vous souhaitez utiliser, cliquez sur **[!UICONTROL Next]**.

![Sélectionner un schéma](../images/tutorials/ingest-batch-data/select-schema.png)

## Configuration d’un jeu de données

Sur l’écran **[!UICONTROL Configure Dataset]**, vous devrez donner un nom à votre jeu de données et peut également fournir une description du jeu de données.

**Remarques sur les noms des jeux de données :**

- Les noms des jeux de données doivent être courts et descriptifs afin qu’ils puissent être facilement retrouvés par la suite dans la bibliothèque.
- Les noms des jeux de données doivent être uniques, ce qui signifie qu’ils doivent également être suffisamment précis pour ne pas être réutilisés à l’avenir.
- Il est recommandé de fournir des informations supplémentaires sur le jeu de données à l’aide du champ de description, car cela peut aider d’autres utilisateurs à différencier les jeux de données à l’avenir.

Une fois que le jeu de données a un nom et une description, cliquez sur **[!UICONTROL Finish]**.

![Configurer un jeu de données](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Activité du jeu de données

Un jeu de données vide a été créé et vous êtes revenu à l’onglet **[!UICONTROL Dataset Activity]** dans l’espace de travail Jeux de données . Vous devriez voir le nom du jeu de données dans le coin supérieur gauche de l’espace de travail, ainsi qu’une notification indiquant « Aucun lot n’a été ajouté ». Cela est normal puisque vous n’avez encore ajouté aucun lot à ce jeu de données.

Sur le côté droit de l’espace de travail Jeux de données , vous verrez l’onglet **[!UICONTROL Info]** contenant des informations relatives à votre nouveau jeu de données, telles que l’identifiant du jeu de données, le nom, la description, le nom de la table, le schéma, la diffusion en continu et la source. L’onglet Infos contient également des informations sur la date de création du jeu de données et sa date de dernière modification.

L’onglet Infos contient également un bouton **[!UICONTROL Profile]** qui est utilisé pour activer votre jeu de données à utiliser avec [!DNL Real-Time Customer Profile]. L’utilisation de ce bouton (bascule) et de ce [!DNL Real-Time Customer Profile] sera expliquée en détail dans la section qui suit.

![Activité du jeu de données](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Activer le jeu de données pour [!DNL Real-Time Customer Profile] {#enable-for-profile}

Les jeux de données sont utilisés pour ingérer des données dans [!DNL Experience Platform], et ces données sont finalement utilisées pour identifier des individus et rassembler des informations provenant de plusieurs sources. Cette information regroupée s&#39;appelle un [!DNL Real-Time Customer Profile]. Pour que les [!DNL Experience Platform] sachent quelles informations doivent être incluses dans le [!DNL Real-Time Profile], les jeux de données peuvent être marqués pour inclusion à l’aide du bouton **[!UICONTROL Profile]** .

Par défaut, ce bouton est désactivé. Si vous choisissez d’activer [!DNL Profile], toutes les données ingérées dans le jeu de données seront utilisées pour aider à identifier un individu et à rassembler ses [!DNL Real-Time Profile].

Pour en savoir plus sur l’[!DNL Real-Time Customer Profile] et l’utilisation des identités, consultez la documentation du [Service d’identités](../../identity-service/home.md).

Pour activer le jeu de données pour [!DNL Real-Time Customer Profile], cliquez sur le bouton **[!UICONTROL Profile]** dans l’onglet **[!UICONTROL Info]** .

![Bascule des profils](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Une boîte de dialogue s’affiche vous demandant de confirmer que vous souhaitez activer le jeu de données pour [!DNL Real-Time Customer Profile].

![Boîte de dialogue d’activation de Profile](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Cliquez sur **[!UICONTROL Enable]** et le bouton bascule devient bleu, ce qui indique qu’il est activé.

![Activé pour Profile](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Ajout de données à un jeu de données

Les données peuvent être ajoutées à un jeu de données de différentes manières. Vous pouvez choisir d’utiliser des API [!DNL Data Ingestion] ou un partenaire ETL tel que [!DNL Unifi] ou [!DNL Informatica]. Pour ce tutoriel, les données seront ajoutées au jeu de données à l’aide de l’onglet **[!UICONTROL Add Data]** dans l’interface utilisateur.

Pour commencer à ajouter des données au jeu de données, cliquez sur l’onglet **[!UICONTROL Add Data]** . Vous pouvez désormais faire glisser et déposer des fichiers ou rechercher sur votre ordinateur les fichiers à ajouter.

>[!NOTE]
>
>Experience Platform prend en charge deux types de fichiers pour l’ingestion de données : Parquet ou JSON. Vous pouvez ajouter jusqu’à cinq fichiers à la fois, la taille maximale de chaque fichier étant de 1 Go.

![Ajouter un onglet de données](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Chargement d’un fichier {#upload-file}

Une fois que vous avez effectué un glisser-déposer (ou que vous avez recherché et sélectionné) d’un fichier Parquet ou JSON que vous souhaitez charger, [!DNL Experience Platform] commencez immédiatement à traiter le fichier et une boîte de dialogue de **[!UICONTROL Uploading]** s’affiche sur l’onglet **[!UICONTROL Add Data]** pour indiquer la progression du chargement de votre fichier.

![Boîte de dialogue de chargement](../images/tutorials/ingest-batch-data/uploading-file.png)

## Mesures de jeux de données

Une fois le chargement du fichier terminé, l’onglet **[!UICONTROL Dataset Activity]** n’indique plus qu’« Aucun lot n’a été ajouté ». Au lieu de cela, l’onglet **[!UICONTROL Dataset Activity]** affiche désormais les mesures du jeu de données. Toutes les mesures indiqueront « 0 » à cette étape, car le lot n’a pas encore été chargé.

Au bas de l’onglet se trouve une liste affichant la **[!UICONTROL Batch ID]** des données qui viennent d’être ingérées par le processus [« Ajouter des données au jeu de données »](#add-data-to-dataset). Vous y trouverez également des informations relatives au lot, notamment la date d’ingestion, le nombre d’enregistrements ingérés et l’état actuel du lot.

![Mesures de jeux de données](../images/tutorials/ingest-batch-data/batch-id.png)

## Détails du lot

Cliquez sur le **[!UICONTROL Batch ID]** pour afficher un **[!UICONTROL Batch Overview]** affichant des détails supplémentaires sur le lot. Une fois le chargement du lot terminé, les informations relatives au lot sont mises à jour pour afficher le nombre d’enregistrements ingérés et la taille de fichier. Le statut passe également sur « Succès » ou « Échec ». Si le lot échoue, la section **[!UICONTROL Error Code]** contient des détails sur les erreurs survenues lors de l’ingestion.

Pour plus d’informations et pour obtenir des questions fréquentes sur l’ingestion par lots, consultez le [guide de dépannage de l’ingestion par lots](../batch-ingestion/troubleshooting.md).

Pour revenir à l’écran de **[!UICONTROL Dataset Activity]**, cliquez sur le nom du jeu de données (**[!UICONTROL Loyalty Details]**) dans le chemin de navigation.

![Aperçu du lot](../images/tutorials/ingest-batch-data/batch-details.png)

## Prévisualisation d’un jeu de données

Une fois que le jeu de données est prêt, une option à **[!UICONTROL Preview Dataset]** s’affiche en haut de l’onglet **[!UICONTROL Dataset Activity]** .

Cliquez sur **[!UICONTROL Preview Dataset]** pour ouvrir une boîte de dialogue affichant des exemples de données du jeu de données. Si le jeu de données a été créé à l’aide d’un schéma, les informations concernant le schéma du jeu de données s’affichent sur le côté gauche de la prévisualisation. Vous pouvez développer le schéma à l’aide des flèches pour voir la structure du schéma. Chaque en-tête de colonne dans la prévisualisation des données représente un champ dans le jeu de données.

![Informations sur le jeu de données](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Étapes suivantes et ressources supplémentaires

Maintenant que vous avez créé un jeu de données et que vous avez ingéré des données avec succès dans [!DNL Experience Platform], vous pouvez répéter ces étapes pour créer un nouveau jeu de données ou ingérer davantage de données dans le jeu de données existant.

Pour en savoir plus sur l’ingestion par lots, veuillez lire la [présentation de l’ingestion par lots](../batch-ingestion/overview.md) et compléter votre apprentissage en regardant la vidéo ci-dessous.

>[!WARNING]
>
>Lʼinterface utilisateur de [!DNL Experience Platform] affichée dans la vidéo suivante est obsolète. Consultez la documentation pour découvrir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
