---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Envoi de données dans un Adobe Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 3%

---


# Envoi de données dans un Adobe Experience Platform

Adobe Experience Platform vous permet d&#39;importer facilement des données dans Platform sous forme de fichiers de commandes. Parmi les exemples de données à ingérer, citons les données de profil provenant d’un fichier plat dans un système de gestion de la relation client (par exemple un fichier de parquet) ou les données conformes à un schéma connu de modèle de données d’expérience (XDM) dans le registre des Schémas.

## Prise en main

Pour terminer ce didacticiel, vous devez avoir accès à un Experience Platform. Si vous n&#39;avez pas accès à une organisation IMS en Experience Platform, contactez votre administrateur système avant de continuer.

Si vous préférez ingérer des données à l&#39;aide des API d&#39;assimilation des données, lisez d&#39;abord le guide [du développeur d&#39;](../batch-ingestion/api-overview.md)assimilation par lots.

## Espace de travail Datasets

L’espace de travail des jeux de données dans Experience Platform vous permet d’afficher et de gérer tous les jeux de données créés par votre organisation IMS ainsi que d’en créer.

Affichez l’espace de travail des jeux de données en cliquant sur **Jeux de données** dans le volet de navigation de gauche. The Datasets workspace contains a list of datasets, including columns showing _Name_, _Created_ (date and time), _Source_, _Schema_, and _Last Batch Status_, as well as the date and time the dataset was _Last Updated_.

>[!NOTE]
>
>Cliquez sur l&#39;icône de filtre en regard de la barre de recherche pour utiliser les fonctionnalités de filtrage afin de ne vue que les jeux de données activés pour le Profil.

![Vue de tous les jeux de données](../images/tutorials/ingest-batch-data/datasets_workspace.png)

## Création d’un jeu de données

Pour créer un jeu de données, cliquez sur **Créer un jeu de données** dans le coin supérieur droit de l’espace de travail Jeux de données.

Dans l’écran **Créer un jeu de données** , indiquez si vous souhaitez &quot;Créer un jeu de données à partir d’un Schéma&quot; ou &quot;Créer un jeu de données à partir d’un fichier CSV&quot;.

Pour ce didacticiel, un schéma sera utilisé pour créer le jeu de données. Cliquez sur **Créer un jeu de données à partir du Schéma** pour continuer.

![Sélectionner la source de données](../images/tutorials/ingest-batch-data/create_dataset.png)

## Sélectionner un schéma de données

Dans l’écran **Sélectionner un Schéma** , choisissez un schéma en cliquant sur le bouton radio en regard du schéma que vous souhaitez utiliser. Pour ce didacticiel, le jeu de données sera créé à l&#39;aide du schéma Membres de fidélité. L&#39;utilisation de la barre de recherche pour filtrer les schémas est un moyen utile de trouver le schéma exact que vous recherchez.

Une fois que vous avez sélectionné le bouton radio en regard du schéma que vous souhaitez utiliser, cliquez sur **Suivant**.

![Sélectionner un schéma](../images/tutorials/ingest-batch-data/select_schema.png)

## Configurer un jeu de données

Dans l&#39;écran **Configurer un jeu de données** , vous devrez attribuer un **nom** à votre jeu de données et peut également fournir une **description** du jeu de données.

**Remarques sur les noms des jeux de données :**

- Les noms des jeux de données doivent être courts et descriptifs afin que le jeu de données puisse être facilement trouvé dans la bibliothèque ultérieurement.
- Les noms des jeux de données doivent être uniques, ce qui signifie qu&#39;ils doivent également être suffisamment précis pour ne pas être réutilisés à l&#39;avenir.
- Il est recommandé de fournir des informations supplémentaires sur le jeu de données à l’aide du champ de description, car cela peut aider d’autres utilisateurs à différencier les jeux de données à l’avenir.

Une fois que le jeu de données a un nom et une description, cliquez sur **Terminer**.

![Configurer un jeu de données](../images/tutorials/ingest-batch-data/configure_dataset.png)

## activité des jeux de données

Un jeu de données vide a maintenant été créé et vous avez été renvoyé à l&#39;onglet Activité **des jeux de** données dans l&#39;espace de travail Jeux de données. Vous devriez voir le nom du jeu de données dans le coin supérieur gauche de l’espace de travail, ainsi qu’une notification indiquant qu’aucun lot n’a été ajouté. Ceci est à prévoir, car vous n&#39;avez encore ajouté aucun lot à ce jeu de données.

L&#39;onglet **Informations** , situé à droite de l&#39;espace de travail Jeux de données, contient des informations relatives à votre nouveau jeu de données, telles que l&#39;ID _du jeu de données, le_ nom _, la__description, le nom de la table, le Schéma, le  de diffusion en continu et le Source._________ L’onglet Infos contient également des informations sur le moment où le jeu de données a été _créé_ et sa date de _dernière modification_ .

L’onglet Infos contient également une bascule _Profil_ utilisée pour activer votre jeu de données en vue de l’utiliser avec le Profil client en temps réel. L’utilisation de cette bascule, ainsi que le Profil client en temps réel, seront expliqués plus en détail dans la section qui suit.

![activité des jeux de données](../images/tutorials/ingest-batch-data/dataset_activity.png)

## Activation du jeu de données pour le Profil client en temps réel

Les jeux de données sont utilisés pour ingérer des données dans l&#39;Experience Platform, et ces données sont en fin de compte utilisées pour identifier les individus et rassembler des informations provenant de sources multiples. Cette combinaison d&#39;informations s&#39;appelle un Profil client en temps réel. Pour que Platform sache quelles informations doivent être incluses dans le Profil en temps réel, les jeux de données peuvent être marqués pour inclusion à l’aide de la bascule **Profil** .

Par défaut, cette bascule est désactivée. Si vous choisissez de basculer sur le Profil, toutes les données saisies dans le jeu de données seront utilisées pour identifier un individu et assembler son Profil en temps réel.

Pour en savoir plus sur le Profil client en temps réel et l&#39;utilisation des identités, consultez la documentation du service [d&#39;](../../identity-service/home.md) identité.

Pour activer le jeu de données pour le Profil client en temps réel, cliquez sur la bascule **Profil** dans l’onglet **Informations** .

![Basculement Profil](../images/tutorials/ingest-batch-data/enable_dataset_unified_profile.png)

Une boîte de dialogue s’affiche vous demandant de confirmer que vous souhaitez activer le jeu de données pour le Profil client en temps réel.

![Boîte de dialogue Activer le Profil](../images/tutorials/ingest-batch-data/confirm_dataset_enable.png)

Cliquez sur **Activer** et la bascule devient bleue, indiquant qu’elle est activée.

![Activé pour le Profil](../images/tutorials/ingest-batch-data/dataset_enabled.png)

## Ajouter les données au jeu de données

Les données peuvent être ajoutées à un jeu de données de différentes manières. Vous pouvez choisir d&#39;utiliser des API d&#39;importation de données ou un partenaire ETL tel que Unifi ou Informatica. Pour ce didacticiel, les données seront ajoutées au jeu de données à l’aide de l’onglet **Ajouter les données** dans l’interface utilisateur.

Pour commencer à ajouter des données au jeu de données, cliquez sur l&#39;onglet **Ajouter les données** . Vous pouvez désormais faire glisser et déposer des fichiers ou rechercher sur votre ordinateur les fichiers à ajouter.

>[!NOTE]
>
>Platform prend en charge deux types de fichiers pour l’assimilation de données : parquet ou JSON. Vous pouvez ajouter jusqu’à cinq fichiers à la fois, la taille maximale de chaque fichier étant de 10 Go.

![Ajouter les données, onglet](../images/tutorials/ingest-batch-data/add_data.png)

## Téléchargement d’un fichier

Une fois que vous faites glisser et déposez (ou parcourez et sélectionnez) un fichier de parquet ou JSON que vous souhaitez télécharger, Platform commence immédiatement à traiter le fichier et une boîte de dialogue de **téléchargement** s’affiche sur l’onglet **Ajouter les données** qui indique la progression du téléchargement de votre fichier.

![Boîte de dialogue de téléchargement](../images/tutorials/ingest-batch-data/uploading.png)

## Mesures de jeux de données

Une fois le transfert du fichier terminé, l’onglet Activité **des** jeux de données ne montre plus qu’aucun lot n’a été ajouté. L’onglet Activité des ensembles de données affiche désormais les mesures des ensembles de données. Toutes les mesures affichent &quot;0&quot; à ce stade, car le lot n’a pas encore été chargé.

Au bas de l&#39;onglet se trouve une liste présentant l&#39;ID __ de lot des données qui viennent d&#39;être ingérées via le [&quot;Ajouter les données au jeu de données&quot;](#add-data-to-dataset) . Sont également incluses les informations relatives au lot, notamment la date _d&#39;importation_ , le nombre d&#39; _enregistrements insérés_ et le _statut_ actuel du lot.

![Mesures de jeux de données](../images/tutorials/ingest-batch-data/batch_loading.png)

## Détails du lot

Cliquez sur l&#39;ID __ de lot pour vue un aperçu **du** lot et afficher des détails supplémentaires sur le lot. Une fois le chargement du lot terminé, les informations relatives au lot sont mises à jour afin d’afficher le nombre d’ _enregistrements insérés_ et la taille _du_ fichier. Le _statut_ devient également &quot;Réussite&quot; ou &quot;Échec&quot;. Si le lot échoue, la section Code _d&#39;_ erreur contiendra des informations détaillées sur les erreurs survenues lors de l&#39;assimilation.

Pour plus d&#39;informations et les questions fréquentes sur l&#39;assimilation de lots, consultez le guide [de dépannage de l&#39;assimilation de](../batch-ingestion/troubleshooting.md)lots.

Pour revenir à l’écran Activité **des** jeux de données, cliquez sur le nom du jeu de données (Détails __ de fidélité) dans la barre de navigation.

![Présentation du lot](../images/tutorials/ingest-batch-data/batch_overview.png)

## Jeu de données de Prévisualisation

Une fois que le jeu de données est prêt, une option de jeu de données **de** Prévisualisation s&#39;affiche en haut de l&#39;onglet Activité **de** données.

Cliquez sur Jeu **de données de** Prévisualisation pour ouvrir une boîte de dialogue présentant les données d’exemple du jeu de données. Si le jeu de données a été créé à l’aide d’un schéma, les détails du schéma du jeu de données s’affichent sur le côté gauche de la prévisualisation. Vous pouvez développer le schéma à l’aide des flèches pour voir la structure du schéma. Chaque en-tête de colonne des données de la prévisualisation représente un champ du jeu de données.

![Détails du jeu de données](../images/tutorials/ingest-batch-data/dataset_details.png)

## Étapes suivantes

Maintenant que vous avez créé un jeu de données et que vous avez bien assimilé des données à un Experience Platform, vous pouvez répéter ces étapes pour créer un nouveau jeu de données ou assimiler davantage de données dans le jeu existant.

Pour en savoir plus sur l&#39;assimilation par lots, veuillez lire l&#39;aperçu [](../batch-ingestion/overview.md)de l&#39;assimilation par lots.
