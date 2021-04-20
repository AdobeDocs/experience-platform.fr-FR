---
keywords: Experience Platform ; accueil ; rubriques populaires ; connexion en flux continu ; créer une connexion en flux continu ; guide ui ; didacticiel ; créer une connexion en flux continu ; assimilation en flux continu ; assimilation ;
solution: Experience Platform
title: Création d’une connexion de diffusion en continu à l’aide de l’interface utilisateur
topic: didacticiel
type: Tutorial
description: Ce guide de l’interface utilisateur vous aidera à créer une connexion en continu à l’aide d’Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
translation-type: tm+mt
source-git-commit: 3b71f1399a770e097cf75827e626d6d4e289ab77
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 10%

---


# Création d’une connexion en continu à l’aide de l’interface utilisateur

Ce didacticiel décrit les étapes à suivre pour créer une connexion source de flux continu à l’aide de l’espace de travail [!UICONTROL Sources].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Création d’une connexion en continu

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Diffusion en flux continu]**, sélectionnez **[!UICONTROL API HTTP]**, puis **[!UICONTROL Ajouter les données]**.

![catalogue](../../../../images/tutorials/create/http/catalog.png)

La page **[!UICONTROL Connect HTTP API account]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte d’API HTTP avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![compte existant](../../../../images/tutorials/create/http/existing.png)

### Nouveau compte

Si vous créez un nouveau compte, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom de compte et une description facultative. Vous aurez également la possibilité de fournir les propriétés de configuration suivantes :

- **[!UICONTROL Authentification] :** cette propriété détermine si la connexion en flux continu nécessite ou non une authentification. L’authentification garantit que les données sont collectées auprès de sources approuvées. Si vous utilisez des informations d’identification personnelle, cette propriété doit être activée. Par défaut, cette propriété est désactivée.
- **[!UICONTROL Compatible] XDM :** cette propriété indique si cette connexion en flux continu envoie des événements compatibles avec les schémas XDM. Par défaut, cette propriété est désactivée.

Une fois terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis **[!UICONTROL Suivant]** pour continuer.

![nouveau compte](../../../../images/tutorials/create/http/new.png)

## Sélectionner des données

Après avoir créé la connexion à l&#39;API HTTP, l&#39;étape **[!UICONTROL Sélectionner les données]** s&#39;affiche, vous offrant une interface pour télécharger et prévisualisation vos données.

Sélectionnez **[!UICONTROL Télécharger les fichiers]** pour télécharger vos données. Vous pouvez également faire glisser et déposer vos données dans la section [!UICONTROL Glisser et déposer des fichiers] de l’interface.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Une fois vos données téléchargées, vous pouvez utiliser le côté droit de l’interface pour prévisualisation la hiérarchie des fichiers. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![prévisualisation-exemple-données](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappage des champs de données à un schéma XDM

L’étape [!UICONTROL Mappage] s’affiche, fournissant une interface permettant de mapper les données source à un jeu de données de plateforme.

Les fichiers de parquet doivent être conformes à XDM et ne nécessitent pas de configuration manuelle du mappage, tandis que les fichiers CSV nécessitent de configurer explicitement le mappage, mais vous permettent de sélectionner les champs de données source à mapper. Les fichiers JSON, s’ils sont marqués comme plainte XDM, ne nécessitent pas de configuration manuelle. Cependant, si elle n’est pas marquée comme compatible XDM, vous devrez configurer explicitement le mappage.

Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez soit utiliser un jeu de données existant, soit en créer un nouveau.

### Création d’un nouveau jeu de données

Pour créer un jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**. Dans le formulaire qui s’affiche, indiquez le nom, une description facultative, ainsi que le schéma de cible du jeu de données. Si vous sélectionnez un schéma activé [!DNL Profile], vous pouvez choisir si le jeu de données doit également être activé [!DNL Profile].

![nouveau jeu de données](../../../../images/tutorials/create/http/new-dataset.png)

### Utilisation d’un jeu de données existant

Pour utiliser un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Dans le formulaire qui s&#39;affiche, sélectionnez le jeu de données à utiliser. Une fois que vous avez sélectionné un jeu de données, vous pouvez choisir si le jeu de données doit être activé [!DNL Profile].

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### Mise en correspondance des champs standard

En fonction de vos besoins, vous pouvez choisir de mapper directement les champs ou utiliser les fonctions de prép de données pour transformer les données source afin de dériver des valeurs calculées ou calculées. Pour plus d&#39;informations sur les fonctions de mappage et de mappage de données, consultez le didacticiel [mappage des données CSV aux champs de schéma XDM](../../../../../ingestion/tutorials/map-a-csv-file.md).

Pour ajouter un nouveau champ source, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Un nouveau couplage des champs source et de cible s’affiche. Pour ajouter un nouveau champ source, sélectionnez l’icône en forme de flèche en regard de la barre d’entrée [!UICONTROL Sélectionner le champ source].

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Le panneau [!UICONTROL Sélectionner des attributs] vous permet d&#39;explorer la hiérarchie de fichiers et de sélectionner un champ source spécifique à mapper à un champ XDM de cible. Une fois que vous avez sélectionné le champ source à mapper, sélectionnez **[!UICONTROL Sélectionner]** pour continuer.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Avec un champ source sélectionné, vous pouvez maintenant identifier le champ XDM de cible à mapper. Sélectionnez l’icône de schéma sous la section Champ de cible.

![sélectionner-cible-champ](../../../../images/tutorials/create/http/select-target-field.png)

La fenêtre [!UICONTROL Faire correspondre le champ source au champ de cible] s&#39;affiche, vous offrant ainsi une interface pour explorer le schéma de votre jeu de données de cible. Sélectionnez le champ de cible correspondant à votre champ source, puis sélectionnez **[!UICONTROL Sélectionner]** pour continuer.

![zone de mappage à cible](../../../../images/tutorials/create/http/map-to-target-field.png)

Une fois que vos champs source sont tous mappés à leurs champs XDM de cible appropriés, sélectionnez **[!UICONTROL Suivant]**.

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Détails du flux de données

L&#39;étape **[!UICONTROL Détails du flux de données]** s&#39;affiche. Sur cette page, vous pouvez fournir des détails sur le flux de données créé en attribuant un nom et une description facultative.

Après avoir fourni des détails pour le flux de données, sélectionnez **[!UICONTROL Suivant]**.

![détails du flux de données](../../../../images/tutorials/create/http/dataflow-detail.png)

## Révision

L&#39;étape **[!UICONTROL Réviser]** s&#39;affiche, vous permettant de vérifier les détails de votre flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

- **[!UICONTROL Connexion]** : Affiche le nom du compte, la plateforme source et le nom de la source.
- **[!UICONTROL Affectez un jeu de données et des champs]** de mappage : Affiche le jeu de données de cible et le schéma auquel il adhère.

Après avoir confirmé que les détails sont corrects, sélectionnez **[!UICONTROL Terminer]**.

![examiner](../../../../images/tutorials/create/http/review.png)

## Obtenir l’URL du point de terminaison de flux continu

Une fois la connexion créée, la page des détails des sources s&#39;affiche. Cette page présente les détails de votre nouvelle connexion, notamment les flux de données, l’ID et l’URL du point de terminaison de diffusion en continu précédemment exécutés.

![point de terminaison](../../../../images/tutorials/create/http/endpoint.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion HTTP en flux continu, ce qui vous permet d’utiliser le point de terminaison de flux continu pour accéder à diverses API [!DNL Data Ingestion]. Pour savoir comment créer une connexion en continu dans l’API, consultez le [tutoriel sur la création d’une connexion en continu](../../../api/create/streaming/http.md).

Pour savoir comment diffuser les données sur la plateforme, veuillez lire le didacticiel sur [les données de séries chronologiques en flux continu](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou le didacticiel sur [les données d&#39;enregistrement en flux continu](../../../../../ingestion/tutorials/streaming-record-data.md).
