---
keywords: Experience Platform;accueil;rubriques les plus consultées;connexion en continu;créer une connexion en continu;guide de l’interface utilisateur;tutoriel;créer une connexion en continu;ingestion en continu;ingestion ;
solution: Experience Platform
title: Création d’une connexion en continu d’API HTTP à l’aide de l’interface utilisateur
topic-legacy: tutorial
type: Tutorial
description: Ce guide de l’interface utilisateur vous aidera à créer une connexion en continu à l’aide d’Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: f5d341daffd7d4d77ee816cc7537b0d0c52ca636
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 10%

---


# Créez un [!DNL HTTP API] connexion en continu à l’aide de l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion à une source de diffusion en continu à l’aide du [!UICONTROL Sources] workspace.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Le cadre normalisé selon lequel [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel de l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md): Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Création d’une connexion en continu

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL Diffusion en continu]** catégorie, sélectionnez **[!UICONTROL API HTTP]** puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/http/catalog.png)

Le **[!UICONTROL Connexion au compte d’API HTTP]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte API HTTP avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existing-account](../../../../images/tutorials/create/http/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom de compte et une description facultative. Vous aurez également la possibilité de fournir les propriétés de configuration suivantes :

- **[!UICONTROL Authentification]:** Cette propriété détermine si la connexion en continu requiert ou non une authentification. L’authentification garantit que les données sont collectées auprès de sources approuvées. Si vous avez affaire à des informations d’identification personnelle, cette propriété doit être activée. Par défaut, cette propriété est désactivée.
- **[!UICONTROL Compatible XDM]:** Cette propriété indique si cette connexion en continu enverra des événements compatibles avec les schémas XDM. Par défaut, cette propriété est désactivée.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![new-account](../../../../images/tutorials/create/http/new.png)

## Sélectionner des données

Après avoir créé la connexion API HTTP, la variable **[!UICONTROL Sélectionner des données]** s’affiche, vous fournissant une interface pour charger et prévisualiser vos données.

Sélectionner **[!UICONTROL Chargement de fichiers]** pour charger vos données. Vous pouvez également faire glisser et déposer vos données dans le [!UICONTROL Glisser-déposer des fichiers] de l’interface.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Une fois les données chargées, vous pouvez utiliser le côté droit de l’interface pour prévisualiser la hiérarchie de fichiers. Sélectionner **[!UICONTROL Suivant]** pour continuer.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappage des champs de données à un schéma XDM

Le [!UICONTROL Mappage] s’affiche, fournissant une interface pour mapper les données source à un jeu de données Platform.

Les fichiers parquet doivent être conformes à XDM et ne nécessitent pas de configurer manuellement le mappage, tandis que les fichiers CSV nécessitent que vous configuriez explicitement le mappage, mais vous permettent de sélectionner les champs de données source à mapper. Les fichiers JSON, s’ils sont marqués comme une plainte XDM, ne nécessitent pas de configuration manuelle. Cependant, s’il n’est pas marqué comme compatible XDM, il vous faudra configurer explicitement le mappage.

Sélectionnez un jeu de données dans lequel ingérer les données entrantes. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Création d’un nouveau jeu de données

Pour créer un jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**. Sur le formulaire qui s’affiche, indiquez le nom, une description facultative, ainsi que le schéma cible du jeu de données. Si vous sélectionnez une [!DNL Profile]Schéma compatible, vous pouvez choisir si le jeu de données doit également être [!DNL Profile]-enabled.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### Utilisation d’un jeu de données existant

Pour utiliser un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Dans le formulaire qui s’affiche, sélectionnez le jeu de données à utiliser. Une fois que vous avez sélectionné un jeu de données, vous pouvez choisir si le jeu de données doit être [!DNL Profile]-enabled.

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### Mappage des champs standard


Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs calculées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, reportez-vous à la section [Guide de l’interface utilisateur de la préparation de données](../../../../../data-prep/ui/mapping.md).

Pour ajouter un nouveau champ source, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Un nouveau couplage champ source et champ cible s’affiche. Pour ajouter un nouveau champ source, cliquez sur l’icône de flèche en regard de l’option [!UICONTROL Sélectionner le champ source] la barre d’entrée.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Le [!UICONTROL Sélectionner des attributs] vous permet d’explorer votre hiérarchie de fichiers et de sélectionner un champ source spécifique à mapper à un champ XDM cible. Une fois que vous avez sélectionné le champ source à mapper, sélectionnez **[!UICONTROL Sélectionner]** pour continuer.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Lorsqu’un champ source est sélectionné, vous pouvez désormais identifier le champ XDM cible approprié à mapper. Sélectionnez l&#39;icône de schéma sous la section du champ cible .

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Le [!UICONTROL Faire correspondre le champ source au champ cible] s’affiche, vous fournissant une interface pour explorer le schéma de votre jeu de données cible. Sélectionnez le champ cible correspondant à votre champ source, puis sélectionnez **[!UICONTROL Sélectionner]** pour continuer.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Une fois que vos champs sources sont tous mappés à leurs champs XDM cibles appropriés, sélectionnez **[!UICONTROL Suivant]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Détails du flux de données

Le **[!UICONTROL Détails du flux de données]** s’affiche. Sur cette page, vous pouvez fournir des détails sur le flux de données créé en attribuant un nom et une description facultative.

Après avoir fourni des détails sur le flux de données, sélectionnez **[!UICONTROL Suivant]**.

![dataflow-detail](../../../../images/tutorials/create/http/dataflow-detail.png)

## Révision

Le **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de consulter les détails de votre flux de données avant qu’il ne soit créé. Les détails sont regroupés dans les catégories suivantes :

- **[!UICONTROL Connexion]**: Affiche le nom du compte, la plateforme source et le nom de la source.
- **[!UICONTROL Attribution de champs de jeu de données et de mappage]**: Affiche le jeu de données cible et le schéma auquel le jeu de données adhère.

Une fois que les détails sont corrects, sélectionnez **[!UICONTROL Terminer]**.

![review](../../../../images/tutorials/create/http/review.png)

## Obtention de l’URL du point de terminaison de diffusion

Une fois la connexion créée, la page des détails des sources s’affiche. Cette page affiche les détails de la connexion que vous venez de créer, y compris les flux de données, l’identifiant et l’URL du point de terminaison de diffusion en continu précédemment exécutés.

![endpoint](../../../../images/tutorials/create/http/endpoint.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion HTTP en continu, ce qui vous permet d’utiliser le point de terminaison de diffusion pour accéder à diverses [!DNL Data Ingestion] API. Pour savoir comment créer une connexion en continu dans l’API, consultez le [tutoriel sur la création d’une connexion en continu](../../../api/create/streaming/http.md).

Pour savoir comment diffuser des données vers Platform, veuillez lire le tutoriel sur [diffusion en continu de données de série temporelle](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou du tutoriel sur [données d’enregistrement en continu](../../../../../ingestion/tutorials/streaming-record-data.md).
