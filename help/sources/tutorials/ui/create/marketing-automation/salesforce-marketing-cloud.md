---
title: Connexion de votre compte Salesforce Marketing Cloud à Experience Platform via l’interface utilisateur
description: Découvrez comment connecter votre compte Salesforce Marketing Cloud à Experience Platform via l’interface utilisateur.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 0c6a51d06e57eb6de063a350bd4b17022555a0b4
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 13%

---

# Connecter votre compte [!DNL Salesforce Marketing Cloud] à Experience Platform via l’interface utilisateur

>[!WARNING]
>
>La source [!DNL Salesforce Marketing Cloud] sera abandonnée en janvier 2026. Une nouvelle source sera publiée plus tard cette année comme alternative. Une fois la nouvelle source publiée, vous devez planifier la migration vers la nouvelle source en créant de nouvelles connexions de compte et de nouveaux flux de données avant la fin du mois de janvier 2026.

Lisez ce guide pour savoir comment connecter votre compte [!DNL Salesforce Marketing Cloud] à Adobe Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur d’Experience Platform.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL Salesforce Marketing Cloud], vous pouvez ignorer le reste de ce document et passer au tutoriel sur [l’importation de données d’automatisation du marketing dans Experience Platform à l’aide de l’interface utilisateur](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises

Lisez la [[!DNL Salesforce Marketing Cloud] présentation](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#prerequisites) pour plus d’informations sur l’authentification.

## Parcourir le catalogue des sources

>[!IMPORTANT]
>
>L’ingestion d’objets personnalisés n’est actuellement pas prise en charge par l’intégration source [!DNL Salesforce Marketing Cloud].


Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]*. Choisissez une catégorie ou utilisez la barre de recherche pour trouver votre source.

Pour vous connecter à [!DNL Salesforce Marketing Cloud], accédez à la catégorie *[!UICONTROL Automatisation du marketing]*, sélectionnez la carte source **[!UICONTROL Salesforce Marketing Cloud]**, puis sélectionnez **[!UICONTROL Configurer]**.

>[!TIP]
>
>Les sources du catalogue affichent l’option **[!UICONTROL Configurer]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois un compte authentifié créé, cette option devient **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources avec la carte source Salesforce Marketing Cloud sélectionnée.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

## Utiliser un compte existant {#existing}

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte [!DNL Salesforce Marketing Cloud] à utiliser.

![Interface des comptes existants dans le workflow des sources avec « Compte existant » sélectionné.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Créer un nouveau compte {#new}

Vous pouvez utiliser la source [!DNL Salesforce Marketing Cloud] pour vous connecter à Experience Platform sur [!DNL Azure] ou [!DNL Amazon Web Services] (AWS).

### Connexion à Experience Platform sur [!DNL Azure] {#azure}

Pour vous connecter à Experience Platform sur [!DNL Azure], indiquez un nom de compte, une description facultative et les informations d’authentification de votre [compte](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#azure). Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** et patientez quelques instants le temps que la connexion s’établisse.

![Nouvelle interface de compte dans le workflow des sources pour la connexion à Experience Platform sur Azure.](../../../../images/tutorials/create/salesforce-marketing-cloud/new-azure.png)

### Connexion à Experience Platform sur Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour vous connecter à Experience Platform sur [!DNL AWS], vérifiez que vous êtes dans un sandbox VA6 et fournissez un nom de compte, une description facultative et vos informations d’authentification [compte](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#aws). Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** et patientez quelques instants le temps que la connexion s’établisse.

![Nouvelle interface de compte dans le workflow des sources pour la connexion à Experience Platform sur AWS](../../../../images/tutorials/create/salesforce-marketing-cloud/new-aws.png)

## Créer un flux de données pour les données [!DNL Salesforce Marketing Cloud]

Maintenant que vous avez correctement connecté votre [!DNL Salesforce Marketing Cloud] , vous pouvez [créer un flux de données et ingérer les données de votre fournisseur d’automatisation marketing dans Experience Platform](../../dataflow/marketing-automation.md).
