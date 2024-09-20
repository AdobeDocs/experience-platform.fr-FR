---
title: Création d’une connexion Google Big Query Source dans l’interface utilisateur
description: Découvrez comment créer une connexion source Google Big Query à l’aide de l’interface utilisateur de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 55aaaa39659566de81bb161d704b6f8212e29a8b
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 39%

---

# Créer une connexion source [!DNL Google BigQuery] dans l’interface utilisateur

>[!IMPORTANT]
>
>La source [!DNL Google BigQuery] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce tutoriel pour apprendre à connecter votre compte [!DNL Google BigQuery] à Adobe Experience Platform à l’aide de l’interface utilisateur.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Google BigQuery] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Lisez le [[!DNL Google BigQuery] guide d&#39;authentification](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) pour obtenir des instructions détaillées sur la collecte de vos informations d&#39;identification requises.

## Connexion à votre compte Google BigQuery

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Sous la catégorie [!UICONTROL Bases de données], sélectionnez **[!UICONTROL Google BigQuery]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les sources dans le catalogue des sources affichent l’option **[!UICONTROL Configurer]** lorsqu’une source donnée n’a pas encore de compte authentifié. Une fois qu’il existe un compte authentifié, cette option devient **[!UICONTROL Ajouter des données]**.

![Catalogue de sources avec Google BigQuery sélectionné.](../../../../images/tutorials/create/google-big-query/catalog.png)

La page **[!UICONTROL Se connecter à Google Big Query]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Google BigQuery] auquel vous souhaitez vous connecter, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

![Page de compte existante où une liste de comptes existants est présentée.](../../../../images/tutorials/create/google-big-query/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouveau compte [!DNL Google BigQuery].

![Nouvelle interface de compte dans le workflow des sources.](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB  Utilisation de l’authentification de base ]

Pour utiliser l’authentification de base, sélectionnez **[!UICONTROL Authentification de base]** et fournissez des valeurs pour votre [projet, identifiant client, secret client, jeton d’actualisation et (facultatif) identifiant de jeu de données de résultats volumineux](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** et attendez quelques instants pour établir la connexion.

![Nouvelle interface de compte dans laquelle l’authentification de base est sélectionnée.](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB Utiliser l’authentification de service]

Pour utiliser l’authentification du service, sélectionnez **[!UICONTROL Authentification de service]** et fournissez des valeurs pour votre [ ID de projet, contenu de fichier clé et (facultatif) identifiant de jeu de données de résultats volumineux](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** et attendez quelques instants pour établir la connexion.

![Nouvelle interface de compte dans laquelle l’authentification de service est sélectionnée.](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Google BigQuery]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/databases.md).
