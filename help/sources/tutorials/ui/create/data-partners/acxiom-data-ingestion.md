---
title: Ingestion de données Acxiom
description: Utilisez Acxiom Data Ingestion pour ingérer des données Acxiom dans Real-Time CDP et enrichir les profils propriétaires. Utilisez vos profils propriétaires enrichis par Acxiom pour améliorer les audiences et les activer sur l’ensemble des canaux marketing.
last-substantial-update: 2024-03-19T00:00:00Z
badge: Beta
exl-id: a0a080ef-4603-437f-8a68-11dbf530ac90
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 14%

---

# Créer une connexion source [!DNL Acxiom Data Ingestion] et un flux de données dans l’interface utilisateur

>[!NOTE]
>
>La source [!DNL Acxiom Data Ingestion] est en version Beta. Lisez les [termes et conditions](../../../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Utilisez la source de [!DNL Acxiom Data Ingestion] pour ingérer des données [!DNL Acxiom] dans Real-Time Customer Data Platform et enrichir les profils propriétaires. Ensuite, vous pouvez utiliser vos profils propriétaires enrichis de [!DNL Acxiom] pour améliorer les audiences et les activer sur l’ensemble des canaux marketing.

Lisez ce tutoriel pour savoir comment créer une connexion source [!DNL Acxiom Data Ingestion] et un flux de données à l’aide de l’interface utilisateur de Adobe Experience Platform. La source [!DNL Acxiom Data Ingestion] est utilisée pour récupérer et mapper la réponse [!DNL Acxiom] service d’amélioration à l’aide d’Amazon S3 comme point de dépôt.

## Conditions préalables {#prerequisites}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Collecter les informations d’identification requises

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| Clé d’authentification [!DNL Acxiom] | La clé d’authentification. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Clé d’accès [!DNL Amazon S3] | Identifiant de clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Clé secrète [!DNL Amazon S3] | L’identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |

>[!IMPORTANT]
>
>Pour connecter votre compte [!DNL Acxiom] à Experience Platform ]**les autorisations**[!UICONTROL  Afficher les sources et **[!UICONTROL Gérer les sources]** doivent être activées. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../../../access-control/ui/overview.md).

## Connecter votre compte [!DNL Acxiom]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Partenaires de données et d’identité]**, sélectionnez **[!UICONTROL Acxiom Data Ingestion]** puis **[!UICONTROL Configurer]**.

>[!TIP]
>
>Une carte source qui affiche **[!UICONTROL Ajouter des données]** signifie que la source dispose déjà d’un compte authentifié. D’un autre côté, une carte source qui affiche **[!UICONTROL Configurer]** signifie que vous devez fournir des informations d’identification et créer un compte pour utiliser cette source.

![Le catalogue des sources avec la source Acxiom sélectionnée.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-catalog.png)

### Créer un nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Acxiom]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte du workflow des sources.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-new-account.png)

| Informations d’identification | Description |
| --- | --- |
| Nom de compte | Nom du compte. |
| Description | (Facultatif) Brève explication de l’objectif du compte. |
| Clé d’authentification [!DNL Acxiom] | Clé [!DNL Acxiom] fournie par pour l’approbation du compte. Elle doit correspondre à la valeur appropriée avant qu’une connexion à la base de données puisse être établie.  Cette clé doit comporter 24 caractères et peut uniquement inclure : A-Z, a-z et 0-9. |
| Clé d’accès S3 | La clé d’accès S3 fait référence à l’emplacement S3 d’Amazon. Cette information est fournie par votre administrateur lorsque des autorisations de rôle S3 sont définies. |
| Clé secrète S3 | La clé secrète S3 fait référence à l’emplacement S3 d’Amazon. Cette information est fournie par votre administrateur lorsque des autorisations de rôle S3 sont définies. |
| s3SessionToken | (Facultatif) Valeur du jeton d’authentification lors de la connexion à S3. |
| serviceUrl | (Facultatif) Emplacement URL à utiliser lors de la connexion à S3 dans un emplacement non standard. |
| Nom du compartiment | (Facultatif) Nom du compartiment S3 configuré sur S3 qui sert de chemin de départ dans la sélection de données. |
| Chemin du dossier | Si des sous-répertoires dans un compartiment sont utilisés, vous pouvez également spécifier un chemin comme chemin de départ dans la sélection de données. |

### Utiliser un compte existant

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]**.

Sélectionnez un compte dans la liste pour en afficher les détails. Une fois que vous avez sélectionné un compte, cliquez sur **[!UICONTROL Suivant]** pour continuer.

![Interface de compte existante du workflow des sources.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-existing-account.png)

## Sélectionner les données

Sélectionnez le fichier à ingérer dans le compartiment et le sous-répertoire de votre choix. Un aperçu des données peut être fourni une fois le délimiteur et le type de compression définis. Une fois le fichier sélectionné, cliquez sur **[!UICONTROL Suivant]** pour continuer.

![Interface de sélection des données et de prévisualisation des fichiers du workflow des sources.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-preview.png)

>[!NOTE]
>
>Bien que les types de fichiers JSON et Parquet soient répertoriés, vous n’êtes pas tenu de les utiliser pendant le workflow source [!DNL Acxiom].

## Fournir des détails sur le jeu de données et le flux de données

Ensuite, vous devez fournir des informations concernant votre jeu de données et votre flux de données.

### Détails du jeu de données

>[!BEGINTABS]

>[!TAB Utiliser un nouveau jeu de données]

Un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les données correctement ingérées par Experience Platform sont conservées sous forme de jeux de données dans le lac de données. Pour utiliser un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**.

![Nouvelle interface du jeu de données.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-new-dataset.png)

| Détails du nouveau jeu de données | Description |
| --- | --- |
| Nom du jeu de données de sortie | Nom du nouveau jeu de données. |
| Description | (Facultatif) Brève explication de l’objectif du jeu de données. |
| Schéma | Liste déroulante des schémas qui existent dans votre organisation. Vous pouvez également créer votre propre schéma avant le processus de configuration de la source. Pour plus d’informations, consultez le guide sur la [création d’un schéma dans l’interface utilisateur](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Utiliser un jeu de données existant]

Pour utiliser un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**.

Vous pouvez sélectionner **[!UICONTROL Recherche avancée]** pour afficher une fenêtre de tous les jeux de données de votre organisation, y compris leurs détails respectifs, par exemple s’ils sont activés pour l’ingestion dans le profil client en temps réel.

![Interface du jeu de données existant.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-dataset.png)

>[!ENDTABS]

+++Sélectionnez pour connaître les étapes d’activation de l’ingestion de profil, des diagnostics d’erreur et de l’ingestion partielle.

Si votre jeu de données est activé pour le profil client en temps réel, au cours de cette étape, vous pouvez activer/désactiver le **[!UICONTROL jeu de données de profil]** pour activer vos données pour l’ingestion de profil. Vous pouvez également utiliser cette étape pour activer les **[!UICONTROL diagnostics d’erreur]** et **[!UICONTROL ingestion partielle]**.

* **[!UICONTROL Diagnostics d’erreur]** : sélectionnez **[!UICONTROL Diagnostics d’erreur]** pour demander à la source de générer des diagnostics d’erreur que vous pourrez référencer ultérieurement lors de la surveillance de l’activité du jeu de données et du statut du flux de données.
* **[!UICONTROL Ingestion partielle]** : l’ingestion par lots partielle est la possibilité d’ingérer des données contenant des erreurs, jusqu’à un certain seuil configurable. Cette fonctionnalité vous permet d’ingérer toutes vos données exactes dans Experience Platform, tandis que toutes vos données incorrectes sont traitées par lots séparément avec des informations sur les raisons de leur non-validité.

+++

### Détails du flux de données

Une fois votre jeu de données configuré, vous devez fournir des détails sur votre flux de données, y compris un nom, une description facultative et des configurations d’alerte.

![Interface des configurations des détails du flux de données.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-dataset-details.png)

| Configurations du flux de données | Description |
| --- | --- |
| Nom du flux de données | Nom du flux de données.  Par défaut, le nom du fichier importé est utilisé. |
| Description | (Facultatif) Brève description de votre flux de données. |
| Alertes | Experience Platform peut générer des alertes basées sur des événements auxquelles les utilisateurs et utilisatrices peuvent s’abonner. Ces options sont toutes exécutées dans un flux de données pour les déclencher.  Pour plus d’informations, reportez-vous à la présentation des alertes [](../../alerts.md) <ul><li>**Début d’exécution du flux de données des sources** : sélectionnez cette alerte pour recevoir une notification lorsque l’exécution du flux de données commence.</li><li>**Succès de l’exécution du flux de données des sources** : sélectionnez cette alerte pour recevoir une notification si votre flux de données se termine sans erreur.</li><li>**Échec de l’exécution du flux de données des sources** : sélectionnez cette alerte pour recevoir une notification si l’exécution de votre flux de données se termine par des erreurs.</li></ul> |

## Mappage

Utilisez l’interface de mappage pour mapper vos données source aux champs de schéma appropriés avant d’ingérer des données vers Experience Platform.  Pour plus d’informations, consultez le guide de mappage [ dans l’interface utilisateur](../../../../../data-prep/ui/mapping.md)

![L’interface de mappage.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-mapping.png)

## Planifier l’ingestion du flux de données

Ensuite, utilisez l’interface de planification pour définir le planning de l’ingestion de votre flux de données.

![Interface de configuration de la planification.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-scheduling.png)

| Configuration de la planification | Description |
| --- | --- |
| Fréquence | Configurez la fréquence pour indiquer la fréquence d’exécution du flux de données. Vous pouvez définir la fréquence sur : <ul><li>**Une fois** : définissez votre fréquence sur `once` pour créer une ingestion unique. Les configurations d’intervalle et de renvoi ne sont pas disponibles lors de la création d’un flux de données d’ingestion unique. Par défaut, la fréquence de planification est définie sur une seule fois.</li><li>**Minute** : définissez la fréquence sur `minute` pour planifier le flux de données afin d’ingérer les données par minute.</li><li>**Heure** : définissez la fréquence sur `hour` pour planifier l’ingestion des données par flux et par heure.</li><li>**Jour** : définissez la fréquence sur `day` pour planifier l’ingestion de données par jour dans le flux de données.</li><li>**Semaine** : définissez la fréquence sur `week` pour planifier l’ingestion de données par semaine dans le flux de données.</li></ul> |
| Intervalle | Une fois que vous avez sélectionné une fréquence, vous pouvez configurer le paramètre d’intervalle afin d’établir la période entre chaque ingestion. Par exemple, si vous définissez la fréquence sur jour et configurez l’intervalle sur 15, votre flux de données s’exécutera tous les 15 jours. Vous ne pouvez pas définir l’intervalle sur zéro. La valeur d’intervalle minimale acceptée pour chaque fréquence est la suivante :<ul><li>**Une fois** : s.o.</li><li>**Minute** : 15</li><li>**Heure** : 1</li><li>**Jour** : 1</li><li>**Semaine** : 1</li></ul> |
| Heure de début | Date et heure de l’exécution projetée, présentées dans le fuseau horaire UTC. |
| Renvoyer | Le renvoi détermine les données initialement ingérées. Si le renvoi est activé, tous les fichiers actuels du chemin spécifié seront ingérés lors de la première ingestion planifiée. Si le renvoi est désactivé, seuls les fichiers chargés entre la première exécution de l’ingestion et l’heure de début sont ingérés. Les fichiers chargés avant l’heure de début ne seront pas ingérés. |

## Vérifier le flux de données

Utilisez la page de révision pour obtenir un résumé de votre flux de données avant l’ingestion. Les détails sont regroupés dans les catégories suivantes :

* **Connexion** - Affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **Attribuer des champs de jeu de données et de mappage** - Affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.
* **Planification** - Affiche la période active, la fréquence et l’intervalle du planning d’ingestion.
Une fois que vous avez révisé votre flux de données, cliquez sur Terminer et patientez quelques instants le temps que le flux de données soit créé.

![Page de révision.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-review.png)

## Étapes suivantes

Ce tutoriel vous a permis de créer un flux de données pour importer des données par lots de votre source de [!DNL Acxiom] vers Experience Platform. Pour obtenir des ressources supplémentaires, consultez la documentation décrite ci-dessous.

### Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées et afficher les informations relatives au taux d’ingestion, aux succès et aux erreurs. Pour plus d’informations sur la surveillance des flux de données, consultez le tutoriel sur la [surveillance des comptes et des flux de données dans l’interface utilisateur](../../../../../dataflows/ui/monitor-sources.md).

### Mettre à jour votre flux de données

Pour mettre à jour les configurations pour la planification, le mappage et les informations générales de vos flux de données, consultez le tutoriel sur la [mise à jour des flux de données sources dans l’interface utilisateur](../../update-dataflows.md).

### Supprimer le flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]**, disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression de flux de données dans l’interface utilisateur](../../delete.md).

## Ressources supplémentaires {#additional-resources}

Pour plus d&#39;informations, consultez la [[!DNL Acxiom] InfoBase](https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf).
