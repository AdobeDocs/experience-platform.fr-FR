---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’utilisateur des jeux de données
topic: datasets
translation-type: tm+mt
source-git-commit: 7d3f64db787aebe46179c0e08ad01878b0ad2877
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---


# Guide de l’utilisateur des jeux de données

Ce guide d’utilisateur fournit des instructions sur l’exécution d’actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur d’Adobe Experience Platform.

## Prise en main

Ce guide d’utilisation nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Jeu de données](overview.md): concept d’enregistrement et de gestion pour la persistance des données dans la plateforme d’expérience.
* [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Éditeur](../../xdm/tutorials/create-schema-ui.md)de Schéma : Découvrez comment créer vos propres schémas XDM personnalisés à l’aide de l’éditeur de Schéma dans l’interface utilisateur de la plate-forme.
* [Profil](../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Gouvernance](../../data-governance/home.md)des données : Veiller au respect des réglementations, restrictions et stratégies relatives à l’utilisation des données client.

## Jeu de données de Vue

Dans l’interface utilisateur de la plate-forme d’expérience, cliquez sur **Jeu de données** dans le volet de navigation de gauche pour ouvrir le tableau de bord *Jeu de données* . Le tableau de bord liste tous les jeux de données disponibles pour votre organisation. Les détails s&#39;affichent pour chaque jeu de données répertorié, y compris son nom, le schéma auquel le jeu de données adhère et l&#39;état de l&#39;exécution d&#39;assimilation la plus récente.

![](../images/datasets/user-guide/browse_datasets.png)

Cliquez sur le nom d&#39;un jeu de données pour accéder à son écran d&#39;activité *des* jeux de données et voir les détails du jeu de données que vous avez sélectionné. L&#39;onglet activité comprend un graphique qui présente le taux de messages consommés ainsi qu&#39;une liste de lots réussis et d&#39;échecs.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Prévisualisation d’un jeu de données

Dans l’écran activité *des* jeux de données, cliquez sur Jeu de données **de** Prévisualisation situé dans le coin supérieur droit de l’écran pour prévisualisation jusqu’à 100 lignes de données. Si le jeu de données est vide, le lien de la prévisualisation est désactivé et indique plutôt que **la Prévisualisation n&#39;est pas disponible**.

![](../images/datasets/user-guide/click_to_preview.png)

Dans la fenêtre prévisualisation, la vue hiérarchique du schéma du jeu de données s’affiche à droite.

![](../images/datasets/user-guide/preview_dataset.png)

Pour des méthodes plus robustes d’accès à vos données, Experience Platform fournit des services en aval tels que Requête Service et JupyterLab pour explorer et analyser les données. Pour plus d’informations, voir les documents suivants :

* [Présentation du service Requête](../../query-service/home.md)
* [Guide de l&#39;utilisateur de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Création d’un jeu de données {#create}

Pour créer un nouveau jeu de données, début en cliquant sur **Créer un jeu de données** dans le tableau de bord *Jeu de données* .

![](../images/datasets/user-guide/click_to_create.png)

Dans l’écran suivant, vous trouverez les deux options suivantes pour la création d’un nouveau jeu de données :

* [Créer un jeu de données à partir d&#39;un schéma](#create-a-dataset-with-an-existing-schema)
* [Création d’un jeu de données à partir d’un fichier CSV](#create-a-dataset-with-a-csv-file)

### Créer un jeu de données avec un schéma existant

Dans l’écran *Créer un jeu de données* , cliquez sur **Créer un jeu de données à partir du schéma** pour créer un nouveau jeu de données vide.

![](../images/datasets/user-guide/create_dataset_schema.png)

L&#39;étape *Sélectionner un schéma* s&#39;affiche. Parcourez la liste des schémas et sélectionnez le schéma auquel le jeu de données doit adhérer avant de cliquer sur **Suivant**.

![](../images/datasets/user-guide/select_schema.png)

L&#39;étape *Configurer le jeu de données* s&#39;affiche. Indiquez un nom et une description facultative au jeu de données, puis cliquez sur **Terminer** pour créer le jeu de données.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Création d’un jeu de données avec un fichier CSV

Lorsqu’un jeu de données est créé à l’aide d’un fichier CSV, un schéma ad hoc est créé pour fournir au jeu de données une structure correspondant au fichier CSV fourni. Dans l’écran *Créer un jeu de données* , cliquez sur la case à cocher &quot; **Créer un jeu de données à partir d’un fichier** CSV&quot;.

![](../images/datasets/user-guide/create_dataset_csv.png)

The *Configure* step appears. Fournissez un nom et une description facultative au jeu de données, puis cliquez sur **Suivant**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

L’étape *Ajouter données* s’affiche. Téléchargez le fichier CSV en le faisant glisser vers le centre de l’écran ou en cliquant sur **Parcourir** pour explorer le répertoire de vos fichiers. La taille du fichier peut atteindre dix gigaoctets. Une fois le fichier CSV téléchargé, cliquez sur **Enregistrer** pour créer le jeu de données.

>[!NOTE] Les noms de colonnes CSV doivent être débuts de caractères alphanumériques et ne peuvent contenir que des lettres, des chiffres et des traits de soulignement.

![](../images/datasets/user-guide/add_csv_data.png)

## Activation d’un jeu de données pour Real-time Customer Profile

Chaque jeu de données peut enrichir les profils clients avec ses données imbriquées. Pour ce faire, le schéma auquel adhère le jeu de données doit être compatible avec le Profil client en temps réel. Un schéma compatible satisfait aux exigences suivantes :

* Le schéma comporte au moins un attribut spécifié comme propriété d&#39;identité.
* Le schéma possède une propriété d&#39;identité définie en tant qu&#39;identité principale.

Pour plus d’informations sur l’activation d’un schéma pour le Profil, consultez le guide [d’utilisation de l’éditeur de](../../xdm/tutorials/create-schema-ui.md)Schémas.

Pour activer un jeu de données pour le Profil, accédez à l&#39;écran activité *du jeu de* données, puis cliquez sur l&#39;icône de **Profil** située dans la colonne *Propriétés* . Une fois activées, les données qui sont incorporées dans le jeu de données sont également utilisées pour renseigner les profils du client.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

Si un jeu de données contient déjà des données et est ensuite activé pour le Profil, les données existantes ne sont pas utilisées par le Profil. Une fois qu’un jeu de données est activé pour le Profil, il est recommandé de réassimiler toutes les données existantes afin qu’elles soient renseignées dans les profils client.

## Gérer et appliquer la gouvernance des données sur un jeu de données

L’étiquetage et l’application de l’utilisation des données (DULE) est le mécanisme de gouvernance des données de base pour la plateforme d’expérience. Les étiquettes DOUBLE vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Pour en savoir plus sur les libellés, consultez l’aperçu [de la gouvernance des](../../data-governance/home.md) données ou consultez le guide [d’utilisation des libellés d’utilisation des](../../data-governance/labels/overview.md) données pour savoir comment appliquer des libellés aux jeux de données.

## Suppression d’un jeu de données

Vous pouvez supprimer un jeu de données en accédant d&#39;abord à son écran d&#39;activité *des* jeux de données. Cliquez ensuite sur **Supprimer le jeu** de données pour le supprimer.

>[!NOTE] Les jeux de données créés et utilisés par les applications et services Adobe (tels qu’Adobe Analytics, Adobe Audience Manager ou le service de prise de décision) ne peuvent pas être supprimés.

![](../images/datasets/user-guide/delete_dataset.png)

Une zone de confirmation s’affiche. Cliquez sur **Supprimer** pour confirmer la suppression du jeu de données.

![](../images/datasets/user-guide/confirm_delete.png)

## Suppression d’un jeu de données compatible avec les Profils

Si un jeu de données est activé pour le Profil, sa suppression via l&#39;interface utilisateur désactive le jeu de données pour l&#39;assimilation, mais ne supprime pas automatiquement le jeu de données dans le serveur principal. Pour supprimer complètement le jeu de données, y compris les données d&#39;profil et d&#39;identité qu&#39;il contient, une demande de suppression supplémentaire doit être effectuée. Pour savoir comment supprimer correctement les données du magasin de Profils, consultez le [sous-guide API Profil client en temps réel sur les tâches du système de profil, également appelé &quot;requêtes de suppression&quot;](../../profile/api/profile-system-jobs.md).

## Analyse de l&#39;assimilation des données

Dans l’interface utilisateur de la plate-forme d’expérience, cliquez sur **Surveillance** dans le volet de navigation de gauche. Le tableau de bord de *surveillance* vous permet de vue des états des données entrantes, que ce soit par lot ou par assimilation. Pour vue les états de lots individuels, cliquez sur *Batch end-end* ou *Streaming end-to-end*. Le tableau de bord liste toutes les exécutions d’assimilation par lot ou en flux continu, y compris celles qui ont réussi, échoué ou sont toujours en cours d’exécution. Chaque liste fournit des détails sur le lot, y compris l&#39;ID du lot, le nom du jeu de données de la cible et le nombre d&#39;enregistrements ingérés. Si le jeu de données de cible est activé pour le Profil, le nombre d&#39;enregistrements d&#39;identité et de profil assimilés s&#39;affiche également.

![](../images/datasets/user-guide/batch_listing.png)

Vous pouvez cliquer sur un ID **de** lot individuel pour accéder au tableau de bord d&#39;aperçu *du* lot et afficher les détails du lot, y compris les journaux d&#39;erreurs en cas d&#39;échec de l&#39;assimilation du lot.

![](../images/datasets/user-guide/batch_overview.png)

Si vous souhaitez supprimer le lot, vous pouvez le faire en cliquant sur **Supprimer le lot** situé en haut à droite du tableau de bord. Ce faisant, il supprimera également ses enregistrements du jeu de données auquel le lot a été initialement assimilé.

![](../images/datasets/user-guide/delete_batch.png)

## Étapes suivantes

Ce guide d’utilisateur fournit des instructions sur l’exécution d’actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur de la plateforme d’expérience. Pour obtenir des instructions sur l’exécution de workflows de plateforme communs impliquant des jeux de données, reportez-vous aux didacticiels suivants :

* [Création d’un jeu de données à l’aide d’API](create.md)
* [Données du jeu de données de Requête à l’aide de l’API d’accès aux données](../../data-access/home.md)
* [Configuration d’un jeu de données pour Real-time Customer Profile et Identity Service à l’aide des API](../../profile/tutorials/dataset-configuration.md)