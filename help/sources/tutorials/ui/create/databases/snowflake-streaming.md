---
title: Diffusion en continu des données de votre base de données de Snowflake vers l’Experience Platform à l’aide de l’interface utilisateur
type: Tutorial
description: Découvrez comment diffuser des données de votre base de données Snwoflake vers Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 49d488f1-90d8-452a-9f3e-02afdcc79b09
source-git-commit: f39ee3af176e3d9b8ad04bfad81793db0ebe71a7
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 17%

---

# Diffusion en continu des données de votre base de données [!DNL Snowflake] vers l’Experience Platform à l’aide de l’interface utilisateur

Découvrez comment utiliser l’interface utilisateur pour diffuser des données de votre base de données [!DNL Snowflake] vers Adobe Experience Platform en suivant ce guide.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Authentification

Pour plus d’informations sur les étapes à suivre avant d’ingérer des données en continu de [!DNL Snowflake] vers l’Experience Platform, consultez le guide sur la [configuration prérequise pour la  [!DNL Snowflake]  diffusion en continu](../../../../connectors/databases/snowflake-streaming.md) .

## Utilisez la source [!DNL Snowflake Streaming] pour diffuser des données [!DNL Snowflake] vers l’Experience Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie *Bases de données*, sélectionnez **[!DNL Snowflake Streaming]**, puis **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les sources qui n’ont pas de compte authentifié dans le catalogue de sources affichent l’option **[!UICONTROL Configurer]** . Une fois qu’il existe un compte authentifié, cette option devient **[!UICONTROL Ajouter des données]**.

![Catalogue de sources dans l’interface utilisateur Experience Platform, avec la carte source de diffusion en continu Snowflake sélectionnée.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

La page **[!UICONTROL Se connecter au compte de diffusion en continu de Snowflake]** s’affiche. Sur cette page, vous pouvez utiliser des informations d’identification nouvelles ou existantes.

>[!BEGINTABS]

>[!TAB Créer un compte]

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** et fournissez un nom, une description facultative et vos informations d’identification.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de création de compte du workflow des sources.](../../../../images/tutorials/create/snowflake-streaming/new.png)

| Informations d’identification | Description |
| --- | --- |
| Compte | Nom de votre compte [!DNL Snowflake]. Pour les conventions sur les noms de compte, lisez le [[!DNL Snowflake Streaming] guide d&#39;authentification](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials). |
| Entrepôt | Nom de votre entrepôt [!DNL Snowflake]. Les entrepôts gèrent l’exécution des requêtes dans [!DNL Snowflake]. Chaque entrepôt [!DNL Snowflake] est indépendant l’un de l’autre et doit être accessible individuellement pour importer des données dans Experience Platform. |
| Base de données | Nom de la base de données [!DNL Snowflake]. La base de données contient les données que vous souhaitez importer dans Experience Platform. |
| Schéma | (Facultatif) Le schéma de base de données associé à votre compte [!DNL Snowflake]. |
| Nom d’utilisateur | Nom d’utilisateur de votre compte [!DNL Snowflake]. |
| Mot de passe | Mot de passe de votre compte [!DNL Snowflake]. |
| Rôle | (Facultatif) Rôle personnalisé pouvant être fourni à un utilisateur pour une connexion donnée. Si elle n’est pas fournie, cette valeur est définie par défaut sur `public`. |

Pour plus d’informations sur la création de compte, consultez la section sur la [configuration des paramètres de rôle](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) dans la présentation de [!DNL Snowflake Streaming].

>[!TAB Utiliser un compte existant]

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** , puis le compte de votre choix dans le catalogue de comptes existant.

Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![Page de sélection de compte existante du catalogue des sources.](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## Sélectionner les données {#select-data}

>[!IMPORTANT]
>
>* Une colonne d’horodatage doit exister dans votre table source pour qu’un flux de données en continu soit créé. L’horodatage est requis pour que l’Experience Platform sache quand les données seront ingérées et quand les données incrémentielles seront diffusées. Vous pouvez ajouter rétroactivement une colonne d’horodatage pour une connexion existante et créer un nouveau flux de données.
>
>* Assurez-vous que la casse des champs de données de votre fichier de données source d’exemple est conforme aux instructions de [!DNL Snowflake] sur la résolution de la casse pour les identifiants. Pour plus d’informations, consultez le [[!DNL Snowflake] document sur la casse de l’identifiant](https://docs.snowflake.com/en/sql-reference/identifiers-syntax#label-identifier-casing) .

L’étape [!UICONTROL Sélectionner des données] apparaît. Au cours de cette étape, vous devez sélectionner les données à importer dans Experience Platform, configurer les horodatages et les fuseaux horaires, puis fournir un exemple de fichier de données source pour l’ingestion de données brutes.

Utilisez le répertoire de la base de données situé à gauche de l&#39;écran et sélectionnez la table à importer dans Experience Platform.

![ L&#39;interface de sélection des données avec une table de base de données sélectionnée.](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

Sélectionnez ensuite le type de colonne d’horodatage de votre tableau. Vous pouvez choisir entre deux types de colonnes d’horodatage : `TIMESTAMP_NTZ` ou `TIMESTAMP_LTZ`. Si vous sélectionnez un type de colonne `TIMESTAMP_NTZ`, vous devez également fournir un fuseau horaire. Vos colonnes doivent avoir une contrainte non nulle. Pour plus d&#39;informations, consultez la section sur les [limitations et les questions fréquentes]

Vous pouvez également configurer les paramètres de renvoi au cours de cette étape. Le renvoi détermine les données ingérées initialement. Si le renvoi est activé, tous les fichiers actuels du chemin spécifié seront ingérés lors de la première ingestion planifiée. Dans le cas contraire, seuls les fichiers chargés entre la première exécution de l’ingestion et l’heure de début seront ingérés. Les fichiers chargés avant l’heure de début ne seront pas ingérés.

Sélectionnez le bouton d’activation/désactivation **[!UICONTROL Renvoi]** pour activer le renvoi.

![ Étapes de configuration de l’horodatage, du fuseau horaire et du renvoi.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

Enfin, sélectionnez **[!UICONTROL Choisir le fichier]** pour charger un exemple de données source afin de créer le jeu de mappages, qui sera utilisé ultérieurement pour mapper vos données d’origine au modèle de données d’expérience (XDM).

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Aperçu des données d’exemple source.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## Fournir des détails sur les jeux de données et les flux de données {#provide-dataset-and-dataflow-details}

Ensuite, vous devez fournir des informations sur votre jeu de données et votre flux de données.

### Détails du jeu de données {#dataset-details}

Un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les données correctement ingérées dans Experience Platform sont conservées en tant que jeux de données dans le lac de données. Au cours de cette étape, vous pouvez créer un nouveau jeu de données ou utiliser un jeu de données existant.

>[!BEGINTABS]

>[!TAB Utiliser un nouveau jeu de données]

Pour utiliser un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**, puis fournissez un nom et une description facultative de votre jeu de données. Vous devez également sélectionner un schéma de modèle de données d’expérience (XDM) auquel votre jeu de données adhère.

![Nouvelle interface de sélection de jeux de données.](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| Détails du nouveau jeu de données | Description |
| --- | --- |
| Nom du jeu de données de sortie | Nom de votre nouveau jeu de données. |
| Description | (Facultatif) Aperçu rapide du nouveau jeu de données. |
| Schéma | Liste déroulante des schémas qui existent dans votre organisation. Vous pouvez également créer votre propre schéma avant le processus de configuration de la source. Pour plus d’informations, consultez le guide sur la [création d’un schéma XDM dans l’interface utilisateur](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Utiliser un jeu de données existant]

Si vous disposez déjà d’un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**, puis utilisez l’option **[!UICONTROL Recherche avancée]** pour afficher une fenêtre de tous les jeux de données de votre organisation, y compris leurs détails respectifs, comme s’ils sont activés pour l’ingestion dans Real-Time Customer Profile.

![Interface de sélection de jeu de données existante.](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

+++Sélectionnez les étapes à suivre pour activer l’ingestion du profil, les diagnostics d’erreur et l’ingestion partielle.

Si votre jeu de données est activé pour Real-time Customer Profile, vous pouvez, au cours de cette étape, activer le **[!UICONTROL jeu de données Profile]** pour activer vos données pour l’ingestion par profil. Vous pouvez également utiliser cette étape pour activer les **[!UICONTROL {diagnostics d’erreur]** et l’ **[!UICONTROL ingestion partielle]**.

* **[!UICONTROL Diagnostic d’erreur]** : sélectionnez **[!UICONTROL Diagnostic d’erreur]** pour demander à la source de produire des diagnostics d’erreur que vous pourrez ensuite référencer lors de la surveillance de l’activité de votre jeu de données et de l’état du flux de données.
* **[!UICONTROL Ingestion partielle]** : l’ingestion par lots partielle permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil configurable. Cette fonctionnalité vous permet d’ingérer toutes vos données précises dans Experience Platform, tandis que toutes vos données incorrectes sont traitées par lots séparément avec des informations sur les raisons de leur non-validité.

+++

### Détails du flux de données {#dataflow-details}

Une fois votre jeu de données configuré, vous devez fournir des détails sur votre flux de données, y compris un nom, une description facultative et des configurations d’alerte.

![L’étape de configuration des détails du flux de données.](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| Configurations de flux de données | Description |
| --- | --- |
| Nom du flux de données | Nom du flux de données.  Par défaut, le nom du fichier importé sera utilisé. |
| Description | (Facultatif) Une brève description de votre flux de données. |
| Alertes | Experience Platform peut produire des alertes basées sur des événements auxquelles les utilisateurs peuvent s’abonner. Ces options nécessitent un flux de données en cours d’exécution pour les déclencher. Pour plus d’informations, consultez la [présentation des alertes](../../alerts.md) <ul><li>**Démarrage de l’exécution du flux de données des sources** : sélectionnez cette alerte pour recevoir une notification lorsque l’exécution du flux de données démarre.</li><li>**L’exécution du flux de données Sources réussit** : sélectionnez cette alerte pour recevoir une notification si votre flux de données se termine sans erreur.</li><li>**Sources Échec de l’exécution du flux de données** : sélectionnez cette alerte pour recevoir une notification si l’exécution du flux de données se termine par des erreurs.</li></ul> |

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]** pour continuer.

## Mappage de champs à un schéma XDM {#mapping}

L’étape [!UICONTROL Mappage] apparaît. Utilisez l’interface de mappage pour mapper vos données source aux champs de schéma appropriés avant d’ingérer ces données dans Experience Platform, puis sélectionnez **[!UICONTROL Suivant]**. Pour obtenir un guide complet sur l’utilisation de l’interface de mappage, consultez le [guide de l’interface utilisateur de la préparation des données](../../../../../data-prep/ui/mapping.md) pour plus d’informations.

![Interface de mappage du workflow des sources.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## Vérifier le flux de données {#review}

La dernière étape du processus de création de flux de données consiste à passer en revue votre flux de données avant de l’exécuter. Utilisez l’étape **[!UICONTROL Réviser]** pour passer en revue les détails de votre nouveau flux de données avant de s’exécuter. Les détails sont regroupés dans les catégories suivantes :

* **Connexion** : indique le type de source, le chemin d’accès approprié du fichier source sélectionné et le nombre de colonnes dans ce fichier source.
* **Attribuer des champs de jeu de données et de mappage** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![L’étape de révision du workflow des sources.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données en continu pour les données [!DNL Snowflake]. Pour obtenir des ressources supplémentaires, consultez la documentation ci-dessous.

### Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données qui sont ingérées par celui-ci pour afficher des informations sur les taux d’ingestion, la réussite et les erreurs. Pour plus d’informations sur la manière de surveiller les flux de données en continu, consultez le tutoriel sur la [surveillance des flux de données en continu dans l’interface utilisateur](../../monitor-streaming.md).

### Mettre à jour votre flux de données

Pour mettre à jour les configurations de la planification, du mappage et des informations générales de vos flux de données, consultez le tutoriel sur la [mise à jour des flux de données de sources dans l’interface utilisateur](../../update-dataflows.md).

### Supprimer le flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]**, disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression des flux de données dans l’interface utilisateur](../../delete.md).
