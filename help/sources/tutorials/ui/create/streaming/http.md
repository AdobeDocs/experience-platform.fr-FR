---
keywords: Experience Platform ; accueil ; rubriques populaires ; connexion en flux continu ; créer une connexion en flux continu ; guide ui ; didacticiel ; créer une connexion en flux continu ; assimilation en flux continu ; assimilation ;
solution: Experience Platform
title: Création d’une connexion de diffusion en continu à l’aide de l’interface utilisateur
topic: tutorial
type: Tutorial
description: Ce guide de l’interface utilisateur vous aidera à créer une connexion en continu à l’aide d’Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a4019227abaddd9dbe143899d273580ebf21849e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 18%

---


# Création d’une connexion en continu à l’aide de l’interface utilisateur

Ce guide de l’interface utilisateur vous aidera à créer une connexion en continu à l’aide d’Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Création d’une connexion en continu

Après vous être connecté à l&#39;interface utilisateur [!DNL Experience Platform], sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Diffusion en flux continu]**, sélectionnez **[!UICONTROL API HTTP]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur de flux continu HTTP.

![](../../../../images/tutorials/create/http/catalog.png)

La page **[!UICONTROL Connect HTTP API account]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom de compte et une description facultative. Vous aurez également la possibilité de fournir les propriétés de configuration suivantes :

- **[!UICONTROL Authentification] :** cette propriété détermine si la connexion en flux continu nécessite ou non une authentification. L’authentification garantit que les données sont collectées auprès de sources approuvées. Si vous utilisez des informations d’identification personnelle, cette propriété doit être activée. Par défaut, cette propriété est désactivée.
- **[!UICONTROL Compatibilité] des Schémas XDM :** cette propriété indique si cette connexion en flux continu envoie des événements compatibles avec les schémas XDM. Par défaut, cette propriété est activée.

Une fois terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/http/new-account.png)

### Compte existant

Pour vous connecter à l’aide des informations d’identification existantes, sélectionnez la connexion de l’API HTTP que vous souhaitez utiliser, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/http/existing-account.png)

## Sélectionner des données

Après avoir créé la connexion à l&#39;API HTTP, l&#39;étape **[!UICONTROL Sélectionner les données]** s&#39;affiche, fournissant une interface pour choisir le jeu de données auquel se connecter. Vous avez la possibilité de créer un nouveau jeu de données ou de vous connecter à un jeu de données existant.

### Création d’un nouveau jeu de données

Pour créer un jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**. Dans le formulaire qui s’affiche, indiquez le nom, une description facultative, ainsi que le schéma de cible du jeu de données. Si vous sélectionnez un schéma activé par Profil, vous pouvez choisir si le jeu de données doit également être activé par Profil.

![](../../../../images/tutorials/create/http/new-dataset.png)

### Utilisation d’un jeu de données existant

Pour utiliser un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Dans le formulaire qui s&#39;affiche, sélectionnez le jeu de données à utiliser. Une fois que vous avez sélectionné un jeu de données, vous pouvez choisir si le jeu de données doit être activé par Profil.

![](../../../../images/tutorials/create/http/existing-dataset.png)

## Détails du flux de données

L&#39;étape **[!UICONTROL Détails du flux de données]** s&#39;affiche. Sur cette page, vous pouvez fournir des détails sur le flux de données créé en attribuant un nom et une description facultative.

Après avoir fourni des détails pour le flux de données, sélectionnez **[!UICONTROL Suivant]**.

![](../../../../images/tutorials/create/http/dataflow-detail.png)

## Révision

L&#39;étape **[!UICONTROL Réviser]** s&#39;affiche, vous permettant de vérifier les détails de votre flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

- **[!UICONTROL Connexion]** : Affiche le nom du compte, la plateforme source et le nom de la source.
- **[!UICONTROL Affectez un jeu de données et des champs]** de mappage : Affiche le jeu de données de cible et le schéma auquel il adhère.

Après avoir confirmé que les détails sont corrects, sélectionnez **[!UICONTROL Terminer]**.

![](../../../../images/tutorials/create/http/review.png)

## Obtenir l’URL du point de terminaison de flux continu

Une fois la connexion créée, la page des détails des sources s&#39;affiche. Cette page présente les détails de votre nouvelle connexion, notamment les flux de données, l’ID et l’URL du point de terminaison de diffusion en continu précédemment exécutés.

![](../../../../images/tutorials/create/http/get-streaming-url.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion HTTP en flux continu, ce qui vous permet d’utiliser le point de terminaison de flux continu pour accéder à diverses API [!DNL Data Ingestion]. Pour savoir comment créer une connexion en continu dans l’API, consultez le [tutoriel sur la création d’une connexion en continu](../../../api/create/streaming/http.md).

Pour savoir comment diffuser les données sur la plateforme, veuillez lire le didacticiel sur [les données de séries chronologiques en flux continu](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou le didacticiel sur [les données d&#39;enregistrement en flux continu](../../../../../ingestion/tutorials/streaming-record-data.md).
