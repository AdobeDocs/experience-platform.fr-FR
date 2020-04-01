---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Importation de données dans Adobe Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Importation de données dans Adobe Experience Platform

Adobe Experience Platform vous permet d’importer facilement des données dans la plate-forme sous forme de fichiers de commandes. Parmi les exemples de données à ingérer, citons les données  d’un fichier plat dans un système de gestion de la relation client (par exemple un fichier de parquet) ou les données conformes à un de modèle de données d’expérience (XDM) connu dans le registre de l’.

## Prise en main

Pour terminer ce didacticiel, vous devez avoir accès à Experience Platform. Si vous n’avez pas accès à une organisation IMS dans Experience Platform, contactez votre administrateur système avant de poursuivre.

Si vous préférez assimiler des données à l&#39;aide des API d&#39;assimilation des données, lisez d&#39;abord le guide [du développeur d&#39;embouteillages](../batch-ingestion/api-overview.md)par lots.

## Espace de travail Datasets

L’espace de travail des jeux de données dans Experience Platform vous permet d’afficher et de gérer tous les jeux de données créés par votre organisation IMS ainsi que d’en créer.

Affichez l’espace de travail des jeux de données en cliquant sur **Jeux de données** dans le volet de navigation de gauche. The Datasets workspace contains a list of datasets, including columns showing _Name_, _Created_ (date and time), _Source_, _Schema_, and _Last Batch Status_, as well as the date and time the dataset was _Last Updated_.

>[!NOTE] Cliquez sur l&#39;icône de filtre en regard de la barre de recherche pour utiliser les fonctionnalités de filtrage afin de ne  que les jeux de données activés pour les  de.

![tous les jeux de données](../images/tutorials/ingest-batch-data/datasets_workspace.png)

## Création d’un jeu de données

Pour créer un jeu de données, cliquez sur **Créer un jeu** de données dans le coin supérieur droit de l’espace de travail Jeux de données.

Dans l’écran **Créer un jeu** de données, indiquez si vous souhaitez &quot;Créer un jeu de données à partir d’un &quot; ou &quot;Créer un jeu de données à partir d’un fichier CSV&quot;.

Dans ce didacticiel, un  sera utilisé pour créer le jeu de données. Cliquez sur **Créer un jeu de données à partir du** pour continuer.

![Sélectionner la source de données](../images/tutorials/ingest-batch-data/create_dataset.png)

## Sélectionner un de jeux de données

Dans l’écran **Sélectionner** de, choisissez un  de en cliquant sur le bouton radio situé à côté de la  à utiliser. Pour ce didacticiel, le jeu de données sera créé à l&#39;aide du  Membres fidélité. L&#39;utilisation de la barre de recherche pour filtrer les  de est un moyen utile de trouver le exact  que vous recherchez.

Une fois que vous avez sélectionné le bouton radio en regard du que vous souhaitez utiliser, cliquez sur **Suivant**.

![Sélectionner](../images/tutorials/ingest-batch-data/select_schema.png)

## Configurer un jeu de données

Dans l’écran **Configurer le jeu de données** , vous devrez attribuer un **nom** à votre jeu de données et vous pouvez également fournir une **description** du jeu de données.

**Remarques sur les noms des jeux de données :**

- Les noms des jeux de données doivent être courts et descriptifs afin que le jeu de données puisse être facilement retrouvé dans la bibliothèque ultérieurement.
- Les noms des jeux de données doivent être uniques, ce qui signifie qu’ils doivent être suffisamment spécifiques pour ne pas être réutilisés à l’avenir.
- Il est recommandé de fournir des informations supplémentaires sur le jeu de données à l’aide du champ de description, car cela peut aider d’autres utilisateurs à différencier les jeux de données à l’avenir.

Une fois que le jeu de données a un nom et une description, cliquez sur **Terminer**.

![Configurer un jeu de données](../images/tutorials/ingest-batch-data/configure_dataset.png)

##  de données 

Un jeu de données vide a maintenant été créé et vous avez été renvoyé à l&#39;onglet  de jeu de **données** dans l&#39;espace de travail Jeu de données. Vous devriez voir le nom du jeu de données dans le coin supérieur gauche de l’espace de travail, ainsi qu’une notification indiquant qu’aucun lot n’a été ajouté. Vous devez vous y attendre, car vous n’avez encore ajouté aucun lot à ce jeu de données.

Sur le côté droit de l’espace de travail Jeu de données, l’onglet **Infos** contient des informations relatives à votre nouveau jeu de données, telles que l’ID _du jeu de données, le_ nom _, la__description, le nomTable, le, leStreaminget leSource._________ L’onglet Infos contient également des informations sur le moment où le jeu de données a été _créé_ et sa date de _dernière modification_ .

L’onglet Infos contient également une bascule de __ qui permet d’activer votre jeu de données pour l’utiliser avec le client en temps réel . L’utilisation de cette bascule et l’ Client en temps réel seront expliquées plus en détail dans la section qui suit.

![de données](../images/tutorials/ingest-batch-data/dataset_activity.png)

## Activer le jeu de données pour les  de clients en temps réel

Les jeux de données sont utilisés pour ingérer des données dans la plateforme d’expérience et ces données sont finalement utilisées pour identifier des individus et rassembler des informations provenant de sources multiples. Cette combinaison d&#39;informations s&#39;appelle un  client en temps réel. Pour que la Plateforme sache quelles informations doivent être incluses dans le  en temps réel, les jeux de données peuvent être marqués pour inclusion à l’aide de la bascule **du** .

Par défaut, cette bascule est désactivée. Si vous choisissez de basculer sur les  de, toutes les données saisies dans le jeu de données seront utilisées pour identifier un individu et assembler son  en temps réel.

Pour en savoir plus sur les  des clients en temps réel et l’utilisation des identités, consultez la documentation du service [d’identité](../../identity-service/home.md) .

Pour activer le jeu de données pour les  de clients en temps réel, cliquez sur le **du****dans l’onglet** Informations.

![Basculement](../images/tutorials/ingest-batch-data/enable_dataset_unified_profile.png)

Une boîte de dialogue s’affiche vous demandant de confirmer que vous souhaitez activer le jeu de données pour les  de clients en temps réel.

![Boîte de dialogue  d’activation](../images/tutorials/ingest-batch-data/confirm_dataset_enable.png)

Cliquez sur **Activer** et la bascule devient bleue, indiquant qu’elle est activée.

![Activé pour les  de](../images/tutorials/ingest-batch-data/dataset_enabled.png)

## Ajouter données à un jeu de données

Les données peuvent être ajoutées à un jeu de données de différentes manières. Vous pouvez choisir d’utiliser des API d’administration de données ou un partenaire ETL, tel que Unifi ou Informatica. Dans ce didacticiel, les données seront ajoutées au jeu de données à l’aide de l’onglet Données **** Ajouter dans l’interface utilisateur.

Pour commencer à ajouter des données au jeu de données, cliquez sur l’onglet Données **** Ajouter. Vous pouvez désormais faire glisser des fichiers ou rechercher les fichiers à ajouter sur votre ordinateur.

>[!NOTE] Platform prend en charge deux types de fichiers pour l’assimilation de données : parquet ou JSON. Vous pouvez ajouter jusqu’à cinq fichiers à la fois, la taille maximale de chaque fichier étant de 10 Go.

![Ajouter, onglet Données](../images/tutorials/ingest-batch-data/add_data.png)

## Téléchargement d’un fichier

Une fois que vous faites glisser et déposez (ou parcourez et sélectionnez) un fichier JSON ou parquet que vous souhaitez télécharger, Platform commence immédiatement à traiter le fichier et une boîte de dialogue de **téléchargement** s’affiche dans l’onglet Données **** Ajouter montrant la progression du transfert du fichier.

![Boîte de dialogue de téléchargement](../images/tutorials/ingest-batch-data/uploading.png)

## Mesures de jeux de données

Une fois le téléchargement du fichier terminé, l’onglet  de **données de l’onglet** n’indique plus qu’aucun lot n’a été ajouté. L’onglet  jeu de données  affiche désormais les mesures des jeux de données. Toutes les mesures indiqueront &quot;0&quot; à cette étape, car le lot n’a pas encore été chargé.

Au bas de l&#39;onglet se trouve un  présentant l&#39;ID __ du lot des données qui venaient d&#39;être assimilées via le processus [&quot;Ajouter données au jeu de données&quot;](#add-data-to-dataset) . Sont également incluses les informations relatives au lot, notamment la date _d’importation_ , le nombre d’ _enregistrements d’importation_ et le _statut_ actuel du lot.

![Mesures de jeux de données](../images/tutorials/ingest-batch-data/batch_loading.png)

## Détails du lot

Cliquez sur l’ID __ du lot pour  une présentation **du** lot, en indiquant des détails supplémentaires sur le lot. Une fois le chargement du lot terminé, les informations sur le lot sont mises à jour afin d’afficher le nombre d’ _enregistrements insérés_ et la taille _du_ fichier. Le _statut_ devient également &quot;Succès&quot; ou &quot;Echec&quot;. Si le lot échoue, la section Code _d&#39;_ erreur contiendra des informations détaillées sur les erreurs survenant lors de l&#39;assimilation.

Pour plus d’informations et pour obtenir des questions fréquentes sur l’assimilation par lots, consultez le guide [de dépannage de l’](../batch-ingestion/troubleshooting.md)assimilation par lots.

Pour revenir à l’écran  de l’ensemble de **données** , cliquez sur le nom du jeu de données (_Détails_ de fidélité) dans le chemin de navigation.

![Présentation du lot](../images/tutorials/ingest-batch-data/batch_overview.png)

## Jeu de données 

Une fois que le jeu de données est prêt, une option permettant de **jeu** de données s’affiche en haut de l’onglet  de jeu de **données** .

Cliquez sur **jeu** de données pour ouvrir une boîte de dialogue présentant les données d’exemple du jeu de données. Si le jeu de données a été créé à l’aide d’un  de, les détails du du jeu de données s’affichent sur le côté gauche du. Vous pouvez développer le  à l’aide des flèches pour voir la structure  du. Chaque en-tête de colonne dans les données  du représente un champ dans le jeu de données.

![Détails du jeu de données](../images/tutorials/ingest-batch-data/dataset_details.png)

## Étapes suivantes

Maintenant que vous avez créé un jeu de données et que vous avez assimilé des données avec succès dans la plateforme d’expérience, vous pouvez répéter ces étapes pour créer un nouveau jeu de données ou intégrer davantage de données dans le jeu de données existant.

Pour en savoir plus sur l&#39;ingestion par lots, veuillez lire l&#39;aperçu [de l&#39;ingestion par](../batch-ingestion/overview.md)lot.
