---
title: Connecter Oracle DB à Experience Platform à l’aide de l’interface utilisateur
description: Découvrez comment connecter votre instance Oracle DB à Experience Platform à l’aide de l’interface utilisateur.
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 17%

---

# Créer une connexion source [!DNL Oracle DB] dans l’interface utilisateur

Lisez ce guide pour savoir comment connecter votre instance [!DNL Oracle DB] à Adobe Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur d’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Oracle DB], vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Lisez la [[!DNL Oracle DB] présentation](../../../../connectors/databases/oracle.md#prerequisites) pour plus d’informations sur l’authentification.

## Parcourir le catalogue des sources

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]*. Choisissez une catégorie ou utilisez la barre de recherche pour trouver votre source.

Pour vous connecter à [!DNL Oracle DB], accédez à la catégorie *[!UICONTROL Bases de données]*, sélectionnez la vignette source **[!UICONTROL Oracle DB]**, puis sélectionnez **[!UICONTROL Configurer]**.

>[!TIP]
>
>Les sources indiquent **[!UICONTROL Configurer]** pour les nouvelles connexions et **[!UICONTROL Ajouter des données]** si un compte existe déjà.

![Le catalogue de sources avec « Oracle DB » sélectionné.](../../../../images/tutorials/create/oracle/catalog.png)

## Utiliser un compte existant {#existing}

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte [!DNL Oracle DB] à utiliser.

![Interface des comptes existants dans le workflow des sources avec « Compte existant » sélectionné.](../../../../images/tutorials/create/oracle/existing.png)

## Créer un nouveau compte {#new}

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** puis indiquez un nom et éventuellement ajoutez une description pour votre compte.

### Se connecter à Experience Platform sur Azure {#azure}

Vous pouvez connecter votre base de données [!DNL Oracle DB] à Experience Platform sur Azure à l’aide d’une chaîne de connexion.

Pour utiliser l’authentification de chaîne de connexion, fournissez votre [chaîne de connexion](../../../../connectors/databases/oracle.md#azure) et sélectionnez **[!UICONTROL Se connecter à la source]**.

![Nouvelle interface de compte dans le workflow des sources avec « Authentification de chaîne de connexion » sélectionné.](../../../../images/tutorials/create/oracle/azure.png)

### Connexion à Experience Platform sur Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour créer un compte [!DNL Oracle DB] et vous connecter à Experience Platform sur AWS, vérifiez que vous vous trouvez dans un sandbox VA6, puis fournissez les informations d’identification [nécessaires pour l’authentification](../../../../connectors/databases/oracle.md#aws).

![Nouvelle interface de compte dans le workflow des sources pour se connecter à AWS.](../../../../images/tutorials/create/oracle/aws.png)

## Créer un flux de données pour les données [!DNL Oracle DB]

Maintenant que vous avez correctement connecté votre base de données [!DNL Oracle DB], vous pouvez [créer un flux de données et ingérer les données de votre base de données dans Experience Platform](../../dataflow/databases.md).
