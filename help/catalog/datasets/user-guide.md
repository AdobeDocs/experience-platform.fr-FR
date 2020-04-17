---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’utilisateur des jeux de données
topic: datasets
translation-type: tm+mt
source-git-commit: 7d3f64db787aebe46179c0e08ad01878b0ad2877

---


# Guide de l’utilisateur des jeux de données

Ce guide d’utilisation fournit des instructions sur l’exécution d’actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur d’Adobe Experience Platform.

## Prise en main

Ce guide d’utilisation nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Jeu de données](overview.md): Le concept  de  et de gestion pour la persistance des données dans la plateforme d’expérience.
* [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Éditeur](../../xdm/tutorials/create-schema-ui.md)de  : Découvrez comment créer votre propre XDM personnalisé à l’aide de l’éditeur de  de dans l’interface utilisateur de la plateforme.
* [](../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Gouvernance](../../data-governance/home.md)des données : Veiller à la conformité aux réglementations, restrictions et stratégies relatives à l’utilisation des données client.

##  de données

Dans l’interface utilisateur de la plate-forme d’expérience, cliquez sur **Jeu de données** dans le volet de navigation de gauche pour ouvrir le  des jeux de *données* . Le   tous les jeux de données disponibles pour votre organisation. Des détails s’affichent pour chaque jeu de données répertorié, y compris son nom, le auquel le jeu de données adhère et l’état de l’exécution d’assimilation la plus récente.

![](../images/datasets/user-guide/browse_datasets.png)

Cliquez sur le nom d&#39;un jeu de données pour accéder à son  de *données l&#39;écran* du et voir les détails du jeu de données que vous avez sélectionné. L’onglet   de comprend un graphique qui présente le taux de messages consommés ainsi qu’un de lots réussis et ayant échoué.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

##  d’un jeu de données

Dans l’écran  de l’ de *jeux de données* , cliquez sur le jeu de données **** situé dans le coin supérieur droit de l’écran pour jusqu’à 100 lignes de données. Si le jeu de données est vide, le lien  du est désactivé et indique **que le  n’est pas disponible**.

![](../images/datasets/user-guide/click_to_preview.png)

Dans la fenêtre  du, le hiérarchique du  dujeu de données s’affiche à droite.

![](../images/datasets/user-guide/preview_dataset.png)

Pour des méthodes plus robustes d’accès à vos données, Experience Platform fournit des services en aval tels que le service de  de et JupyterLab pour explorer et analyser les données. Pour plus d’informations, reportez-vous au  suivant :

* [Présentation du service](../../query-service/home.md)
* [Guide de l&#39;utilisateur de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Création d’un jeu de données {#create}

Pour créer un jeu de données,  en cliquant sur **Créer un jeu** de données dans le *Jeu de données* .

![](../images/datasets/user-guide/click_to_create.png)

Dans l’écran suivant, vous trouverez les deux options suivantes pour la création d’un jeu de données :

* [Création d’un jeu de données à partir d’](#create-a-dataset-with-an-existing-schema)
* [Création d’un jeu de données à partir d’un fichier CSV](#create-a-dataset-with-a-csv-file)

### Création d’un jeu de données avec un existant 

Dans l’écran *Créer un jeu* de données, cliquez sur **Créer un jeu de données à partir de** de pour créer un jeu de données vide.

![](../images/datasets/user-guide/create_dataset_schema.png)

L’étape *Sélectionner* du s’affiche. Parcourez la liste des  du et sélectionnez le auquel le jeu de données doit adhérer avant de cliquer sur **Suivant**.

![](../images/datasets/user-guide/select_schema.png)

L’étape *Configurer le jeu de données* s’affiche. Indiquez un nom et une description facultative au jeu de données, puis cliquez sur **Terminer** pour créer le jeu de données.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Création d’un jeu de données avec un fichier CSV

Lorsqu’un jeu de données est créé à l’aide d’un fichier CSV, un ad hoc est créé pour fournir au jeu de données une structure qui correspond au fichier CSV fourni. Dans l’écran *Créer un jeu* de données, cliquez sur la zone correspondant à **Créer un jeu de données à partir d’un fichier** CSV.

![](../images/datasets/user-guide/create_dataset_csv.png)

The *Configure* step appears. Attribuez un nom au jeu de données et une description facultative, puis cliquez sur **Suivant**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

L’étape de données ** Ajouter s’affiche. Téléchargez le fichier CSV en le faisant glisser vers le centre de votre écran ou en cliquant sur **Parcourir** pour explorer le répertoire de vos fichiers. La taille du fichier peut atteindre dix gigaoctets. Une fois le fichier CSV téléchargé, cliquez sur **Enregistrer** pour créer le jeu de données.

>[!NOTE] Les noms de colonnes CSV doivent être  de caractères alphanumériques et ne peuvent contenir que des lettres, des chiffres et des traits de soulignement.

![](../images/datasets/user-guide/add_csv_data.png)

## Activation d’un jeu de données pour Real-time Customer Profile

Chaque jeu de données permet d’enrichir les  clients avec ses données assimilées. Pour ce faire, le auquel adhère le jeu de données doit être compatible pour être utilisé dans le client en temps réel . Un  compatible satisfait aux exigences suivantes :

* Le  comporte au moins un attribut spécifié comme propriété d’identité.
* La propriété d’identité du est définie en tant qu’identité principale.

Pour plus d’informations sur l’activation d’un  pour les  de, consultez le guide [de l’utilisateur de l’éditeur de](../../xdm/tutorials/create-schema-ui.md)ded’d’.

Pour activer un jeu de données pour les  de, accédez à l’écran de  de jeu de *données* et cliquez sur le **** ** basculede la colonne Propriétés. Une fois activées, les données qui sont assimilées dans le jeu de données sont également utilisées pour renseigner les  du client.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

Si un jeu de données contient déjà des données, puis est activé pour les  de, les données existantes ne sont pas consommées par les  de. Une fois qu’un jeu de données est activé pour les  de, il est recommandé de réassimiler toutes les données existantes afin qu’elles renseignent le du client .

## Gérer et appliquer la gouvernance des données sur un jeu de données

L’étiquetage et l’application de l’utilisation des données (DULE) est le mécanisme de gouvernance des données de base pour la plateforme d’expérience. Les libellés DULE vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Pour en savoir plus sur les libellés, consultez l’aperçu [de la gouvernance des](../../data-governance/home.md) données ou consultez le guide [utilisateur des libellés d’utilisation des](../../data-governance/labels/overview.md) données pour savoir comment appliquer des libellés aux jeux de données.

## Suppression d’un jeu de données

Vous pouvez supprimer un jeu de données en accédant d’abord à son  de *données l’écran* du. Cliquez ensuite sur **Supprimer le jeu** de données pour le supprimer.

>[!NOTE] Les jeux de données créés et utilisés par les applications et services Adobe (tels qu’Adobe Analytics, Adobe  Gestionnaire de  de ou Service de prise de décision) ne peuvent pas être supprimés.

![](../images/datasets/user-guide/delete_dataset.png)

Une zone de confirmation s’affiche. Cliquez sur **Supprimer** pour confirmer la suppression du jeu de données.

![](../images/datasets/user-guide/confirm_delete.png)

## Suppression d’un jeu de données compatible avec les 

Si un jeu de données est activé pour les  de, sa suppression via l’interface utilisateur désactive le jeu de données pour l’assimilation, mais ne supprime pas automatiquement le jeu de données dans le serveur principal. Pour supprimer complètement le jeu de données, y compris les données d&#39; et d&#39;identité qu&#39;il contient, une demande de suppression supplémentaire doit être effectuée. Pour savoir comment supprimer correctement les données du magasin de  de, reportez-vous au [sous-guide de l’API d’de clients en temps réel sur les tâches de  système de](../../profile/api/profile-system-jobs.md)gestion des données, également appelé &quot;requêtes de suppression&quot;.

## Analyse de l&#39;assimilation des données

Dans l’interface utilisateur de la plateforme d’expérience, cliquez sur **Surveillance** dans le volet de navigation de gauche. Le  de *surveillance* vous permet de  les états des données entrantes issues de l’assimilation par lot ou en flux continu. Pour  les états de lots individuels, cliquez sur *Traitement par lots de bout en bout* ou *Diffusion en* flux continu de bout en bout. Le  toutes les exécutions d’assimilation par lot ou en flux continu, y compris celles qui sont réussies, échouées ou encore en cours. Chaque liste fournit des détails sur le lot, y compris l’ID du lot, le nom du jeu de données du  et le nombre d’enregistrements assimilés. Si le jeu de  de données du est activé pour les  de, le nombre d’enregistrements d’identité et d’enregistrements de est également affiché.

![](../images/datasets/user-guide/batch_listing.png)

Vous pouvez cliquer sur un ID **de** lot individuel pour accéder au  d’aperçu *du* lot et afficher les détails du lot, y compris les journaux d’erreurs en cas d’échec de l’assimilation du lot.

![](../images/datasets/user-guide/batch_overview.png)

Si vous souhaitez supprimer le lot, vous pouvez le faire en cliquant sur **Supprimer le lot** situé en haut à droite du  de. Cela supprimera également ses enregistrements du jeu de données auquel le lot a été initialement assimilé.

![](../images/datasets/user-guide/delete_batch.png)

## Étapes suivantes

Ce guide de l’utilisateur fournit des instructions sur l’exécution d’actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur de la plateforme d’expérience. Pour obtenir des instructions sur l’exécution de  de plateforme commune impliquant des jeux de données, reportez-vous aux didacticiels suivants :

* [Création d’un jeu de données à l’aide d’API](create.md)
* [des données de jeu de données à l’aide de l’API d’accès aux données](../../data-access/home.md)
* [Configuration d’un jeu de données pour Real-time Customer Profile et Identity Service à l’aide des API](../../profile/tutorials/dataset-configuration.md)